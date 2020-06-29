## High Level Design
*  Client -> CDN | DNS -> LB -> Http Cache -> APIG -> XL -> Feature Services -> Core Services -> Domains

[Stacks comparison](https://stackshare.io/categories)

|  Generic 	| Client | CDN | DNS | LB | Http Cache | APIG | XL | Feature Services / Application tier | Core Services | Domains | Analytics | 
|:-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  |
| AWS | Mobile/Web/Affiliates | Cloudfront | Route53 | ELB | Varnish | APIG | XL |  Services - Integration [Step Fns, SNS, SQS, SES, EventBridge] Compute [λ, EC2] Storage[S3, EBS, EFS]| Elastic In Memory Cache [Redis] Data Tier[RDS, Aurora, DynamoDB] Containers[ECS,EKS,Fargate] | DW[Redshift] ETL[EMR, Glue] |CloudWatch, CloudTrail, Quicksight | 
| Features | Mobile/Web/Affiliates | pull CDN / globally distributed cache / ssl termination / Faster Performance | High-availability, DNS health, Domain Registration, routing policies based on geagraphy, latency | High availability, reverse proxy server, mail proxy server, TLS termination, Operational monitoring. | caching HTTP reverse proxy | routing policies, traffic control, auth, access control, monitoring, API version management. | aggregated features, map user journey, transformation, Scalability   | Application tier Lambda / SNS / SQS / Kinesis | Redis[fully managed, automated DR, store session persistently , faster failover]Aurora[persistence storage, integration with λ, Cost] RDS [MySQL, Postgres, SQLServer] DynamoDB[Managed NoSQL, always clustered, automatic shards on latency / throughput] | Redshift[PostgresSQL based]  EMR Glue[Data Catalog]| |
| Popular alternates | Mobile/Web/Affiliates | CloudFlare, MaxCDN, Akamai, Incapsula | Google Cloud DNS, DNS Made Easy, Dyn, and DNSimple  | NGiNX, HAProxy, Traefik, Envoy, DigitalOcean | Apache Traffic Server, Squid | KONG,  | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Not so popular alternates | Mobile/Web/Affiliates | Fastly, MaxKeyCDN, Azure CDN, CDNify | BIND9, PowerDNS, NS1 | GLBC, Fly, F5, Google Cloud, Seesaw | Section, Nuster | apigee, mulesoft, zuul | XL | Application tier Lambda / SNS / SQS / Kinesis | Elastic In Memory Cache[Memcached] | Redshift + EMR |Grafana, NewRelic, SumoLogic, Kibana |

