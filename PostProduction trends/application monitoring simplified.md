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
  
* Different signals have different levels of importance to an application’s health. 
  * For example, a latency increase is less critical than error rate increase and some error codes are less critical than others. 
  * A canary launch two layers downstream might not be as significant as a deployment immediately upstream. 
* A regional traffic shift means one region ends up with zero traffic while another region has double. You can imagine the impact that has on metrics. A metric’s meaning determines how we should interpret it. Telltale takes all those factors into consideration when constructing its view of application health. The application health model is the heart of Telltale.

#### Intelligent Monitoring

* Every service operator knows the difficulty of alert tuning. 
  * Set thresholds too low and you get a deluge of spurious alerts. So you overcompensate and relax the tuning to the point of missing important health warnings. The end result is a lack of trust in alerts.
  * We make setup and configuration easy for application owners by providing curated and managed signal packs. These packs are combined into application profiles to address most common service types. 
  * Telltale automatically tracks dependencies between services to build the topology used in the application health model. Signal packs and topology detection keep configuration up-to-date with minimal effort. Those who want a more hands-on approach can still do manual configuration and tuning.
  * No single algorithm can account for the wide variety of signals we use. So, instead, we employ a mix of algorithms including statistical, rule based, and machine learning. 
  * **Intelligent monitoring means results our users can trust. It means a faster time to detection and a faster time to resolution during an incident.**
  
#### Intelligent Alerting
* Intelligent monitoring yields intelligent alerting. 
  * Telltale creates an issue when it detects a health problem in your application’s ecosystem. 
  * Teams can opt in to alerting via Slack, email, or PagerDuty (all powered by our internal alerting system). 
  * If the issue is caused by an upstream or downstream system then Telltale’s context-aware routing alerts that team instead. Intelligent alerting also means a team receives a single notification, alert storms are a thing of the past.
![slack](https://miro.medium.com/max/676/0*ekggl_Oabo2vJocj)
  * When a problem strikes, it’s essential to have the right information. Our **Slack alerts also start a thread containing only the most relevant context about the incident.** This includes the signals that Telltale identified as unhealthy and the reasons why. The right context provides a better understanding of the application’s current state so the on-call engineer can return it to health. 

* Incidents evolve and have their own lifecycle, so updates are essential. 
  * Are things getting better or worse? Are there new signals or events to consider? Telltale updates the Slack thread as the current incident unfolds. 
  * The thread is marked Resolved upon return to healthy state so users know, at a glance, which incidents are ongoing and which have been successfully remediated.
  * But these Slack threads aren’t just for Telltale. Teams use them to share additional data, observations, theories, and discussion about the incident. Incident data and discussion all in one thread makes for shared understanding, faster resolution, and easier post-incident analysis.
  * We strive to improve the quality of Telltale alerts. One way to do that is to learn from our users. So we provide feedback buttons right in the Slack message. Users can tell us to suppress future occurrences of an alert. Or provide a reason for why an alert isn’t actionable. Intelligent alerting means alerts our users can trust.
![alerts](https://miro.medium.com/max/577/0*oXj7Nyz9LZPOmpMZ)

### Why Is My Service Unhealthy?
* A wide variety of signals, knowledge of the application’s ecosystem, and correlation of signals across multiple services helps Telltale to detect the possible causes of an application’s degraded health. Causes such as an outlier instance, a canary or deployment by a dependent service, an unhealthy database, or just a spike in traffic. Highlighting possible causes saves valuable time during an incident.

### Incident Management
![incident](https://miro.medium.com/max/700/0*p6sSp5oj_A_mPVVy)
* When Telltale sends an alert it also creates a snapshot that has references to the unhealthy signals. As new information arrives, it’s added to this snapshot. 
  * This simplifies the post-incident review process for many teams. 
  * When it’s time to review past issues, the Application Incident Summary feature shows all aspects of recent issues in a single place including key metrics like total downtime and MTTR (Mean Time To Resolution). 
  * We want to help our teams see larger patterns of incidents so they can improve overall service availability.
  
![patterns](https://miro.medium.com/max/604/0*ZfKPKbIU-PNGF5NN)

[Source](https://netflixtechblog.com/telltale-netflix-application-monitoring-simplified-5c08bfa780ba)
