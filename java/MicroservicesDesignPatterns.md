# Microservices Design Patterns # 


- An application exists to handle requests, so the first step in defining its architecture is to distill the application’s requirements into the key requests. A system operation is an abstraction of a request that the application must handle. It’s either a command, which updates data, or a query, which retrieves data. The behavior of each command is defined in terms of an abstract domain model, which is also derived from the requirements.
- The second step in the process is to determine the decomposition into services.
- The third step in defining the application's architecture is to determine each service's API. 


### System of Study ###

- Context 

- Problems

- Solutions

- Benefits and Drawbacks

#### Application Architecture Pattern ####

- Monolithic architecture
- Microserivces architecture

#### Decomposition patterns ####
To decompose a system into a set of services
- Decompose by Business capability
- Decompose by subdomain

#### Messaging Style Patterns ####
Interprocess Communication is very important in Microservices Architecture. 
Communication patterns are organized into five categories: 
1. Communication style: What kind of IPC mechanism to use?
2. Discovery: How does the client of a service determine the IP address of the service instance?
3. Reliability: How to ensure that the communication between services is reliable even though the services are unavailable?
4. Transactional Messaging: How to integrate the sending of messages and publishing of events with database transactions that update business data? 
5. External API: How do the clients communicate with external APIs?

- Messaging
- Remote Procedure Invocation

#### Reliable Communications Pattern ####

- Circuit Breaker

#### Service Discovery Patterns ####

- 3rd Party Registration
- Client-side Discovery
- Self-registration
- Server-side discovery

#### Transactional Messaging Patterns ####

- Polling Publisher
- Transcation Log Tailing
- Transactional Outbox

#### Data Consistency Patterns ####
How to ensure that the datastores maintained by each service, maintain consistent databases?
- Saga Pattern

#### Business Logic Design Pattern ####

- Aggregate
- Domain Event
- Domain Model
- Event Sourcing
- Transaction Script

#### Querying Patterns ####

- API Composition
- Command query responsibility segregation (CQRS)

#### External API patterns ####

- API Gateway
- Backends for Frontends

#### Testing Patterns ####

- Consumer-driven Contract Testing
- Consumer-side Contract Test
- Service Component Test

#### Security Patterns ####

- Access Token

#### Cross Cutting Concerns Patterns ####

- Externalized Configuration
- Microservice Chassis

#### Observability Patterns ####

- Application metrics
- Audit Logging
- Distributed Logging
- Exception Tracking
- Health Check API
- Log Aggregation

#### Deployment Patterns ####

- Deploy a service as a container
- Deploy a service as a VM
- Language specific packaging format
- Service Mesh
- Serverless Deployment
- Sidecar

#### Refactoring to Microservices patterns #### 

- Anti-corruption layer
- Strangler application



## Monolithic Architecture ## 

Problems with Monolithic architecture: 
1. Large and complex application.
2. Use of obsolete frameworks.
3. Packaged into a single WAR file. 

> Hexagonal architecture: The core of the applications consists of the business logic. Surrounding the business logic are various adapters that implement the UIs and integrate with external systems.
>   - The business logic consists of modules, each of which is a collection of domain objects. 
>   - There are several adapters which interface with the external systems - Inbound and Outbound adapters.

### Benefits of Monolithic Architecture ###

- Simple to develop 
- Easy to make radical changes to the application
- Straight-forward to test - Selenium
- Straight-forward to deploy - Copy the WAR file to a server that had the Tomcat installed
- Easy to scale - can run on multiple instances behind a load balancer

### Drawbacks of Monolithic Architecture ###

- With each change the code base becomes larger and more complex to understand. The application can easily outgrow its architecture.
- Fixing bugs and correctly implementing new changes become more difficult.
- The large application overloads and slows down the developer's IDE. 
- Lengthy and painful merges during deployment. Deployment is slow. Deadlines are missed. 
- Continuous integration server must run the entire test suite. 
- Difficult to diagnose and fix the cause of test failure. 
- There could be frequent production outages. 
- The application *lacks fault isolation* as all the modules are running within the same process.
- Monolithic architecture forces the use of obsolete technology stack.


## Some Key concepts ##

#### Three-tier architecture #### 
- It organizes applications into three logical and physical computing tiers: 
  - The presentation tier or UI
  - The application tier - application data is processed.
  - The data tier - data associated with the application is stored and managed. 
- Each tier runs on its own infrastructure - Each tier can be developed by its own development team. 

> Layer vs Tier: 
    > Layer refers to the functional division of the software.
    > Tier refers to the functional division of the software that runs on infrastructure separate from the other divisions.  

- The three tiers have different names but perform the same functions: 
  - Web Server: For UI - HTML, CSS and Javascript - What is typically called as the frontend
  - Application Server: houses business logic. - What is typically called as the backend
  - Database Server: Data tier of a web application. 

#### 4+1 View Model of Software Architecture ####
There are 4 views:
1. Logical view: Software elements that are created by developers. These elements are classes and packages. Relations between them are Inheritance, Association, etc.
2. Implementation view: The output of the build system. This view consists of the modules and components. The relations between them include dependency relationships between modules, and composition relationships between components and modules.
    - Modules - represent packaged code. In Java, this is JAR.
    - Components - These are deployable or executable units consisting of one or more modules. In Java, this is WAR file or Executable JAR file.
