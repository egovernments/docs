# The concept of Tenant in DIGIT

#### What is a tenant?

In the context of software architecture, a "tenant" typically refers to an individual or organization that uses a shared software application or service. Each tenant operates within its isolated portion of the application's resources, such as data, configuration, and user interface.

#### What is a multitenant system?

Multitenancy refers to a software architecture where a single instance of the software serves multiple tenants or clients. Each tenant typically has its own isolated and customizable environment, but they all share the same underlying infrastructure and codebase.

In a multitenant system, tenants are often distinguished by factors such as data, configuration, user interface, and access rights. This architecture is commonly used in cloud-based applications, where it allows software providers to efficiently serve multiple customers while minimizing infrastructure costs and maintenance efforts.

For example, in a multitenant web application, each tenant might have its own database or database schema or data partition, ensuring data isolation and security. However, all tenants share the same application codebase and runtime environment, reducing overhead and simplifying updates and maintenance.

#### Goals and Objectives

* Implement multi-tenancy to support multiple tenants within a single instance of the platform and product.
* Enable creation, updating, and searching of tenants/accounts&#x20;
* Ensure data isolation and security by enforcing tenant-level authorization.
* Provide configuration options for administrators to customize system behaviour.

#### Key Stakeholders

* Development Team
* Project Stakeholders
* End Users
