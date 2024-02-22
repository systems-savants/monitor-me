[> Home](../README.md)    [> ADRs](README.md)

---

# Deployment Strategy

Date: 2024-02-15

## Status

Accepted

## Context
Once the solution is implemented it has to be to deploy and manage service at scale.The first and most obvious one is  scale to provide the capacity for business necessity.we could chose private cloud deployment model in which computing resources available on-premises in the hospital data center.we could take into consideration as deployment platforms such: on-premise servers,container orchestrations such as Kubernetes (on-premise or as PaaS), or OpenShift -enterprise flavor of on-premise Kubernetes. Finally, we  decide to go to use Kubernetes cluster on own data center for MonitorMe

## Decision
We decided to go with on-premises in the Hospital’s data centers for two reason. First,There is businenss requiremnt to run workload locally, 
second it increase application portability and for microservices: Containerized applications are an excellent fit for the microservice architecture because we can deploy and scale containers individually. 
When we will reach the limits of up-scaling than the natural thing to follow is, to scale out (scale horizontally) increasing the number of running instances. 

## Consequences
Kubernetes allows you to deploy, scale, and manage containerized applications in a regulated and automated manner.Simply put, Kubernetes is a container orchestrator. The OpenShift Container Platform is a highly scalable Kubernetes platform by Red Hat that allows you to develop and run containerized applications.There is a downside to running Kubernetes on-premises.Do-It-Yourself (DIY), or self-managed, Kubernetes is known for its steep learning curve and operational complexity

**Positive:**
 Manage highly available,Load balancing


**Negative:**
expensive at scale,operational complexity




---

[> Home](../README.md)    [> ADRs](README.md)
