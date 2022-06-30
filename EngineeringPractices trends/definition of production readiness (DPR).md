## Definition of production readiness (DPR)

- In an organization that practices the **"you build it, you run it"** principle, a definition of production readiness (DPR) is a useful technique to support teams in assessing and preparing the operational readiness of new services. 
- Implemented as a checklist or a template, a DPR gives teams guidance on what to think about and consider before they bring a new service into production. 
- While DPRs do not define specific service-level objectives (SLOs) to fulfill (those would be hard to define one-size-fits-all), they remind teams what categories of SLOs to think of, what organizational standards to comply with and what documentation is required. 
- DPRs provide a source of input that teams turn into respective product-specific requirements around, for example, observability and reliability, to feed into their product backlogs.
- DPRs are **closely related to Google's concept of a production readiness review (PRR).** 
- In organizations that are too small to have a dedicated site reliability engineering team, or who are concerned that a review board process could negatively impact a team's flow to go live, having a DPR can at least provide some guidance and document the agreed-upon criteria for the organization. 
- For highly critical new services, extra scrutiny on fulfilling the DPR can be added via a PRR when needed.

### The SRE Engagement Model
- SRE seeks production responsibility for important services for which it can make concrete contributions to reliability. SRE is concerned with several aspects of a service, which are collectively referred to as production. These aspects include the following:
  - System architecture and interservice dependencies
  - Instrumentation, metrics, and monitoring
  - Emergency response
  - Capacity planning
  - Change management
  - Performance: availability, latency, and efficiency
  - When SREs engage with a service, we aim to improve it along all of these axes, which makes managing production for the service easier.

### The Launch Coordination Engineering (LCE) team
- The Launch Coordination Engineering (LCE) team (see [Reliable Product Launches at Scale](https://sre.google/sre-book/reliable-product-launches/)) spends a majority of its time consulting with development teams. SRE teams that aren't specifically dedicated to launch consultations also engage in consultation with development teams.

- When a new service or a new feature has been implemented, developers usually consult with SRE for advice about preparing for the Launch phase. Launch consultation usually involves one or two SREs spending a few hours studying the design and implementation at a high level. 
- The SRE consultants then meet with the development team to provide advice on risky areas that need attention and to discuss well-known patterns or solutions that can be incorporated to improve the service in production. Some of this advice may come from the Production Guide mentioned earlier.

- Consultation sessions are necessarily broad in scope because it's not possible to gain a deep understanding of a given system in the limited time available. For some development teams, consultation is not sufficient:
  - Services that have grown by orders of magnitude since they launched, which now require more time to understand than is feasible through documentation and consultation.
  - Services upon which many other services have subsequently come to rely upon, which now host significantly more traffic from many different clients.
  - These types of services may have grown to the point at which they begin to encounter significant difficulties in production while simultaneously becoming important to users. In such cases, long-term SRE engagement becomes necessary to ensure that they are properly maintained in production as they grow.


## Production Readiness Reviews: Simple PRR Model
- When a development team requests that SRE take over production management of a service, SRE gauges both the importance of the service and the availability of SRE teams. If the service merits SRE support, and the SRE team and development organization agree on staffing levels to facilitate this support, SRE initiates a Production Readiness Review with the development team.

- The objectives of the Production Readiness Review are as follows:

  - Verify that a service meets accepted standards of production setup and operational readiness, and that service owners are prepared to work with SRE and take advantage of SRE expertise.
  - Improve the reliability of the service in production, and minimize the number and severity of incidents that might be expected. A PRR targets all aspects of production that SRE cares about.
  - After sufficient improvements are made and the service is deemed ready for SRE support, an SRE team assumes its production responsibilities.

- This brings us to the Production Readiness Review process itself. There are three different but related engagement models (Simple PRR Model, Early Engagement Model, and Frameworks and SRE Platform), which will be discussed in turn.

- We will first describe the Simple PRR Model, which is usually targeted at a service that is already launched and will be taken over by an SRE team. A PRR follows several phases, much like a development lifecycle, although it may proceed independently in parallel with the development lifecycle.

