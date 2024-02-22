[> Home](../README.md)    [> ADRs](README.md)

---

# Use K8s with containerize microservice architecture style

Date: 2024-02-15

## Status

Accepted

## Context
StayHealthy, Inc. is now expanding into the medical monitoring market with a new medical patient monitoring system for hospitals that monitors a patient's vital signs using proprietary medical devices. The overarching architecture style for the patient monitoring system should be simple, easy to establish, and resilient. A considerable portion of computing and network resources are involved in processing, storing, and retrieving data. it also brings problems like fault, latency, and performance issues. As it deals with patient safety, an IT administration is required to ensure effective and efficient responses in the event of system failure. also, architecture should be adaptable to expand and scale enough to further process the large volume of data.

Microservices architecture goes well with small easily deployable units, which could be individually scaled to handle the load efficiently as process of scaling is quite simple. each microservice's requirement has a limited scope and could be containerized. All the microservices are not required to deploy together, and changes could be implemented separately and as frequently. This feasibility of developing both separately is something that helps in the future as well for monitoring the performance of all the microservices. then it is going to be pretty easy for you to make the right decision when required.

The architectural decisions made on this project must be recorded in a useful and comprehensible manner.

## Decision
We will use the microservice architecture style for backend services in the MonitorMe system. Microservices will be containerized using Docker.These days, backend services for software systems similar to the MonitorMe system commonly use a microservice architecture. In itself, this is not a reason for adopting the microservice style. However, positive consequences of the wide use of microservices contribute to this decision:

We will use Architecture Decision Records, [as described by Michael Nygard](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions).

## Consequences
A nice benefit of the microservice style is flexibility, which enables evolution. This benefit is two-fold:
At deploy- and run-time: flexibility to employ service-specific security, data replication, persistence, and monitoring configurations; flexibility to use different scalability mechanisms for each service.
At development-time: flexibility to use different technologies, patterns, frameworks, libraries, data sources, and other resources in each service.

**Positive:**
large number of tools and frameworks for microservice development, as well as for monitoring, logging and distributed tracing.
increasing number of devloper familiar with the style and respective dev tools and frameworks.
support for containerized microservices widely available in public forums.
Nevertheless, there are important tradeoffs involved in using the microservice style.

- Easy to access decisions.
- Easy to find out why a decision was made.
- Quick to learn how to create and use ADRs.
- 

Rejected alternatives and rationale:
Serverless: it would be perfectly feasible to create MonitorMe services using FaaS (AWS Lambda for example) which could stream vital sign.However, requirement is  MonitorMe will be deployed as an on-premises system and Each physical hospital location will have its own installation of the complete MonitorMe system.On top of that it just required sallow cloud intregration .

**Negative:**
The challenge with increased flexibility is the need to establish some design guidelines and design standards for microservice development. Since it's new medical patient monitoring system it should to define and enforce (via governance mechanisms) a basic reference architecture (with room for evolution). 

suggesting can be as simple as:
Have a clear representation of the reference architecture (we have a good start in our hex architecture, and deployment architecture).
Make sure all devs know about and understand the reference architecture.
Create a space (e.g., a Slack channel) for occasionally discussing changes and evolution of the reference architecture. 
MonitorMe a team of developers familiar with microservice development, microservice patterns, as well as with tools and frameworks, such as:
Spring Boot
Docker
Kubernetes
Spring Cloud AWS
The team will also need some basic knowledge around tools for log consolidation, monitoring, and distributed tracing for microservice

- Need to on-board everyone on the project to understand ADRs.

**Risks:**


- Someone not familiar with ADRs may not know where to find them or that they exist.

**Bonus Features:**

- This format will be something we use in other projects to improve architecture decisions governance!

---

[> Home](../README.md)    [> ADRs](README.md)
