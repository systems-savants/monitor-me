[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](README.md)  |  [Next >](002-Use-API-Gateway-in-self-hosted-mode.md)

---

# 001 - Use K8s with containerize microservice architecture style

Date: 2024-02-22

## Status

Proposed

## Context
Microservices architecture goes well with small easily deployable units, which could be individually scaled to handle the load efficiently as process of scaling is quite simple. Each microservice's requirement has a limited scope and could be containerized. All the microservices are not required to deploy together, and changes could be implemented separately and as frequently. This feasibility of developing both separately is something that helps in the future as well for monitoring the performance of all the microservices. then it is going to be pretty easy for you to make the right decision when required.

The architectural decisions made on this project must be recorded in a useful and comprehensible manner.

## Decision
We will use the microservice architecture style for backend services in the MonitorMe system, with AWS EKS as the tool of choice in a high availability and auto scale setup.

## Consequences
Microservices will be containerized using AWS EKS. Microservices architecture facilitates 
1. Scalability: Each microservice can be scaled independently. Ex: Heart rate service with the most events can be scaled independently.
2. Partition Tolerant: The system requirement of being partition tolerant is satisfied. An outage of one microservice does not impact the overall system.
3. Maintainance and Modularity: Each microservice can be modified, developed, maintained, and upgraded independently.

**Positive:**
Scalability, Resiliency, Maintainability, Flexibility, Security (granular security as needed)

**Negative:**
The challenge with increased flexibility is the need to establish some design guidelines and design standards for microservice development. Since it's new medical patient monitoring system it should to define and enforce (via governance mechanisms) a basic reference architecture (with room for evolution). 


---

[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](README.md)  |  [Next >](002-Use-API-Gateway-in-self-hosted-mode.md)
