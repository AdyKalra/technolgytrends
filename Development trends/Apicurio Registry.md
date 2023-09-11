## Apicurio Registry

- Within any organization, API producers and consumers need to stay in sync about the schemas that will be used for communication among them.
- Especially as the number of APIs and related producers and consumers grow in the organization, what may start with simply passing around schemas among teams will start to hit scaling challenges.
- Faced with this issue, some of our teams have turned to [Apicurio Registry](https://www.apicur.io/registry/), an open-source, centralized registry for various types of schemas and API artifacts, including OpenAPI specifications and Protobuf and Avro schemas.
  - Apicurio Registry allows users to interact with it through a UI as well as a REST API and a Maven plugin.
  - It also has the option to enforce schema evolution restrictions, such as backward compatibility.
  - Moreover, when it comes to working with Kafka clients, Apicurio Registry is compatible with Confluent Schema Registry.
  - While our teams have found Confluent Schema Registry's documentation more helpful, Apicurio Registry meets their needs for a source of truth for various schemas.
 
### Apicurio Registry Use Cases
- API Registry
The key use case for the Apicurio community, an API registry is a system that enables you to register your API designs, for example, OpenAPI or AsyncAPI files, so that potential API consumers can do the following:
  - Browse or search the list of APIs available in production
  - View details about a single available API
  - Learn how to use an API using auto-generated documentation
  - Generate client SDKs for an API
 
- Schema Registry
In the messaging and event streaming world, data published to topics and queues often must be serialized or validated using a schema, for example, Apache Avro, JSON Schema, or Google Protocol Buffers. Schemas can be packaged in each application, but it is often a better architectural pattern to register schemas in an external system and then reference them from each application instead. A schema registry provides the following benefits:
  - Decoupling schemas from producers and consumers
  - Potential to upgrade producers without upgrading consumers
  - Central location to track all schemas used in production
  - Document the data format required for each topic or queue
  - Centralized control of data format and schema evolution
