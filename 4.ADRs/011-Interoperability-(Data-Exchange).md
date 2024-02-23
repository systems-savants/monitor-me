[> Home](../README.md)    [> ADRs](README.md)

---

# Interoperability (Data Exchange)

Date: 2024-02-22

## Status

Accepted

## Context
For Monitoring Vital Signs, the most crucial is part is to record the patient's data in the contextual form. Context awareness enables models and creates data integration, aggregation, sharing, and analysis opportunities with average response time less than 1 second . So making data self-contained information in different viewpoints addresses the concerns of managing data. Also making data distributed allows cross-domain data validation or enrichment.Managing data in distributed form separate concerns and make more cost-effective choices and reduce complexity 



## Decision
Context awareness enables models for MyMedicalData/MonitorThem creates data integration, aggregation and sharing. For the current requriement of cross-domain data exchange with MyMedicalData, using the API Gateway will sufice given the integration is via secure HTTP.

## Consequences
need to think what might make for good shared key for more common queries 

**Positive:**
-  Maintainability (only have to deal with one system - API Gateway vs. dealing with Integration Inteface like Mulesoft, etc.)



---

[> Home](../README.md)    [> ADRs](README.md)
