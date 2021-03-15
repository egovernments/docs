---
description: Technology insights into DIGIT STACK
---

# Stack Overview

The technology binding the DIGIT Stack is highly resilient and versatile in nature. Seamless integrations, easy extensions, secure data and remote accessibility are the key paradigms defining the efficacy of the DIGIT Urban Stack. Read on to find out more about the key technology tools driving the platform performance. 

### KAFKA - For asynchronous execution

 Digit has a write-heavy platform that benefits from **asynchronous** execution. It removes the need to wait for a response thereby decoupling the execution of two or more services. Asynchronous communication is based on AMQP \(**Advanced Message Queuing Protocol**\). The client or service usually doesn't wait for a response. It just sends the message as and when sending a message to a Kafka queue or any other message broker. Digit uses Kafka as a message broker.

### Persister 

Persister is a service running independently that simply reads the designated Kafka topics and put the messages in DB. By design, we write a yml configuration and put the file path in application.properties.

Features supported: 

* Insert/Update Incoming Kafka messages to Database
* Add Modify Kafka msg before putting it into the database

### Indexer

The Indexer is an independent service indexing various tasks of the DIGIT platform. The service reads records posted on specific Kafka topics and picks the corresponding index configuration from the yml file provided by the respective module.

Features supported:

* Multiple indexes of a record posted on a single topic
* Provision for custom index id
* Performs both bulk and non-bulk indexing
* Supports custom json indexing with field mappings, Enrichment of the input object on the queue
* Performs ES down handling
* Application properties \(application.properties of the citizen-indexer application\)
* Key : egov.indexer.yml.repo.path

**Spring Boot**: Though we had multiple choices of frameworks available in the market, we decided to go with spring boot for our microservice development. The clear advantages of spring boots come along with the legacy of spring framework which spring boot is carrying. It is highly _configurable_, _lightweight_, _easy to maintain dependencies_, _annotations_, availability of open-source _jars & library_ and a highly active _open source community_ which really speed up our development. Interesting to know that **Netflix’s** all major services are developed using the spring boot framework.

**NodeJS**: It is the fastest-growing programming language currently and startups & enterprises have adopted it very well. We have some microservices such as Telemetry, Content Share etc. in nodeJs and planning to have more services in nodeJs in future. 

**ReactJs**: I do not think ReactJs needs any introduction here. It is the most obvious choice for the frontend. We realized React’s ability to remain relevant in the market for a long time.

ReactJs was developed by facebook in 2011 and made it open source in 2013. It is literally capturing the entire frontend market. Whether it is startup or giant tech enterprises, everyone is using ReactJs.

**API Gateway \(Zuul\)**: Zuul is an open-source API Gateway by Netflix which is a unified interface for a set of microservices so that the clients do not need to know about all the details of microservices internals. **DIGIT** uses **Zuul** as an edge service that proxies requests to multiple back-end services. This allows any browser, mobile app or another user interface to consume underlying services. **Zuul** is an open-source API gateway developed by Netflix and it is one of the most popular and widely used API gateway services.

**Kafka**: Kafka is an open-source  _Distributed, Replicated Messaging Queue_ platform developed by Linkedin. Kafka is everywhere nowadays. It is the backbone of every microservices & distributed computing architecture. Kafka is the backbone of the DIGIT platform. Every stream of data goes through Kafka and later on this data gets stored in persistent storage \(**RDBMS**\) and Elasticsearch.  
  
**ELK Stack or Elastic Stack \(Elasticsearch, Logstash & Kibana\)**: Elastic Stack is the world's most popular open-source stack for search, log management & analytics visualisation. It is the combination of 3 open-source platforms Elasticsearch, Logstash & Kibana, developed by [Elastic.co](http://elastic.co/). It is an end to end solution used for search, analysis, & visualisation. 

* **Elasticsearch** is based on the Lucien search and it is mainly used for storage, indexing and search of data. You can think of it as a NoSQL database but it is not exactly a NoSQL database. The best use of elasticsearch is with persistent storage \(RDBMS or NoSql DB\).
* **Logstash** is a log pipeline that takes data from various sources and executes various transformations. 
* **Kibana** is a visualisation layer on elasticsearch. DIGIT's various visualisation dashboards are on Kibana which are being used government, citizen & our internal team.

**Postgresql:** We use PostgreSQL for persistent storage. Though we can use any RDBMS such as MySql, MariaDB etc. PostgreSQL isn't just relational, it's object-relational. This gives it some advantages over other open-source SQL databases like MySQL, MariaDB and Firebird.

### **Tools & Technology Infra**

* Cloud - **AWS**, **Azure**, **Google Cloud, On-Premises** … - run anywhere
* Containers - **Docker**
  * Allows Polyglot stack, Faster Deployment
* Orchestration - **Kubernetes**
  * Managing cluster
* Monitoring and Alerting - **ElasticSearch/Kibana/Prometheus**
* CI/CD pipeline - **Jenkins, Spinnaker**
* Repositories - **Github**

**Docker & Kubernetes**: Maintaining hundreds of services in production could be a nightmare. If you are a developer you can manage a small set of services running on your development environment for build & test but in the production environment, it should be more robust, reliable, easy to maintain & highly scalable. In the last few years, containers have changed the face of software development & deployment. Each microservice is packed into a docker container with all it’s dependencies and deployed into the docker environment. Kubernetes \(K8S\) which a container orchestration system helps us in automating deployments, and scaling and management of these containerized services.

**Jenkins & spinnaker**: Spinnaker is an open-source cloud-agnostic multi-cloud deployment tool, which automates the deployments with built-in deployment strategies/pipelines with ACL as well as Manual approvals. It integrates with various DevOps echo systems like Git, CI \(Jenkins\),  Docker Repos and bakes the docker/container that can be deployed across clusters and infrastructure with efficiency canary analysis or Red/Black strategies.