3. Process view: The components at runtime. Each element is a process. The relations between process represent Interprocess Communication.
4. Deployment: How the processes are mapped to machines? The elements in this view consist of machines and the processes. The relations between machines represent networking.
5. Scenarios: These animate views. Each scenario describes how the various architectural components within a particular view collaborate in order to handle a request.

- Hexagonal Architectural style organizes the logical view. 
- Implementation view: 
  - Monolithic architecture organizes the implementation view as a single component: a single executable or WAR file. 
  - Microservices architecture structures the implementation view as a set of multiple components: executables or WAR files. The components are services, and the connectors are the communication protocols. 


#### Hexagonal Architectural Style ####

This is an alternative to the layered architectural style. 
> Hexagonal Architectural style organizes the logical view in a way that places the business logic at the center. 

It organizes the **logical view**.
- Instead of the presentation layer, the application has one or more inbound adapters that handle requests from outside by invoking the business logic and the inbound port. Example: Spring MVC Controller or a message broker client that subscribes to messages. 
- Instead of data persistence layer, the application has one or more outbound adapters that are invoked by the business logic and invoke external applications through the outbound port. Example: A DAO (Data Access Object) class that implements operations to access a database. They can also publish events. 
- The business logic has one or more ports.
  - A port defines a set of operations and how the business logic interacts with what is outside of it. In Java, a port is a Java Interface. 
  - There are two kinds of ports: inbound and outbound. 
    - Inbound port: external systems invoke business logic. - Example: A service interface. 
    - Outbound port: The business logic communicates with external systems. - Example: A repository interface. 

##### Benefits of Hexagonal Architecture #####
1. It decouples the business logic from the presentation and the data access logic in the adapters. 
2. The business logic can be invoked via multiple adapters. 



#### Quality of Services ####

**Non-functional requirements; quality attributes; ilities**

1. Scalability
2. Reliability
3. Availability
4. Maintainability
5. Flexibility
6. Security
7. Usability
8. Interoperability
9. Performance
10. Testability


#### Patterns and Patterns Languages ####

Pattern
: A pattern is a reusable solution to a problem that occurs in a particular context. 

Software Pattern
: A software pattern solves a software architecture or design problem by defining a set of collaborating software elements. 

Pattern Structure:
1. Forces - What conditions and circumstances made the implementation of the pattern necessary?
2. Resulting context - What happens after the pattern is implemented?
3. Related patterns - similar or other patterns that are adopted to solve the problems

High level microservices patterns can be divided into three layers: 
1. Infrastructure patterns: Infrastructure issues outside of development
   - Deployment
   - Discovery
   - External API
2. Application Infrastructure patterns: For infrastructure issues that also impact developers
   - Cross-cutting concerns
   - Security
   - Transactional messaging
   - Communication style
   - Reliability
   - Observability
3. Application patterns: Solve problems faced by developers
    - Decomposition
    - Database Architecture
    - Querying
    - Maintaining data consistency
    - Testing

#### Services ####
- A service is a standalone, independently deployable software component that implements some useful functionality. 
- A service has an API that provides its clients access to its functionality.
- Each service in a microservice architecture has its own architecture, and potentially, technology stack. 


#### Loose Coupling ####

Loose Coupling in Microservices
: All interactions with a service happens via its API, which encapsulates the implementation details. This enables the implementation of the service to change without impacting its clients. 

- But loose coupling also prohibits the services from communicating via a database. One downside of not sharing databases is that maintaining data consistency and querying across services are more complex. 




## Microservices Architecture ##

### Scale Cube ###

1. X-axis scaling: Common way to scale monolithic applications
    - Increasing the number of identical applications - Cloning similar instances
    - Load balancer is used to route requests across multiple identical instances.
    - Horizontal Duplication.
    - Improves application's capacity and availability.

2. Y-axis scaling: Common way to scale Microservices applications
    - Entire system is decomposed to address the unique scaling needs of different functionalities.
    - Scale by splitting different things.
    - The application is functionally decomposed into services - **functional decomposition**
    - Solves the problems of increasing development and application complexity.
        - A service is a mini application that implements narrowly focussed functionality.
        - Some services are scaled used X-axis scaling while some are scaled using Z-axis scaling.

3. Z-axis scaling: Commonly used to partition distributed databases - **Sharding**
    - Scale by splitting similar things based on a criteria.
    - Request is routed based on an attribute of the request.
    - Improves application's capacity and availability.


### Modularity in Microservices ###

Applications must be decomposed into modules that are developed and understood by different people. 

    - In a monolithic application, modules are defined using a combination of programming language constructs and build artifacts. 

**The microservices architecture uses services as the unit of modularity.**
- Why is modularity preserved in microservices? - A service has an API which is an impermeable boundary that is difficult to violate. The API cannot be bypassed to access an internal class. This preserves the modularity of the application over time. 
- Modularity also allows for the applications to be deployed and scaled independently. 

### Each service has its own database ###

Services are loosely coupled and communicate only via APIs. To achieve loose coupling, each service has its own datastore. 
- At runtime, the services are isolated from each other. 
- The requirement of each service having its own datastore does not mean that each service has its own database server. 

Section 1.4.4 - 02/07/2024

### Microservices Architecture ###

