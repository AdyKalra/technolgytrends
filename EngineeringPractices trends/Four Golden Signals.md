# Distributed Monitoring 101: the “Four Golden Signals”

* In monitoring distributed systems, Google’s SRE book outlines the four golden signals of monitoring as LETS 
  #### **Latency, Errors, Traffic, and Saturation.**

## Summary
* In monitoring distributed systems, Google’s SRE book outlines the four golden signals of monitoring as latency, traffic, errors and saturation. If I could wave a magic wand and immediately improve the culture of an organization, then I would have service-level objectives (SLOs) tied to these four metrics. But going back to habit formation: If you make acquiring a habit too difficult upfront, then an engineering team will ultimately reject it. So if your organization isn’t mature enough to create SLOs, simply beginning to track these metrics will up-level your game tremendously. They will give you an understanding of what is not working well and help guide your priorities.

* **Dreaming** Imagine a world where, after a major incident happens, the points of failure involved become DNR(Do Not Repeat) work. The same failure is not allowed to happen again and no new feature work will be completed until the fixes are implemented. And more importantly, no new feature work will be completed until those fixes are verified via a chaos engineering experiment, which is then cataloged and run continuously against your system. Then you take that knowledge and share it with other teams so they can run the same experiments and make sure they are immune to those failures as well.

