## Metrics Store

* **[Metrics store](https://blog.transform.co/data-talks/what-is-a-metrics-store-why-your-data-team-should-define-business-metrics-in-code/), sometimes referred to as headless business intelligence (BI), is a layer that decouples metrics definitions from their usage in reports and visualizations.** 
* Traditionally, metrics are defined inside the context of BI tools, but this approach leads to duplication and inconsistencies as different teams use them in different contexts. By decoupling the definition in the metrics store, we get clear and consistent reuse across BI reports, visualizations and even embedded analytics. 
* This technique is not new; for example, Airbnb introduced Minerva a year ago. However, we're now seeing considerable traction in the data and analytics ecosystem with more tools supporting metrics stores out of the box.

https://medium.com/airbnb-engineering/airbnb-metric-computation-with-minerva-part-2-9afe6695b486


“A metrics store allows data teams to lock down metrics so they spend more of their time on interesting work and less time on repetitive tasks.”

* A metrics store is a centralized and governed place for organizations to store key metrics. It is a way of centralizing organizational knowledge, creating a repository for stakeholders to access key metrics in a repeatable way, regardless of how they plan to consume them downstream.

* Until recently, metrics stores were built in-house. Companies with large data teams (like Airbnb) built internal metrics stores to standardize metrics definitions across data sets and data tools. This helped streamline experimentation and at a larger scale, it helped get everyone on the same page when it comes to defining important indicators like “revenue,” “new users,” or “customer growth.” Today, data teams can purchase this functionality with Transform, the first centralized metrics store.


### Benefits of a metrics store: consistency, access, and productivity
* Metrics stores are starting to gain traction as part of the modern data stack. That's because having a metrics store can provide some major benefits. With a metrics store, you can:

Have a centralized place to consume data off the data warehouse.
Ensure that the data fueling your metrics is accurate and consistent.
Provide access to accurate data so that people see the same results when they analyze the data, regardless of the tool they’re using.

A metrics store puts metrics where your internal customers already work. It helps people deliver accurate insights, defining and managing metrics in code.
To understand the value of a metrics store, you need to understand the context. Most organizations have indicators to track success and progress towards goals. Some organizations call them key performance indicators (KPIs) or leading indicators, while others call them metrics. The premise is the same—organizations need to understand if their decisions (or actions) are helping them achieve their objectives.

Usually data teams are responsible for building accurate data sets for the business to track these metrics in downstream business intelligence (BI) tools like Tableau, Looker, or Mode. But not every team uses the same tool, and the underlying data used to define a metric like revenue might live in a few different tables in the warehouse. That means that reporting “revenue” can become a battle of questions like...

“Which definition is right?” Why are there multiple definitions?” “Can I even trust this data?” Even simple questions like “How many sales did we make last week?” can lead to confusion.

By building metrics in code (in a metrics store), data teams have a centralized location to build, measure, and identify business metrics. This also makes your data teams more efficient and strategic because they don’t have to build data sets over and over. Instead, they become enablers, helping business leaders define, share, and champion their metrics across the organization.


### How does a metrics store fit into the modern data stack?

Companies design their data infrastructure based upon how they expect to drive decision-making through analytical systems.

Typically, these companies manage vast amounts of data, flowing from various different applications or third-party source systems. Data is captured and stored in a data warehouse or lake, depending on the type of analytical or operational workflows that the data is intended for. Some transformation may occur before the data flows to the warehouse (think ETL), but more often than not companies are opting for an ELT approach, where datasets are loaded into the warehouse, then prepared for analytical application consumption downstream.

Another approach is when denormalization is performed at the application layer itself, sequestering the metric logic within those bespoke tools (see diagram below).

A metrics store like Transform sits conveniently in between an organization’s data warehouse and other downstream tools. Essentially, it acts as a proxy to the warehouse, translating metric requests into SQL queries to the warehouse. In this way, transformation occurs at the 'metric level' —consistently defined in code, accessible to all downstream tools, and centrally governed to maximize insights.


### How does a data and analytics team use a metrics store?

Although metrics consistency is one critical piece of an organization’s success, data teams also use a metrics store for a variety of other important tasks. As Nick Handel explained on the Data Engineering Podcast, teams use a metrics store to:

1. Interface with metric knowledge: Explore and set metrics definitions and see metrics lineage. Get everyone on the same page when it comes to defining important metrics like “active users,” “net churn,” or “monthly recurring revenue.” That also includes the lineage of how each metric is built, including information at the data source level.
2. Meet consumers in the interfaces they already use: Exposing metrics to all the different places where they’re consumed, like CRMs, experimentation tools, BI tools, and data quality tools. That means that a salesperson looking at a “opportunities created” metric in a BI tool would see the same numbers as a marketer.
3. Manage metrics lifecycles: Track changes to metrics over time and alert metrics owners when things change. If the lineage or definition of a metric changes, the owner is immediately notified and can see why and how this change occurred. If a spike or a dip in the data is present, the owner already knows it happened and has answers for stakeholders. No more tracking down anomalies in the data warehouse.

This is an example of how a metrics store like Transform can help you track the lineage of a ratio metric. This specific metric is made up of multiple measures from the same data source.

### Who is a metrics store made for? Use cases for data and business teams

A metrics store has direct benefits for data and analytics teams, but more importantly, it has a direct impact on the organization as a whole. When everyone is speaking the same language of data, you have less tension over what a metric means or which number is accurate. Everyone has a single source of truth.

The primary people who use a metrics store are:

Data producers (Data engineers, analytics engineers, data analysts) - People who build normalized data sets in the warehouse and who build and test hypotheses. These producers are responsible for providing clean data sets for business users.

How they use a metrics store: Data producers, typically roles within the data and analytics team, use a metrics store to centralize definitions for metrics, calculate metrics, and then surface these metrics to data consumers wherever they like to consume data. This alleviates a lot of repeatable work.
Data consumers (Line-of-business owners) - People who like to consume and explore data. They want everyone to use the same definitions for metrics and they want to see metrics sliced by different dimensions.

How they use a metrics store: Data consumers could be in more technical roles, like a product manager, or they could be a business stakeholder like a head of sales. These consumers can use a metrics store to see an overview of how metrics are performing or they can access these calculated metrics in other tools, like a business intelligence tool, for example.
