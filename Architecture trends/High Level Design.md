## High Level Design
*  Client -> CDN | DNS -> LB -> Http Cache -> APIG -> XL -> Feature Services -> Core Services -> Domains
   * Cloud formation - stacks
     * AMI to bake instances, launch config mgmt

[Stacks comparison](https://stackshare.io/categories)

|  Generic 	| Client | CDN | DNS | LB | Http Cache | APIG | XL | Feature Services / Application tier | Core Services | Domains | Analytics | 
|:-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  |
| AWS | Mobile/Web/Affiliates | Cloudfront | Route53 | ELB | Varnish | APIG | XL |  Services - Integration [Step Fns, SNS, SQS, SES, EventBridge] Compute [λ, EC2] Storage[S3, EBS, EFS]| Elastic In Memory Cache [Redis] Data Tier[RDS, Aurora, DynamoDB] Containers[ECS,EKS,Fargate] | DW[Redshift] ETL[EMR, Glue] |CloudWatch, CloudTrail, Quicksight | 
| Features | Mobile/Web/Affiliates | pull CDN / globally distributed cache / ssl termination / Faster Performance | High-availability, DNS health, Domain Registration, routing policies based on geagraphy, latency | High availability, reverse proxy server, mail proxy server, TLS termination, Operational monitoring. | caching HTTP reverse proxy | routing policies, traffic control, auth, access control, monitoring, API version management. | aggregated features, map user journey, transformation, Scalability   | Application tier Lambda / SNS / SQS / Kinesis | Redis[fully managed, automated DR, store session persistently , faster failover]Aurora[persistence storage, integration with λ, Cost] RDS [MySQL, Postgres, SQLServer] DynamoDB[Managed NoSQL, always clustered, automatic shards on latency / throughput] | Redshift[PostgresSQL based]  EMR Glue[Data Catalog]| |
| Popular alternates | Mobile/Web/Affiliates | CloudFlare, MaxCDN, Akamai, Incapsula | Google Cloud DNS, DNS Made Easy, Dyn, and DNSimple  | NGiNX, HAProxy, Traefik, Envoy, DigitalOcean | Apache Traffic Server, Squid | KONG,  | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Not so popular alternates | Mobile/Web/Affiliates | Fastly, MaxKeyCDN, Azure CDN, CDNify | BIND9, PowerDNS, NS1 | GLBC, Fly, F5, Google Cloud, Seesaw | Section, Nuster | apigee, mulesoft, zuul | XL | Application tier Lambda / SNS / SQS / Kinesis | Elastic In Memory Cache[Memcached] | Redshift + EMR |Grafana, NewRelic, SumoLogic, Kibana |


## Big Picture
*  Client ->DNS/CDN->LB->APIG/XL -> Feature services -> Core services ->Domain / Storage / BI
   * Client[Mobile / Web / Affiliates] -> DNS[Route53]
   * Routing policies based on latency / geo
*  Client[Mobile / Web / Affiliates] ->  CDN[Incapusla / Cloudfront] (pull CDN for making it faster after first fetch) -> LB[ELB/NGINX] 
   * Globally distributed Cache, static assets file – image or video
* LB[ELB/NGINX] -> APIG / XL -> Feature Services -> Core Services -> Domain
   *	Scales automatically, throughput , latency , secure via https , SSL termination capabilities
   *	Http Cache for Web Server - Varnish
* APIG
   *	Security, authorization, traffic control , ops, logging and transformation
* XL 
   *	abstraction, hide complexity , business domain driven user journeys
* EC2 servers with ASG  
   *	AMIs to bake these instances and load configurations 
   *	Multiple AZ, M4 enhanced networking , EBS optimised
* Elastic Cache[Redis, Memcached] between application and storage for scaling DB 
   *	Session management closer to the user , 
   *	Why? Redis better than Memcached –sessions persistently and DS like sets / lists
   *	In memory cache  and Further scaling using Read replicas 
* DB scaling is seasonal for games – warm the DBs 
   *	Key value store- cached objects for user sessions , fully rendered blogs , activity streams
* Database scaling 
   * DB reads - Inmemory cache - Replication 
   *	DB writes - Sharding – horizontal / Federation
   *	Consistent hashing for dynamic shards (Memcached)
   *	Read Replicas / Write always to Master
* Storage Relational[Aurora, RDS]
   *	Aurora – Why?Cost , Persistent storage, Integration with Lambda
   *	 Compare to RDS - More read replicas on Aurora/Failover time is faster on Aurora 
* NoSQL[Dyna/moDB]
   *	Managed NoSQL , always clustered, automatically shards on latency / throughput
   *	because it has on-demand scaling. This was important for us, as we were uncertain about what kinds of loads we would need. It’s also cheap, and 25GB comes free under AWS’s Free Tier.
   *	Why?When key-value or simple queries are present./When a very high read/write rate is needed./ When auto-sharding is required./When auto-scaling is required./When low latency is required./When there is no size or throughput limit./When there is no tuning./When high durability is required.
* Customer Analytics [Google Analytics] 
* Data Analytics – Cloudwatch, Cloudtrail logs , NewRelic, 
* BI – Data warehouse[Redshift , EMR] = Tableau 
   *	Pull data from services tier to DW
* Redshift – postgres SQL based
* Lambda 
  *	Why?Lambda, however, has two big benefits: first, it scales up and down instantly with zero effort on our part, meaning we are not ever paying for an idling server.
Second, it’s what the rest of our stack is built on. Less technology means less cognitive overhead. If the number of pages we crawl ramps up, it will make sense to reconsidering EC2 or a similar compute service.