1. FrontEnd Services 
   - includes an API Gateway 
     - API Gateway plays the role of a facade   
     - provides the REST APIs used by the consumers and couriers' mobile applications

2. Backend Logic
   - consists of numerous backend services 
     - Each backend service has a REST API and its own datastore. 

Benefits
: Each service and its API are clearly defined. 
        - Each service can be independently developed, tested, deployed and scaled. 
        - This architecture preserves modularity. A developer cannot bypass an API and access its internal components.

### Microservices vs SOA (Service Oriented Architecture) ###

Both SOA and microservices are architectural styles that structure a system as a set of services. 

Differences: 
1. Both use different technology stacks. 
   - SOA applications typically use heavyweight technologies such as SOAP and Enterprise Service Bus (ESB) - or smart pipes that contain business and message processing logic.
   - Microservices use lightweight and open source technologies. The services communicate via dumb pipes such as message brokers or lightweight protocols like REST.
2. Both treat data differently.
   - SOA applications typically have global data model and shared databases. 
   - In microservices, each service has its own domain model and its own database. 
3. Both SOA and microservices differ in size:
   - SOA is typically used to integrate large, complex monolithic applications.
   - Microservices applications consist of dozens or hundreds of smaller services.

### Benefits of Microservices Architecture ###
1. Continuous delivery and deployment of large, complex applications. 
2. Services are
   - small and easily deployable
   - independently deployable and scalable
3. Teams can be autonomous
4. Easy to experiment and adopt new technologies
5. Provides better fault isolation


### Drawbacks of Microservices Architecture ###
1. Finding the right set of services is difficult
2. Distributed systems are complex 
    - this makes development, testing, and deployment very difficult
    - Services must use interprocess communication mechanisms
    - Maintaining data consistency across services is difficult. 
    - High level of automation is required:
      - Netflix Spinnaker for automated deployment
      - PaaS like Pivotal Cloud Foundry or Red Hat OpenShift
      - Docker Orchestration platform like Docker Swarm or Kubernetes
3. Requires careful coordination between development teams. 
4. Deciding when to adopt microservices architecture is difficult.
5. Services are loosely coupled. Consequently, there are restrictions on how the services collaborate. 

## Patterns for Decomposing an Application into services ##

Two patterns: 
1. Decompose by Business Capability
2. Decompose by Subdomain - DDD subdomains (Domain Driven Design)

Functional decomposition of the application into services. 

Why is decomposition important? 
1. It facilitates division of labor and knowledge. 
2. Defines how the software elements interact. 


## Interprocess Communication in a Microservice Architecture ##

Communication Patterns:
- Remote procedure invocation,
- Circuit breaker, 
- Client-side discovery, 
- Self registration, 
- Server-side discovery, 
- Third party registration, 
- Asynchronous messaging,
- Transactional outbox, 
- Transaction log tailing,
- Polling publisher


IPC mechanism can impact the availability of an application. It even intersects with transaction management. 
Common methods of IPC: 
1. Synchronous messaging over the REST. 
2. Asynchronous messaging with or without a message broker.

Think about the style of interaction between the services. The choice of the interaction style impacts the availability of the application. 

Two dimensions of IPC: 
1. One-to-One or One-to-Many style of interaction.
2. Synchronous or Asynchronous style of communication.

- Synchronous and One-to-One: Request/Response kind of interaction
- Asynchronous and One-to-One: Asynchronous request/response (Asynchronous response is sent back to the client service) or One way Notification (No response is expected by the sending client service) 
- Asynchronous and One-to-Many: Publish/Subscribe(A client publishes a message which is consumed by zero or more interested services) and Publish/Async Responses (The client publishes a request message and waits for a certain amount of time for responses from interested services)

> A service's API is a contract between the service and its clients. A service's API consists of operations, which the clients can invoke, and events, which are published by the service. 
    
    -   An operation has a name, parameters and a return type. 
    -   An event has a type and a set of fields and is published to a message channel.  

02-08-2022: pg. 98.

> Interface Definition Language (IDL) is used to define a service's API. API first design is essential. 

### How to deal with evolving APIs? ###
APIs change due to: 
- Adding of new features
- Changing of existing features
- Removal of old features.

Problems with evolving APIs:
- In microservices architecture, a service's clients are other services and they cannot be forced to be upgraded in lockstep with the changing API. 
- Modern applications are usually never down for maintenance. This means that a rolling upgrade of the service has to be done and this results in the old and the new versions of the service running simultaneously. 

#### Using Semantic Versioning Solution ####

- http://semver.org - Semantic versioning specification - originally intended for versioning of software packages - Can also be used with APIs.
  - MAJOR.MINOR.PATCH : 
    - MAJOR: When incompatible changes are made to the API
    - MINOR: When backward-compatible changes are made to the API.
    - PATCH: When a backward-compatible bug-fix is made.
- The goal is to properly version APIs and evolve them in a controlled fashion.
- Strive to only make backward-compatible changes to an API: 
  - Adding optional attributes to request.
  - Adding attributes to a response.
  - Adding new operations. 
- Older clients can still work with new services if only make backward compatible changes are made and also if they observe the Robustness Principle. 

> Robustness Principle: "Be conservative in what you do, be liberal in what you accept from others".

### Message Formats ###

- It is essential to use a cross-language message format. 
- Do not use Java Serialization. 
- There are two main categories of message formats: Text and Binary

