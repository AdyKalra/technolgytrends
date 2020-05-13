* **Kubernetes** is a vendor-agnostic cluster and container management tool, open-sourced by Google in 2014. It provides a “platform for automating deployment, scaling, and operations of application containers across clusters of hosts”.
* Kubernetes (commonly stylized as k8s) is an open-source **container-orchestration system** for **automating application deployment, scaling, and management**. ... It aims to provide a "platform for automating deployment, scaling, and operations of application containers across clusters of hosts".
* What's great about Kubernetes is that it's built to be used anywhere so you can deploy to public/private/hybrid clouds, enabling you to reach users where they're at, with greater availability and security. You can see how Kubernetes can help you avoid potential hazards with “vendor lock-in”

* [k8s Learning Path](https://developer.ibm.com/technologies/containers/series/kubernetes-learning-path/)

* [Managed Kubernetes EKS](https://aws.amazon.com/eks/)
  * Amazon Elastic Kubernetes Service (Amazon EKS) is a fully managed Kubernetes service.
  * **AWS Fargate is a serverless compute engine for containers that works with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS).** 
  * EKS is the best place to run Kubernetes for several reasons. First, you can choose to **run your EKS clusters using AWS Fargate, which is serverless compute for containers.** Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design. 
  * Second, **EKS is deeply integrated with services such as Amazon CloudWatch, Auto Scaling Groups, AWS Identity and Access Management (IAM), and Amazon Virtual Private Cloud (VPC)**, providing you a seamless experience to monitor, scale, and load-balance your applications. Third, **EKS integrates with AWS App Mesh and provides a Kubernetes native experience to consume service mesh features and bring rich observability, traffic controls and security features to applications.** Additionally, EKS provides a scalable and highly-available control plane that runs across multiple availability zones to eliminate a single point of failure.
* While Netflix claims most organizations look to write greenfield applications on new container platforms such as Kubernetes, its team wanted to consider existing applications as well. ... Also, operations teams can deploy legacy apps into Docker containers and deploy the containers to Kubernetes clusters.

![k8s](https://miro.medium.com/max/1400/1*tRebIPaAjL8ZtTvu4CC_3w.png)
