[> Home](../README.md)    [> ADRs](README.md)

---

# Interoperability (Data Exchange)

Date: 2024-02-15

## Status

Accepted

## Context
For Monitoring Vital Signs, the most crucial is part is to record the patient's data in the contextual form. Context awareness enables models and creates data integration, aggregation, sharing, and analysis opportunities. So making data self-contained information in different viewpoints addresses the concerns of managing data. Also making data distributed allows cross-domain data validation or enrichment.
Managing data in distributed form separate concerns and make more cost-effectives choices and reduce complexity 

The architectural decisions made on this project must be recorded in a useful and comprehensible manner.

## Decision
Nurse station, Analyzer, integration   must treat data as self-contained product. Each application should define shape, interfaces and maintenance and refresh cycle. Domain data shared with downstream processes through service level agreement

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