#### Text Based Message format ####

JSON and XML are text based message formats. These are self-describing and human-readable.

Downsides of Text Based message format: 
1. The messages tend to be verbose. They would have overhead of containing the names of the attributes in addition to their values. 
2. The overhead of parsing the text is especially large when the messages are large. 
3. It is better to use the binary format if efficiency and power are important. 


#### Binary Message format ####

Popular formats include Protocol Buffers and Avro. 
- Both the formats provide a typed IDL for defining the structure of the message. 
- Both the formats provide a compiler for Serializing and De-serializing. 
- Protocol Buffers use tagged fields where as Avro consumers need to know the schema in advance before interpretation. 

### Remote Procedure Invocation Pattern ###

Remote Procedure Invocation Pattern
: A client sends a request to a service, and the service processes the request and sends back a response. 
- Some clients may block waiting for a response. 
- Others might have a reactive, non-blocking architecture. 

Whatever be the case, unlike messaging, the client expects the response from the service in a reasonable time. 

How does RPI work? 
1. The business logic in the client invokes an proxy interface, implemented by an RPI proxy adapter class. 
2. The RPI proxy makes a request to the service. 
3. The request is handled by an RPI server adapter class, which invokes the service's business logic via an interface. 
4. The reply is then sent back to the RPI proxy by the RPI server adapter class. 
5. RPI proxy returns the reply as a result to the client's business logic. 

Proxy Interface
: The proxy interface usually encapsulates the underlying communication protocol. There are numerous protocols to choose from - of which REST is one. 

RPI using services must: 
1. Handle partial failures - Circuit Breaker pattern
2. Use Service Discovery mechanisms 

#### RESTful APIs ####
REST is an IPC mechanism that uses HTTP. 

1. The key concept of REST is a resource, which is a single business object or a collection of business objects. 
2. REST uses HTTP verbs for manipulating resources which are referenced using a URL. 

The major problems with REST API: 
1. Fetching multiple resources in a single request.                                      
2. Mapping Operations to HTTP verbs. 

These challenges have led to the emergence of GraphQL, gPRC and other technologies. 


##### The REST maturity model ##### 
1. Level 0 - Clients invoke the service by using a POST request to its sole URL endpoint. 
2. Level 1 - The service supports the idea of resources. To perform an action on the resource, the client specifies a POST request. 
3. Level 2 - Uses HTTP verbs to perform actions - GET to retrieve, POST to create, and PUT to update. The request query parameters and body, if any, specify the action's parameters. 
4. Level 3 - HATEOAS (Hypertext As The Engine Of Application State) principle is followed: The representation of a resource returned by GET must contain links for performing actions on the resource. 

##### Specifying REST APIs #####
Open API Specification - which evolved from the Swagger Open Source Project. The Swagger project is a set of tools for developing and documenting REST APIs. 
It includes tools that generate client stubs and server skeletons from an interface definition. 

##### The challenge of fetching multiple resources in a single request #####

REST resources are usually oriented around business objects. - A common problem when designing REST APIs is how to enable a client to retrieve multiple related objects in a single request. 

- Solution: 
	1. To allow the client to retrieve related resources when it gets a resource. This method is insufficient in complex scenarios. 
	2. GraphQL and Netflix Falcor as alternative API technologies that support efficient data fetching. 

##### The challenge of Mapping Operations to HTTP verbs #####

How to map the operations that one want to perform on a business object to an HTTP verb? 

Solution: 
1. One way is to define a sub-resource for updating a particular aspect of a resource. 
2. Another solution is to specify a HTTP verb as a URL query parameter. 

##### Benefits of REST #####
1. Testing is easy.
2. Directly supports request/response style communication.
3. HTTP is firewall friendly.
4. It does not require intermediate broker.

##### Drawback of REST #####
1. It only supports request/response style of communication.
2. Reduced availability - As both the client and the service communicate directly, they both must be running for the duration of the exchange. 
3. Clients must know the locations (URLs) of the service instances. Clients must use a service discovery mechanism to locate the running instances of the services. 
4. Fetching multiple resources in a single request is challenging. 
5. It is sometimes difficult to map multiple update operations to HTTP verbs - Comes the use of gRPC. 


#### gRPC ####

Problems: It is difficult to map multiple update operations in REST using HTTP verbs. 
Solution: IPC technology that avoids this issue is gRPC - gRPC is a framework for writing cross-language clients and servers. 

gRPC
: It is a binary message-based protocol, this means that the API first approach should be taken to the design approach. 

Remote Procedure Call framework that can run in any environment. Pluggable support for load balancing, tracing, health checking and authentication. 

Use Protocol Buffer compiler to generate client-side stubs and server-side skeletons. The compiler can generate code for a variety of languages. 
Each field of a Protocol Buffers message is numbered and has a type code. 

#### Circuit Breaker Patterns ####

Problems: Whenever a service makes a synchronous request to another service, there is an ever-persistent risk of partial failure. Because the client is blocked waiting for response, the danger is that the failure could cascade to the client's clients and so on and cause an outage. 

Solution: Circuit Breaker Pattern - A RPI proxy that immediately rejects invocations after a timeout period after the number of consecutive failures exceeds a specific thershold. 

There are two parts to the solution: 
1. Design RPI proxies to handle unresponsive remote services. 
2. Decide how to recover from a failed remote service. 

