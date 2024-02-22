[> Home](../README.md)    [> ADRs](README.md)

---

# System Approach

Date: 2024-02-22

## Status

Accepted

## Context
Here we are trying to find out the architectural charcteristics of the system which will drive our design decision.
Implicit Characteristics
-High Availibility  -  system needs to be available all the times as the medical professional need to monitor patients vitals and take decision based on them.
-Interoperability - should be able to interact (impot/export) with StayHealthyInc's other software products.
-Performance - Since the devices emit data continuosly and our requirement states the average response time of 1 second.
-Deployability -  We are proposing a micro service architecture with a service for each device ,being able to deploy the whole system seemlessly is important. 
-Data Intergrity -  Raw data coming from the devices and the data thats displayed on the Nurse's screen should always be accurate.Process of consolidation should not affect data integrity in any way.

Explicit Characteristics
-Security
-Usability
-Maintainability
-Observability


## Decision

Based on the requirements and our analyses we decided to go with Microservices and an event driven architecture.
Both microservices and event driven architecture are good choices for scalability ,fault tolerance (High Availibility) .

## Consequences

**Positive:**

- Scalability -  As the problem statement suggests that StayHealthy Inc might add aditional devices to this monitoring system in the future ,scalability is important.
- Resilience -  Requirement mention that the system should stay operational in the event of any device failures.

**Risks:**

- Since we are proposing multiple microservices each one catering to a seperate device ,automated deployments is a must.


---

[> Home](../README.md)    [> ADRs](README.md)