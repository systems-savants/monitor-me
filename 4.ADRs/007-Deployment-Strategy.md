[> Home](../README.md)    [> ADRs](README.md)

---

# Deployment Strategy

Date: 2024-02-22

## Status

Accepted

## Context
Once the solution is implemented it has to be to deploy and manage service at scale.The first and most obvious one is  scale to provide the capacity for business necessity. We could chose private cloud deployment model in which computing resources available on-premises in the hospital data center. 

## Decision
We decided to go with AWS EKS on-premises installation (via AWS Outpost Servers) in the Hospital’s data centers for two reason. First, There is businenss requiremnt to run workload locally.

Second it increases application portability and for microservices: Containerized applications are an excellent fit for the microservice architecture because we can deploy and scale containers individually. 

The setup of AWS Elastic Kubernetes Service (EKS) is setup with high availability and scalability in mind. 

## Consequences
AWS EKS allows you to deploy, scale, and manage containerized applications in a regulated and automated manner.Simply put, Kubernetes is a container orchestrator. There is a downside to running Kubernetes on-premises.Do-It-Yourself (DIY), or self-managed, Kubernetes is known for its steep learning curve and operational complexity.

**Positive:**
Manage highly available, Load balancing


**Negative:**
Expensive at scale, Operational complexity




---

[> Home](../README.md)    [> ADRs](README.md)
