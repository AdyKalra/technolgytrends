## Arm compute instances 
- [arm in the cloud](https://www.arm.com/markets/computing-infrastructure/cloud-computing) have become increasingly popular in recent years due to their cost and energy efficiency compared to traditional x86-based instances.
- Many cloud providers now offer Arm-based instances, including [AWS](https://www.arm.com/markets/computing-infrastructure/works-on-arm?#AWS), [Azure](https://azure.microsoft.com/en-us/blog/azure-virtual-machines-with-ampere-altra-arm-based-processors-generally-available/) and [GCP](https://cloud.google.com/blog/products/compute/tau-t2a-is-first-compute-engine-vm-on-an-arm-chip).
- The cost benefits of running Arm in the cloud can be particularly beneficial for businesses that run large workloads or need to scale.
- We’re seeing many teams of ours moving to Arm instances for workloads like JVM services and even databases (including RDS) without any change in the code and minimal changes in the build scripts.
- New cloud-based applications and systems increasingly default to Arm in the cloud. Based on our experiences
- Arm compute instances are recommended for all workloads unless there are architecture-specific dependencies. The tooling to support multiple architectures, such as multi-arch Docker images, also simplifies build and deploy workflows.
