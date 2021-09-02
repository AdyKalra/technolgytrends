## Zero Trust Architecture

- Zero Trust has become one of cybersecurity’s latest buzzwords. It’s imperative to understand what Zero Trust is, as well as what Zero Trust isn’t.

- **Zero Trust is a strategic initiative that helps prevent successful data breaches by eliminating the concept of trust from an organization’s network architecture. Rooted in the principle of “never trust, always verify,” Zero Trust is designed to protect modern digital environments by leveraging network segmentation, preventing lateral movement, providing Layer 7 threat prevention, and simplifying granular user-access control.**

- Zero Trust was created by John Kindervag, during his tenure as a vice president and principal analyst for Forrester Research, based on the realization that traditional security models operate on the outdated assumption that everything inside an organization’s network should be trusted. Under this broken trust model, it is assumed that a user’s identity is not compromised and that all users act responsibly and can be trusted. The Zero Trust model recognizes that trust is a vulnerability. Once on the network, users – including threat actors and malicious insiders – are free to move laterally and access or exfiltrate whatever data they are not limited to. Remember, the point of infiltration of an attack is often not the target location.

- According to The Forrester Wave™: Privileged Identity Management, Q4 2018, This trust model continues to be abused credentials.1 Zero Trust is not about making a system trusted, but instead about eliminating trust.

### A Zero Trust Architecture

- In Zero Trust, you identify a “protect surface.” The protect surface is made up of the network’s most critical and valuable data, assets, applications and services – DAAS, for short. Protect surfaces are unique to each organization. Because it contains only what’s most critical to an organization’s operations, the protect surface is orders of magnitude smaller than the attack surface, and it is always knowable.

- With your protect surface identified, you can identify how traffic moves across the organization in relation to protect surface. Understanding who the users are, which applications they are using and how they are connecting is the only way to determine and enforce policy that ensures secure access to your data. Once you understand the interdependencies between the DAAS, infrastructure, services and users, you should put controls in place as close to the protect surface as possible, creating a microperimeter around it. This microperimeter moves with the protect surface, wherever it goes. You can create a microperimeter by deploying a segmentation gateway, more commonly known as a next-generation firewall, to ensure only known, allowed traffic or legitimate applications have access to the protect surface.

- The segmentation gateway provides granular visibility into traffic and enforces additional layers of inspection and access control with granular Layer 7 policy based on the Kipling Method, which defines Zero Trust policy based on who, what, when, where, why and how. The Zero Trust policy determines who can transit the microperimeter at any point in time, preventing access to your protect surface by unauthorized users and preventing the exfiltration of sensitive data. Zero Trust is only possible at Layer 7.

- Once you’ve built your Zero Trust policy around your protect surface, you continue to monitor and maintain in real time, looking for things like what should be included in the protect surface, interdependencies not yet accounted for, and ways to improve policy.

### Zero Trust: As Dynamic as Your Enterprise

- Zero Trust is not dependent on a location. Users, devices and application workloads are now everywhere, so you cannot enforce Zero Trust in one location – it must be proliferated across your entire environment. The right users need to have access to the right applications and data.

- Users are also accessing critical applications and workloads from anywhere: home, coffee shops, offices and small branches. Zero Trust requires consistent visibility, enforcement and control that can be delivered directly on the device or through the cloud. A software-defined perimeter provides secure user access and prevents data loss, regardless of where the users are, which devices are being used, or where your workloads and data are hosted (i.e. data centers, public clouds or SaaS applications).  

- Workloads are highly dynamic and move across multiple data centers and public, private, and hybrid clouds. With Zero Trust, you must have deep visibility into the activity and interdependencies across users, devices, networks, applications and data. Segmentation gateways monitor traffic, stop threats and enforce granular access across north-south and east-west traffic within your on-premises data center and multi-cloud environments.  

### Deploying Zero Trust

Achieving Zero Trust is often perceived as costly and complex. However, Zero Trust is built upon your existing architecture and does not require you to rip and replace existing technology. There are no Zero Trust products. There are products that work well in Zero Trust environments and those that don't. Zero Trust is also quite simple to deploy, implement and maintain using a simple five-step methodology. This guided process helps identify where you are and where to go next:

1. Identify the protect surface
2. Map the transaction flows
3. Build a Zero Trust architecture
4. Create Zero Trust policy
5. Monitor and maintain

#### Creative a Zero Trust environment – consisting of a protect surface that contains a single DAAS element protected by a microperimeter enforced at Layer 7 with Kipling Method policy by a segmentation gateway – is a simple and iterative process you can repeat one protect surface/DAAS element at a time.