[SRE Book](https://landing.google.com/sre/sre-book/chapters/foreword/)

* A big part of our work within the DevOps team lately has been to empower dev teams to take responsibility. Responsibility for their services’ availability, reliability and code quality. We first needed to reduce the anxiety that comes with such duties. A good way to do so is to start by giving developers enough visibility to diagnose a problem when it occurs. A good way to give visibility over a system’s state is to implement monitoring.

* **Latency**, which is the time it takes to serve a request. We should separate success latency from error latency and watch them both. In fact, success latency is important, but also a long error is more frustrating than a short one.

* **Traffic**, which is a high-level measure of how requested our service is. In the case of an API, this would be the number of queries received every second. For a music streaming service, that would be the amount of data streamed per second.

* **Errors**. Another important indicator is our service’s error rate. These errors can be both explicit (500 error codes for example) or implicit. An implicit error would be a successful response but with the wrong content or long response time.

* **Saturation** is the last of the “Golden Signals”. Saturation is about how “full” our service is. How much more load can it handle? Services are usually either CPU-constrained or memory-constrained. In either case, you should watch any constraining parameter. For a database system, you will want to watch available storage space.

## How to monitor?
* First, let’s talk about our technical stack. We tend to use popular tools over custom solutions. We only use custom code whenever we are not satisfied with the already available options. We deploy most of our services in Kubernetes environments. We instrument our code to expose metrics about each of our custom services. To collect these metrics and make sure they are scraped by Prometheus, we use one of Prometheus’ client libraries. There are client libraries for almost every popular language. The documentation also provides you with all the information you need to write your own.
* For third-party open-source services we usually rely on the community’s exporters. Exporters are an additional piece of software that helps scrape metrics from a service and format them for Prometheus. They are typically used with services that weren’t designed to expose metrics using the Prometheus format.
* We send metrics through our pipeline then store them as time-series in Prometheus. We also use Kubernetes’ kube-state-metrics to collect and send system metrics to Prometheus. We can then build our Grafana dashboarding and alerting systems by querying Prometheus. We aren’t going to get into too many technical details in this article, but feel free to go check them out. They are pretty easy to get started with and their documentations were very helpful.

### Latency
* Latency corresponds to the time it takes to serve a request. As stated a few lines above, we separate both success and error latencies. We didn’t want errors to false our success latency, but we also wanted to measure error latency.
* A common mistake people make is averaging the latency: while it could work, it’s not always a good idea. You should look at latency distribution instead, as it fits availability requirements better. In fact, a common Service Level Indicator (SLI) is the part of requests served faster than a threshold. The following is an example of Service Level Objective (SLO) for that SLI:
  * “Over a 24-hour period, serve 99% of requests faster than 1 second”
* An easy way to measure that is to store latency metrics as histogram time-series. We put our metrics into buckets that our exporters collect every minute. This way we can calculate the n-quantiles for our services’ latencies. For 0 < n < 1 and a histogram with q values, the n-quantile of that histogram is the value that ranks n*q amongst the q values. This means the 0.5-quantile (aka. the median) for a histogram with x entries is the value for which half of the x values are smaller or equal.
![Latency](https://miro.medium.com/max/2000/1*Tj1pExwN5WyK8cdhqquUJg.png)

* On the above graph, we can see that most of the time, our API serves 99% of our requests in under 1 second. Yet, we see spikes at around 2 seconds, which would not be ok with the SLO earlier.
* Now, because we are using Prometheus, we must be very careful with the bucket sizes we pick. Prometheus allows for both linear and exponential bucket sizes. It doesn’t really matter which of the two options you choose. As long as you factor estimation errors in your choice, you’re good to go. Prometheus doesn’t give the exact value for a quantile. It actually detects which of the buckets that quantile is in. Once it has done that, it uses linear interpolation to give an estimated value.

### Traffic
* To measure traffic for the API, we want to count how many requests it receives every second. Now, because we only get new metrics every minute, we can’t get an exact value for a given second. We use Prometheus’ rate and irate functions to work with averaged numbers of queries per second instead.
 * To display this information, we use the Grafana SingleStat panel. It allows us to give the current average of queries per second, and to display its trend in the background.
 ![grafana](https://miro.medium.com/max/1400/1*EZzI7WgwUasiLvITbmRu7w.png)
 * What we are looking for here is to be able to see sudden changes in the number of queries per second. This way, we can immediately know there is a problem when our traffic gets divided by 2 in just a few minutes.
 
### Errors
* The explicit error rate is pretty easy to compute, as we only need to divide HTTP 500s served by the total number of requests served. Like for traffic, we use an averaged value.
* The only thing we are careful about is picking the same average intervals as for traffic. It makes it easier to get an idea of the error traffic without duplicating panels.
For example, let’s say we have a 10% error rate and 200 queries per second over the last five minutes. It is now easy to deduce that we’ve had an average of 20 errors per second over the last 5 minutes.
### Saturation
* To watch a service’s saturation, we need to determine its constraining parameters. For this API, we started by measuring both CPU and Memory usage, as we initially didn’t know which of the two we needed to watch. Kubernetes internals and kube-state-metrics allow us to get such metrics for containers.
![Saturation](https://miro.medium.com/max/2000/1*hpMomTl1UgkZsIOb83XSjw.png)
* Measuring saturation can also be useful to predict an outage and capacity planning. Take a database’s storage for instance: we can measure both the available disk space and its fill rate. This way we can have an idea of the moment we need to take action.

### Using drill-down dashboards to monitor distributed services
* Let’s now consider another service: say a distributed API that acts as a proxy to other services. The API now has multiple instances, possibly in many regions. Also, the API now has a few different endpoints. Each of them relying on a different set of services. Soon enough, it becomes quite difficult to read graphs with dozens of series. We need to monitor the system as a whole, but still be able to detect individual failures.
* To do so, we use drill-down dashboards. Each panel of a given dashboard gives a global view of the system and clicking on it gives a more detailed view. For saturation, we use simple colored rectangles instead of graphs with CPU and RAM usage. Whenever an API’s resource usage exceeds a predefined threshold, the rectangle becomes orange.

![drill](https://miro.medium.com/max/1400/1*d32wYpkqyXBmBWd0C4aXRg.png)
* This way we only need to click on that rectangle to access a more detailed view. In said view, we display even more colored squares, each of them representing an API instance.
![distributed](https://miro.medium.com/max/2000/1*Rvi5Bax0_jmx93gHC-Pmlw.png)
