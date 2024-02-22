[> Home](../README.md)    [> ADRs](README.md)

---

# Interoperability (Data Exchange)

Date: 2024-02-15

## Status

Accepted

## Context
For Monitoring Vital Signs, the most crucial is part is to record the patient's data in the contextual form. Context awareness enables models and creates data integration, aggregation, sharing, and analysis opportunities with average response time less than 1 second . So making data self-contained information in different viewpoints addresses the concerns of managing data. Also making data distributed allows cross-domain data validation or enrichment.Managing data in distributed form separate concerns and make more cost-effective choices and reduce complexity 



## Decision
As MonitorMe required near-real time usage consideration to analyze vital sings constantly, by utilizing resource-oriented read optimization approaching using sharding technique with patient shard-key data could be analyzed more efficiently,Shared services are stateful services and capable to scale horizontally so patients can be evenly distributed on per nurse station.

Context awareness enables models and creates data integration, aggregation and sharing opportunities. So making data self-contained information in different viewpoints addresses the concerns of managing data. Also making data distributed allows cross-domain data validation or enrichment and exchange

## Consequences
need to think what might make for good shared key for more common queries 

**Positive:**
-  scale Horizontally
-  Stateful
-  Refine shared key if not return expected result

**Negative:**

- Not able to create  shared-key on more descriptive value



---

[> Home](../README.md)    [> ADRs](README.md)
