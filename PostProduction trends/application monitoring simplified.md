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

[Source](https://netflixtechblog.com/telltale-netflix-application-monitoring-simplified-5c08bfa780ba)
