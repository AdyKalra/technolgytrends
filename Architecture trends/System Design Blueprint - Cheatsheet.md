[Source](https://medium.com/bytebytego-system-design-alliance/system-design-blueprint-the-ultimate-guide-e27b914bf8f1)

## System Design Blueprint / Cheatsheet
- visual guide that provides developers with a quick and easy reference to key concepts and best practices in system design.
- This handy cheatsheet or blueprint covers essential topics such as DNS, load balancing, API Gateway, video and image handling, caching, databases, unique ID generation, standard components like payment and recommendation services, and chat and streaming protocols.

![SDB (1)](https://github.com/user-attachments/assets/b537d5a1-2006-4e28-ad1b-46e6c6b68349)

### Section 1: Principles of System Design
1.1: Modularization
Dividing the system into smaller, manageable modules helps reduce complexity, improve maintainability, and increase reusability.

1.2: Abstraction
Hiding the implementation details and showing only the essential features helps simplify complex systems and promote modularity.

1.3: Layering
Organizing the system into layers, each layer providing a specific set of functionalities promotes the separation of concerns and enhances maintainability.

1.4: Scalability
Design systems to handle the increased load by adding more resources (horizontal scaling) or optimizing the system's capacity (vertical scaling).

1.5: Performance
Optimizing the system's response time, throughput, and resource utilization is crucial for a successful design.

1.6: Security
Ensure the system's confidentiality, integrity, and availability by implementing proper security measures and practices.

1.7: Fault Tolerance and Resilience
Design systems to withstand failures and recover gracefully from errors, ensuring reliability and availability.

### Section 2: Key Components of System Design
2.1: DNS (Domain Name System)
DNS is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network. It translates human-readable domain names (e.g., www.example.com) into IP addresses, allowing users to access websites and services more efficiently. 
![image](https://github.com/user-attachments/assets/0def2aa1-ef7e-4baf-bb26-02b4f2bc546f)

2.2: Load Balancing
Load balancing refers to distributing network traffic across multiple servers to ensure no single server is overwhelmed. This approach improves the system's availability, reliability, and performance. Standard load balancing algorithms include Round Robin, Least Connections, and IP Hash. [Read More with Cheatsheet](https://medium.com/bytebytego-system-design-alliance/everything-about-load-balancer-with-cheat-sheet-64b351f0f7b3)

2.3: API Gateway
An API Gateway is a server that acts as an intermediary between clients and microservices in a distributed system. It manages and routes requests, enforces security policies, and may provide additional features such as caching, logging, and monitoring

2.4: Content Delivery Network (CDN)
A CDN is a network of servers distributed across various locations, designed to serve content to users with lower latency and higher bandwidth. CDNs cache content on edge servers close to end-users, improving the system's performance and reducing the load on origin servers. [Read More with Cheatsheet](https://medium.com/bytebytego-system-design-alliance/a-beginners-guide-to-cdn-what-it-is-and-how-it-works-f06946288fbb)

2.5: Message Queue
Message queues facilitate communication between distributed system components by temporarily storing messages in a queue. They enable asynchronous processing and help decouple components, improving the system's scalability and fault tolerance. [Read more](https://medium.com/bytebytego-system-design-alliance/everything-about-distributed-message-queue-ae6597d84b36)

2.6: Communication Protocols
Different communication protocols are used in system design, such as HTTP/HTTPS, WebSocket, and gRPC. These protocols have advantages and trade-offs, and the choice depends on factors like latency, security, and data transmission requirements.

2.7: Cache
Caching is a temporary technique used to store copies of data, allowing for faster retrieval in future requests. It helps reduce latency, server load, and bandwidth consumption. Popular caching mechanisms include in-memory caching, distributed caching, and browser caching. [Read more with Cheatsheet.](https://medium.com/bytebytego-system-design-alliance/a-comprehensive-guide-to-distributed-caching-827f1fa5a184)

2.8: Database
Choosing the appropriate database for a system depends on data structure, scalability, consistency, and latency. Common database types include relational databases (e.g., MySQL, PostgreSQL), NoSQL databases (e.g., MongoDB, Cassandra), and NewSQL databases (e.g., Cockroach DB, Google Spanner).

2.9: Replication Techniques
Replication is maintaining multiple copies of data across different nodes for increased reliability, availability, and fault tolerance. Standard replication techniques include synchronous replication, asynchronous replication, and semi-synchronous replication.

2.10: Distributed Unique ID Generation
Creating unique identifiers in a distributed system can be challenging but is essential for maintaining data consistency and integrity. Read more with Comparison Table

### Section 3: Uploading Videos and Images in Chunks Using Signed URLs
In this section, we'll explore how to upload large video and image files in chunks using signed URLs. This method can significantly improve the efficiency and reliability of file uploads, especially in scenarios where network conditions are less than ideal.
