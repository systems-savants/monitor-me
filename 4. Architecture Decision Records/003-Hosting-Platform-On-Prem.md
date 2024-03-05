[> Home](../README.md)    [> ADRs](README.md)

---

# Hosting Platform On Prem - AWS Outposts Servers

Date: 2024-02-22

## Status

Accepted

## Context

The requirement is to host the solution locally on-premises in hospitals.

## Decision

The decision is to use AWS Outpost Servers in a high availability mode. AWS Outposts is a family of fully managed solutions delivering AWS infrastructure and services to virtually any on-premises or edge location for a truly consistent hybrid experience. Outposts solutions allow you to extend and run native AWS services on premises, and is available in a variety of form factors, from 1U and 2U Outposts servers to 42U Outposts racks, and multiple rack deployments.

With AWS Outposts, you can run some AWS services locally and connect to a broad range of services available in the local AWS Region. Run applications and workloads on premises using familiar AWS services, tools, and APIs. Outposts supports workloads and devices requiring low latency access to on-premises systems, local data processing, data residency, and application migration with local system interdependencies. 

## Consequences
The requirement is met along with the ability to run cloud-native technologies on-premises. This allows for local data processing which is a core requirement.

**Positive:**

- Access to cloud-native technology
- Faster time to market
- Local data storage and processing
- Low latency data processing

**Negative:**

- Potential cost
- Disaster recovery limnited to hospital infrastructure

**Risks:**

- Capacity management

[> Home](../README.md)    [> ADRs](README.md)