##### Develop robust RPI proxies #####

Developing a robust RPI proxy is a combination of the following mechanisms: 
1. ** Network Timeouts **: Never block indefinitely and always use a timeout when waiting for a response. 
2. ** Limit the number of outstanding requests from a client to a service **: Any further attempts should fail immediately. 
3. ** Circuit Breaker Pattern **: Track the number of successful and failed requests, and if the error rate exceeds a threshold, trip the circuit breaker so that further attempts fail immediately. 

Netflix Hystrix - implements Circuit Breaker Pattern. Use Hystrix when using RPI proxies. 

###### Recovering from an unresponsive service ######
How to recover from an unresponsive remote service? 
1. Return simply an error to the client. 
2. Return a fallback value - could be a default value or a cached response. 

#### Using Service Discovery Mechanism ####

Dynamically assigned IP and dynamically created and destroyed services. 

- Key component of service discovery is Service Registry. - A Service Registry is a database of Network locations of an application's service instances.
- The service discovery mechanism update the service registry whenever service instances start and stop.

There are two main ways to implement service discovery: 
1. The services and the clients directly interact with the service registry. 
2. The deployment infrastructure handles service discovery. 

##### Application-level Service Discovery Patterns #####

1. A service instance registers its network location with the service registry. 
2. A service client invokes a service by first querying the service registry to obtain a list of service instances. 
3. It then sends a request to one of those instances. 

This approach is a combination of two patterns: 
1. Self Registration Pattern
2. Client Side Discovery Pattern

###### Self Registration Pattern ######
A service instance invokes the service registry's registration API to register its service location. 

It may also supply a health check URL. - A health check URL - an API endpoint that the service registry invokes periodically to verify that the service instance is healthy and able to handle requests. 

###### Client Side Discovery Pattern ######
1. When a service client wants to invoke a service, it requests the service registry to obtain a list of the service's instances.
2. To improve performance, a client may cache the service instances. 
3. The service client then uses a load balancing algorithm to select a service instance - round-robin or random. 
4. It then makes a request to a select service instance. 

Application-level service discovery - Netflix Eureka - highly available Service Registry + Eureka Java Client and Netflix Ribbon - a sophisticated HTTP client that supports the Eureka client. 

Netflix Ribbon - Client-side Service Discovery. 

Spring Cloud based services automatically register with Eureka, and Spring Cloud based Clients automatically use Eureka for service discovery. 

** Benefit **: Application-level service discovery is that it handles the scenario in which the services are deployed on multiple deployment platforms. 
** Drawback **: 
1. The need for a service discovery library for every language and possibly framework that is used. Spring Cloud only helps Spring developers. 
2. Developer is responsible for setting up and managing the service registry. 


###### Platform-provided Service Discovery Patterns ######

Docker and Kubernetes have built-in service registry and service discovery mechanism. The deployment platform gives each service a DNS name, a Virtual IP (Virtual IP) address and a DNS name that resolves to the VIP address. 

Service Registration, Service Discovery and Request Routing are all done by the deployment platform. 

This approach is a combination of two patterns: 
1. 3rd Party Registration Pattern: A third party called the **Registrar** handles the registration. It is part of the deployment platform. 
2. Server-Side Discovery Pattern: Instead of the client querying to a service registry, it makes a request to the DNS name, which resolves to a request router that queries the Service Registrar and load balances request.  

Benefits of Platform provided Service Discovery: 
1. All aspects of service discovery are entirely handled by the deployment platform. Neither the client nor the services contain any service discovery code. 
2. The service discovery mechanism is available to all services and clients regardless of which language or framework they are written in. 

Drawbacks: 
It only supports the discovery of services that have been deployed using the platform. 



### Communicating using Asynchronous Messaging Pattern ###

Services communicate by asynchronously exchanging messages. 

A messaging based application typically uses a message broker, which acts as an intermediary between services. Brokerless architecture can also be used. 

Communication is asynchronous - client is not blocked waiting for a reply. 

Important aspects: Scaling consumers, preserving message ordering, detecting and discarding duplicate messages, sending and receiving messages as part of database transactions. 

Components: Message, Message Channels, 

#### Messages ####
A message consists of: 
1. Header - name-value pairs and metadata about the message - may also contain unique messageId. 
2. Message Body - either binary or text format.

Different kinds of messages: 
1. Document - a generic message that contains only data. The receiver decides how to interpret it. 
2. Command - Message that is equivalent to an RPC request. It specifies the operation to invoke and its parameters. 
3. Event - It is often a domain event that represents state change of a domain object - signifies that something notable has occurred in the sender. 

#### Message Channels ####

Messages are exchanged over channels. A message channel is an abstraction of the messaging infrastructure. 

Any number of senders can send messages to a channel and any number of receivers can receive messages from a channel. 

There are two kinds of channels: 
1. Point-to-Point
2. Publish/Subscribe

** Point-to-Point **: Delivers message to exactly one of the consumers that subscribe to the messaging channel. Services use point-to-point for one-to-one communication.

** Publish-Subscribe **: It delivers messages to all of the subscribed consumers. Suited for one-to-many interaction styles. 

#### Implementations of various messaging interactions ####
Various interaction styles: Asynchronous Request/Response, One-way Notifications, Publish-Subscribe and Publish-Async Responses.

Messaging is inherently asynchronous.

1. Asynchronous Request-Response: By exchanging a pair of messages.  The client must tell the service where to send a reply message and must match reply messages to requests. The message sent by the client must contain a reply channel header. The service sends a reply message that contains a correlationId that has the same value as the message identifier, to the reply channel. 

2. One-way Notifications: The client sends a message, typically a command-message to a point-to-point messaging channel owned by the service. The client does not expect any reply. 

3. Publish-Subscribe: A client publishes a message to a publish-subscribe channel that is read by multiple consumers. 
	- Services typically use publish-subscribe to publish domain events, which represent changes to domain objects. 
	- Services that publish domain events, typically own a publish-subscribe channel, whose name is derived from the domain class. 

4. Publish/Async Responses: Combines elements of publish-subscribe and request-response. A client publishes a message containing a reply channel header to a publish-subscribe channel. A consumer writes a reply message containing the correlationId to the reply channel. The client gathers the responses by using the correlation Id, to match the reply messages with the requests. 

#### How to create an API for message-based service ####

Such messaging based asynchronous services must specify: 
- Names of the message channels
- The message types that are exchanged over each channel
- Message formats

There is no standard documenting style for channels and message types. You need to write an informal document. 

A service's asynchronous operations consists of operations, invoked by clients, and events, published by services. 

#### Using a Message Broker ####

A message broker is a infrastructure service through which services communicate. 

	##### Brokerless Architecture #####
	
	Services exchange messages directly. ZeroMQ is a popular brokerless messaging technology. 
	Benefits of Brokerless Architecture: 
	1. Lighter network traffic and message latency as there is no intermediating broker. 
	2. The message broker cannot be a performance bottleneck or a single point of failure. 
	3. Less operational complexity. 
	
	Drawbacks of Brokerless Architecture: 
	1. Should use service discovery mechanisms. 
	2. Offers reduced availability as both the client and the service must be available during the exchange of the message. 
	3. Implementing guaranteed delivery is more challenging. 

Broker-based messaging architecture: 

A message broker is a intermediary through which all messages flow. 

Benefits: 
1. Sender does not need to know the network location of the consumer. 
2. Message broker buffers messages until the consumer is able to process them.

Popular open-source message brokers: Almost all message brokers support both point-to-point and publish-subscribe type of messaging except for SQS.
- ActiveMQ - JMS message broker - has queues and topics
- Apache Kafka - topics
- RabbitMQ - AMQP based - has exchanges and queues
- Cloud based: 
	- AWS Kinesis - streams
	- AWS SQS - queues - supports only point-to-point.

Factors to consider when selecting a messaging broker: 
- Supported programming languages.
- Supporting messaging standards
- Messaging order
- Delivery guarantees
- Persistence
- Durability
- Scalability
- latency
- Competing consumers

Benefits of Broker-based messaging: 
1. Loose Coupling: The client is completely unaware of the service instances. 
2. Message buffering
3. Flexible Communication
4. Explicit interprocess Communication

Downsides to Broker-based messaging: 
1. Potential bottleneck
2. Potential Single point of failure
3. Additional operational complexity

#### Message based communications Problems and solutions ####

1. Competing receivers and Message ordering - How to ensure that each message is processed once and only once while maintaining high throughput with concurrent processing of messages through multi-threading and multiple service instances. 
2. Handling duplicate messages

##### Competing receivers and Message ordering #####

How to scale our consumers while preserving message ordering? 
It is a general practice to use multiple threads and service instances to concurrently process messages to increase the throughput of the application. But the challenge that arises with this is ensuring that each message is processed once and only once. 

Common Solution: Used by Kafka and AWS Kinesis - to use ** Sharded Channels **. There are three parts to the solution: 
1. A sharded channel ( or replica) consists of two or more shards, each of which behaves like a channel. 
2. The message sender provides a shard key (partition key for Kafka) which the message broker uses to allocate the message to a particular shard/partition. 
3. The messaging broker groups together multiple instances of a receiver and treats them as the same logical receiver. Kafka - consumer group.

This ensures that each event for a particular order are sent to the same shard, which is read by a single consumer instance. As a result, messages are guaranteed to be processed in order. 

##### Handling Duplicate Messages #####

Ideally, a message broker should deliver each message only once. But guaranteeing that each message is delivered only once is costly. Most message brokers promise to deliver each message at least once. - A failure of the message broker, client or network can result in the message being delivered multiple times. 

Two ways to handle duplicate messages: 
1. Write idempotent message handlers.
2. Track messages and discard duplicates. 

###### Writing idempotent message handlers ######

Application logic is idempotent if calling it multiple times with the same input values has no additional effect.

An idempotent message handler can be safely executed multiple times, provided that the message broker preserves ordering when redelivering messages. 

Unfortunately application logic is often not idempotent.  


###### Tracking messages and discard duplicates ######

Message handler should become idempotent by detecting and discarding duplicate messages. 

Simple solution: The message consumer should keep track of the messages it has processed using the message id and discard any duplicates. Store the message id of each message that it has consumed in a database table. Use a dedicated table for Processed messages and a separate table for application processing. 

If using a NoSQL database, a dedicated table for storing processed_messages is not required. The message handler can record message Ids in an application table instead of dedicated table. 

