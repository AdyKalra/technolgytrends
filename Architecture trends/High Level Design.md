## High Level Design
*  Client -> CDN | DNS -> LB -> Http Cache -> APIG -> XL -> Feature Services -> Core Services -> Domains

[Stacks comparison](https://stackshare.io/categories)

|  Generic 	| Client | CDN | DNS | LB | Http Cache | APIG | XL | Feature Services | Core Services | Domains |
|:-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |
| AWS | Mobile/Web/Affiliates | Cloudfront | Route53 | ELB | Varnish | APIG | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Features | Mobile/Web/Affiliates | pull CDN / globally distributed cache / ssl termination / Faster Performance | High-availability, DNS health, Domain Registration, routing policies based on geagraphy, latency | High availability, reverse proxy server, mail proxy server, TLS termination, Operational monitoring. | caching HTTP reverse proxy | routing policies, traffic control, auth, access control, monitoring, API version management. | aggregated features, map user journey, transformation, Scalability   | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Popular alternates | Mobile/Web/Affiliates | CloudFlare, MaxCDN, Akamai, Incapsula | Google Cloud DNS, DNS Made Easy, Dyn, and DNSimple  | NGiNX, HAProxy, Traefik, Envoy, DigitalOcean | Apache Traffic Server, Squid | KONG,  | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Not so popular alternates | Mobile/Web/Affiliates | Fastly, MaxKeyCDN, Azure CDN, CDNify | BIND9, PowerDNS, NS1 | GLBC, Fly, F5, Google Cloud, Seesaw | Section, Nuster | apigee, mulesoft, zuul | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |

