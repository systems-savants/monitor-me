[> Home](../README.md)    [> ADRs](README.md)

---

# Deployment Strategy

Date: 2024-02-15

## Status

Accepted

## Context
Once the solution is implemented it has to be to deploy and manage service at scale.The first and most obvious one is  scale to provide the capacity for business necessity.we could chose private cloud deployment model in which computing resources available on-premises in the hospital data center.we could take into consideration as deployment platforms such: on-premise servers, serverless solutions, container orchestrations such as Kubernetes (on-premise or as PaaS), or OpenShift -enterprise flavor of on-premise Kubernetes. Finally, we  decide to go to use Kubernetes cluster on own data center for MonitorMe

The architectural decisions made on this project must be recorded in a useful and comprehensible manner.

## Decision
We decided to go with  on-premises in the client’s data centers for two reason. First, we busienss policy reason to run workload locally, second  it increase application portability and better for microservices: Containerized applications are an excellent fit for the microservice architecture because we can deploy and scale containers individually. 
When we will reach the limits of up-scaling than the natural thing to follow is, to scale out (scale horizontally) increasing the number of running instances. Second, Horizontal scaling adheres to our architecture where we can scale individual components of our system according to the component's load. 

We will use Architecture Decision Records, [as described by Michael Nygard](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions).

## Consequences
Kubernetes allows you to deploy, scale, and manage containerized applications in a regulated and automated manner.Simply put, Kubernetes is a container orchestrator. The OpenShift Container Platform is a highly scalable Kubernetes platform by Red Hat that allows you to develop and run containerized applications.There is a downside to running Kubernetes on-premises.Do-It-Yourself (DIY), or self-managed, Kubernetes is known for its steep learning curve and operational complexity

**Positive:**
 Manage highly available,Load balancing


- Easy to access decisions.
- Easy to find out why a decision was made.
- Quick to learn how to create and use ADRs.

**Negative:**
expensive at scale., operational complexity

- Need to on-board everyone on the project to understand ADRs.

**Risks:**

- Someone not familiar with ADRs may not know where to find them or that they exist.

**Bonus Features:**

- This format will be something we use in other projects to improve architecture decisions governance!

---

[> Home](../README.md)    [> ADRs](README.md)
