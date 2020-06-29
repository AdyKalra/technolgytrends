## High Level Design
*  Client -> CDN | DNS -> LB -> Http Cache -> APIG -> XL -> Feature Services -> Core Services -> Domains

|  Generic 	| Client | CDN | DNS | LB | Http Cache | APIG | XL | Feature Services | Core Services | Domains |
|:-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |
| AWS | Mobile/Web/Affiliates | Cloudfront | Route53 | ELB | Varnish | APIG | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Features | Mobile/Web/Affiliates | pull CDN / globally distributed cache / ssl termination / Faster Performance | High-availability, DNS health, Domain Registration | ELB | Varnish | APIG | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Popular alternates | Mobile/Web/Affiliates | CloudFlare, MaxCDN, Akamai, Incapsula | Google Cloud DNS, DNS Made Easy, Dyn, and DNSimple  | ELB | Varnish | APIG | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
| Not so popular alternates | Mobile/Web/Affiliates | Fastly, MaxKeyCDN, Azure CDN, CDNify | BIND9, PowerDNS, NS1 | ELB | Varnish | APIG | XL | Application tier Lambda / SNS / SQS / Kinesis | Data Tier- RDS / Aurora / DynamoDB | Redshift + EMR |
