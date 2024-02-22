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

We will use Architecture Decision Records, [as described by Michael Nygard](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions).

## Consequences

**Positive:**

- Easy to access decisions.
- Easy to find out why a decision was made.
- Quick to learn how to create and use ADRs.

**Negative:**

- Need to on-board everyone on the project to understand ADRs.

**Risks:**

- Someone not familiar with ADRs may not know where to find them or that they exist.

**Bonus Features:**

- This format will be something we use in other projects to improve architecture decisions governance!

---

[> Home](../README.md)    [> ADRs](README.md)