##### Transactional Messaging #####
 
A service often needs to publish messages as part of a transaction that updates the database. Both the database update and the sending of the message must happen within a transaction. If the service does not perform these two operations atomically, a failure could leave the system in an inconsistent state. 

Traditional Solution: Use a distributed database that spans the database and the message broker - but distributed transactions are not a good choice for modern applications + many modern brokers such as Apache Kafka do not support distributed transactions. 

Design patterns to solve this problem: Transactional Outbox Pattern.

In Transactional Outbox Pattern, how to move messages from the Database to the message broker. 
1. Polling Publisher Pattern.
2. Transaction Log Tailing Pattern. 

###### Transactional Outbox Pattern - Using Database table as a Message Queue ######

This pattern uses a database table as a temporary message queue. A service that sends messages has an OUTBOX database table. The service sends messages by INSERTing them into the OUTBOX table. The OUTBOX table acts as a temporary message queue. The MessageRelay component reads from the OUTBOX table and publishes the message to a message broker. - This is a simple Polling Publisher Pattern. 

In NoSQL databases, each business entity is stored as a *record* in the database, has an attribute that is a list of messages that need to be published. When a service updates an entity in the database, it appends a message to that list. This is atomic because it is done with a single database operation. The challenge is efficiently finding business events that have events and publishing them. 

###### Polling Publisher Pattern - ######

Polling the database is a simple approach that works reasonably at low scale. The downside is that frequently polling the database can be expensive. 

###### Transaction Log Tailing Pattern ######

A sophisticated solution is for MessageRelay to tail the database transaction log - also called the commit log. 
- Every committed update made by an application is represented as an entry in the database's transaction log. A transaction log miner can read the transaction log and publish each change as a message to the message broker.  
- The TRANSACTION_LOG_MINER reads the transaction logs. It converts each relevant log entry corresponding to an inserted message into a message and publishes that message to the message broker. 
- Few technologies used in Transactional Log Tailing Pattern: 
	- Debezium - open source project that publishes database changes to the Apache Kafka message broker. 
	- LinkedIn Databus - Open Source project that mines the Oracle transaction log and publishes the changes as events. 
	- DynamoDB streams - DynamoDB streams contain time ordered sequence of changes made to the items in a DynamoDB table in the last 24 hours. 
	- Eventuate Tram - uses MySQL binlog protocol, PostGres WAL, or polling to read changes made to an OUTBOX table and publish them to Apache Kafka. 


#### Benefits of Asynchronous Messaging ####

Synchronous Communication reduces availability. REST is a synchronous HTTP protocol. This problem exists even if services communicate over asynchronous request/response style interaction. Eliminating Synchronous communication - There are ways to handle synchronous requests without making synchronous requests. 

1. Use Asynchronous Interaction styles - all interactions are asynchronous. No participant is ever blocked waiting for a response. The message broker buffers messages until they are consumed. 

2. Replicate Data: If a service has a synchronous API, one way to improve availability is to replicate data. This is one of the ways to minimize synchronous requests. A service maintains a replica of the data that it needs when processing requests. It keeps the replica up-to-date by subscribing to events published by the services that own the data. This can be inefficient if it requires replication of large amounts of data.	

3. Another way to eliminate synchronous communication during processing is by following method:
		1. Validate the request using only the data available locally. 
		2. Update its database, including inserting messages into the OUTBOX table. 
		3. Return a response to its client. 
While handling a request, the service does not synchronously interact with any other services. Instead, it asynchronously sends messages to other services. This approach ensures that the services are loosely coupled. 
This is often implemented using a SAGA pattern. 



## Managing Transactions with SAGAs ##

Challenges: Implementing ACID compliant transactions for operations that update data owned by multiple services. 

Traditional approach to distributed transaction management is not suitable for modern applications. 

> An operation that spans services must use SAGA, a message driven sequence of local transactions, to maintain data consistency. 

Challenge with SAGA: The operations are ACD (Atomocity, Consistent and Durability) but not ACID. They lack the isolation feature of ACID. As a result, an application must use countermeasures (design techniques) that prevent or reduce the impact of concurrenty anomalies caused by lack of isolation. 

Multi-database architecture with ACD SAGAs. 

Two different ways of coordinating SAGAs: Choreography and Orchestration. 
- Choreography: Participants exchange messages without a centralized point of control. 
- Orchestration: A centralized controller tells the SAGA participants what operations to perform. 

Spring Framework provides a declarative mechanism to transaction management. The @Transactional annotation arranges for method invocations to be automatically executed within a transaction. 

### Why transaction management is a challenge in microservices architecture? ###

1. The needed data is scattered around in multiple services. Because each service has its own database, you need a mechanism to maintain data consistency across those databases.
2. Problems with distributed transactions: 
	- Java has JTA for distributed transactions. But most NoSQL databases do not support distributed transactions. 
	- Distributed transactions are not supported by modern message brokers such as RabbitMQ or Apache Kafka. 
	- Distributed transactions are a form of synchronous IPC, which reduces availability. 

pg. 144 - 4.1.3 - 02/12/2024

### SAGA pattern for data consistency ###

