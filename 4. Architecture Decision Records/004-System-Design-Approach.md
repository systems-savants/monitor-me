[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](003-Hosting-Platform-On-Prem.md)  |  [Next >](005-Telemetry-Observability-with-Elastic.md)

---

# 004 - System Design Approach

Date: 2024-02-22

## Status

Accepted

## Context
Here we are trying to find out the architectural charcteristics of the system which will drive our design decision.<br>
Key Characteristics
<br>-High Availibility  -  system needs to be available all the times as the medical professional need to monitor patients vitals and take decision based on them.
<br>-Interoperability - should be able to interact (impot/export) with StayHealthyInc's other software products.
<br>-Performance - Since the devices emit data continuosly and our requirement states the average response time of 1 second.
<br>-Deployability -  We are proposing a micro service architecture with a service for each device ,being able to deploy the whole system seemlessly is important. 
<br>-Data Intergrity -  Raw data coming from the devices and the data thats displayed on the Nurse's screen should always be accurate.Process of consolidation should not affect data integrity in any way.

Implicit Characteristics
<br>-Security
<br>-Usability
<br>-Maintainability
<br>-Observability


## Decision

Based on the requirements and our analyses we decided to go with a combination of Microservices and an event driven architecture.

Both microservices and event driven architecture are good choices for scalability and fault tolerance (High Availibility) .

## Consequences

**Positive:**

- Scalability -  As the problem statement suggests that StayHealthy Inc might add aditional devices to this monitoring system in the future, scalability is important.
- Resiliency -  Requirement mention that the system should stay operational in the event of any device failures.

**Suggestion:**
- Since we are proposing multiple microservices each one catering to a seperate device ,automated deployments is a must.


---

[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](003-Hosting-Platform-On-Prem.md)  |  [Next >](005-Telemetry-Observability-with-Elastic.md)
