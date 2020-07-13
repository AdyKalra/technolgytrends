# Setting SLOs

## Overview 

* Are you responsible for a customer-facing service? If you are, you know that when that service is unavailable, it can impact your revenue. A lengthy outage could drive your customers to competitors. How do you know if your customers are generally happy with your service?
* If you follow site reliability engineering (SRE) principles, you can **measure customer experience with service-level objectives (SLOs). SLOs allow you to quantifiably measure customer happiness, which directly impacts the business.**
  * Instead of creating a potentially unbounded number of monitoring metrics, we suggest using a small number of alerts grounded in customer pain—i.e., violation of SLOs. This lets you focus alerts on scenarios where you can confidently assert that customers are experiencing, or will soon experience, significant pain.
* Here we’ll walk through a hands-on approach for coming up with SLOs for a service and creating real dashboards and alerts.


