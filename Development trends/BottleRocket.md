### BottleRocket
* Everyone knows how good are containers like Docker, but AWS has now created a **stripped-down version of Linux called Bottlerocket that has just enough code to keep the machine running.** Teams running microservices can choose it and quit worrying about extra cruft like FTP servers sitting around in the background.
* Updates to Bottlerocket are applied in a single step rather than package-by-package. This single-step update process helps reduce management overhead by making OS updates easy to automate using container orchestration services such as Amazon EKS. 
  * The single-step updates also improve uptime for container applications by minimizing update failures and enabling easy update rollbacks. 
* Additionally, Bottlerocket includes only the essential software to run containers, which improves resource usage and reduces the attack surface.

![BottleRocket](https://d1.awsstatic.com/diagrams/Product-Page-Diagram_Bottlerocket_How-it-Works@2x.d950a3b457975c07ed3883f389c1be19f0f98a40.png)