SAGA
: Sagas are mechanisms to maintain data consistency in a microservice architecture without having to use distributed transactions. A *saga* is defined for each system command that needs to update data in multiple services. A **Saga** is a sequence of local transactions. Each local transaction updates the data within a single service using the ACID transaction frameworks and libraries. The completion of a local transaction triggers the execution of the next local transaction. Coordination of the steps is implemented using asynchronous messaging. 
- Asynchronous messaging ensures that all the steps of the Saga are executed, even if one or more saga participants are temporarily unavailable. 
- Asynchronous messaging also ensures that all saga participants are loosely coupled. 
- Since each local transaction commits its changes, a saga must be rolled back using compensating transactions. 
- If the *(n+1)* transaction of a saga fails then all the previous *n* transactions must be undone. Conceptually each of those transactions has a corresponding compensating transaction that undoes the effects of the transaction. To undo the effects of the first *n* steps, the saga must execute each compensating transaction in the reverse order. 

SAGA steps: 
1. Implement each business transaction that spans multiple services as saga.
2. A saga is a sequence of local transactions. Each local transaction updates the database and publishes a message or event to trigger the next local transaction in the saga. 
3. If a local transaction fails because it violates a business rule, then the saga executes a series of compensating transactions that undo the changes that were made by the preceding local transactions. 

Challenges to implementing Sagas: 
1. Lack of isolation between sagas. 
2. Rolling back changes when an error occurs - Sagas cannot be automatically rolled back because each transaction commits its changes to the local database. This requires the use of compensating transactions. 

> Pivot Transaction: It is that transaction which is followed by steps that never fail. The steps after pivot transaction are called retriable transactions, because they always succeed. 

### Coordinating Sagas ###

A saga's implementation consists of logic that coordinates the steps of the saga. There are couple of ways to strucuture a saga's coordination logic: 
1. Choreography: Distribute the decision making and sequencing among the saga participants. They primarily communicate by exchanging events. 
2. Orchestration: Centralize a saga's coordination logic in a saga orchestrator class. A saga orchestrator sends command messages to participants telling them which operations to perform. 

#### Choreography based Sagas ####
The saga participants subscribe to each other's events and respond accordingly. The participants of choreography-based sagas interact using publish/subscribe. 

Choreography can work well with simple sagas. But it is often better to use orchestration for more complex sagas. 

Issues with Choreography based Sagas: 
1. Ensuring that the service updates its database, and publishes an event, atomically, as part of a database transaction. 
2. Ensurint that a saga participant maps each event that it receives to its own data. 

**Solution to these issues**: A saga participant must publish events containing a correlationId, which is data that enables other participants to perform mapping. 

##### Benefits of Choreography based Sagas #####
1. Simplicity
2. Loose Coupling - participants subscribe to events and have no direct knowledge of each other. 

##### Drawbacks of Choreography based Sagas #####
1. Code is more difficult to understand: the implementation of the saga is distributed among the services. 
2. Cyclic dependencies between the services.
3. Risk of tight coupling: Each saga participant must subscribe to all the events that affect them.  


#### Orchestration based Sagas ####

- An orchestrator class is defined whose sole responsibility is to tell the saga participants what to do. 
- The Saga Orchestrator communicates with the participants using command/async reply style interaction. 
	- To execute a saga step, it sends a command message to a saga participant telling it what operation to perform. 
	- After the saga participant has performed the action, it sends a reply message to the orchestrator.
	- The orchestrator then processes the message and determines which saga step to perform. 

pg. 153 - 02/13/2024

##### Modeling Saga Orchestrators as State Machines #####
A state machine consists of states and a set of transitions between states that are triggered by events. Each transaction can have an action, which is for saga the invocation of a saga participant. The current state the specific outcome of the local transaction determine the state transition and what action, if any, to perform. 

##### Benefits of Orchestration #####
1. Simpler dependencies - no cyclic dependencies.
2. Less coupling. 
3. Improves separation of concerns and simplifies business logic. 

Drawbacks of Orchestration: The risk of centralizing too much business logic in the orchestrator. 
Solution: Design orchestrators that are solely responsible for sequencing and do not contain any other business logic. 

### Handling lack of Isolation in Sagas ###

Isolation
: It ensures that the outcome of executing multiple transactions concurrently is the same as if they were executed in some serial order. 

Isolation problem created by Sagas
: Updates made by each of a saga's local transactions are immediately visible to other sagas once that transaction commits: 
	1. Other sagas can change the data accessed by the saga while it is executing. 
	2. Other sagas can read its data before it has completed its updates, and consequently can be exposed to inconsistent data. 
	
Sagas are to be considered ACD: 
1. Atomocity: All transactions are executed or all changes are undone. 
2. Consistency: Referential integrity within a service is handled by local databases. Referential integrity across services is handled by the services.
3. Durability: Handled by local databases. 

Lack of isolation in the Saga transactions can cause anomalies. An anomaly is when a transaction reads or writes data in a way that it would not if transactions were executed one at time. 
- The default isolation level is usually an isolation level that is weaker than full isolation, also known as Serializable transactions. 
- Strategies that deal with lack of isolation are called countermeasures. 

#### Anomalies in Saga due to lack of isolation ####
1. Lost updates: One saga overwrites without reading changes made by another saga. 
2. Dirty reads: A transaction or saga reads the updates made by a saga that has not yet completed those updates. 
3. Fuzzy/non-repeatable reads: Two different steps of a saga read the same data and get different results because another saga has made updates. 