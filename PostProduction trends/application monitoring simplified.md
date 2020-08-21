## Application Monitoring Simplified
### How Netflix built TellTale

* Over the years we’ve learned from on-call engineers about the pain points of application monitoring: too many alerts, too many dashboards to scroll through, and too much configuration and maintenance. 
  *  Our streaming teams need a monitoring system that enables them to quickly diagnose and remediate problems; seconds count! 
  *  Our Node team needs a system that empowers a small group to operate a large fleet. 
  
![telltale](https://miro.medium.com/max/700/0*otr8oTJj6Azt457O)

* Telltale combines a variety of data sources to create a holistic view of an application’s health. Telltale learns what constitutes typical health for an application, no alert tuning required. And because we know what’s healthy, we can let application owners know when their services are trending towards unhealthy.

* Metrics are a key part of understanding application health. But sometimes you can have too many metrics, too many graphs, and too many dashboards. '
  * Telltale shows only the relevant data from the application plus that of upstream and downstream services. 
  * We use colors to indicate severity (users can opt to have Telltale display numbers in addition to colors) so users can tell, at a glance, the state of their application’s health. 
  * We also highlight interesting broader events such as regional traffic evacuations and nearby deployments, information that is vital to understanding health holistically. Especially during an incident.

* That is our Telltale vision. It exists today and monitors the health of over 100 Netflix production-facing applications.
![netflix](https://miro.medium.com/max/700/0*cTKhcfxS_XD5L-9n)

### The Application Health Model
* A microservice doesn’t live in isolation. It usually has dependencies, talks to other services, and lives in different AWS regions. 
 * The call graph above is a relatively simple one, they can be much deeper with dozens of services involved. An application is part of an ecosystem that can be subtly influenced by property changes or radically altered by region-wide events. 
 * The launch of a canary can affect an application. As can an upstream or downstream deployments.

* Telltale uses a variety of signals from multiple sources to assemble a constantly evolving model of the application’s health:
 * [Atlas](https://netflixtechblog.com/introducing-atlas-netflixs-primary-telemetry-platform-bd31f4d8ed9a) time series metrics.
 * [Regional traffic evacuations](https://netflixtechblog.com/project-nimble-region-evacuation-reimagined-d0d0568254d4)
 * [Mantis](https://netflixtechblog.com/open-sourcing-mantis-a-platform-for-building-cost-effective-realtime-operations-focused-5b8ff387813a) real-time streaming data.
 * Infrastructure change events.
 * [Canary](https://netflixtechblog.com/automated-canary-analysis-at-netflix-with-kayenta-3260bc7acc69) launches and [deployments](https://netflixtechblog.com/global-continuous-delivery-with-spinnaker-2a6896c23ba7)
 * The health of upstream and downstream services.
 * [Client metrics and QoE changes](https://netflixtechblog.com/optimizing-the-netflix-streaming-experience-with-data-science-725f04c3e834)
 * Alerts triggered by our alerting platform.

[Source](https://netflixtechblog.com/telltale-netflix-application-monitoring-simplified-5c08bfa780ba)
