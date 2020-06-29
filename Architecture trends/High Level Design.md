## High Level Design
*  Client -> CDN | DNS -> LB -> Http Cache -> APIG -> XL -> Feature Services -> Core Services -> Domains

|  Generic 	| Client | CDN | DNS | LB | Http Cache | APIG | XL | Feature Services | Core Services | Domains |
|:-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |:-:  | :-:  |:-:  |:-:  |


### AWS
*  Mobile | Web | Affiliates -> Cloudfront | Route53 -> ELB -> Varnish -> APIG -> Application tier Lambda / SNS / SQS / Kinesis -> Data Tier RDS / Aurora / DynamoDB -> Redshift + EMR
