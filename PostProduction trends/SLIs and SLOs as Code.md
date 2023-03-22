## SLIs and SLOs as Code

* Since Google first popularized service-level indicators (SLIs) and service-level objectives (SLOs) as part of their site reliability engineering (SRE) practice, observability tools like Datadog, Honeycomb and Dynatrace started incorporating SLO monitoring into their toolchains. 
* OpenSLO is an emerging standard that allows defining SLIs and SLOs as code, using a declarative, vendor-neutral specification language based on the YAML format used by Kubernetes. While the standard is still quite new, we're seeing some encouraging momentum, as with Sumo Logic's contribution of the [slogen](https://github.com/OpenSLO/slogen) tool to generate monitoring and dashboards. 
* We're excited by the promise of versioning SLI and SLO definitions in code and updating observability tooling as part of the CI/CD pipeline of the service being deployed.
