[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](010-Interoperability.md)  |  [Next >](../5.%20Proposed%20Solution/README.md)

---

# 011 - Postgre SQL for Data Storage

Date: 2024-02-22

## Status

Options: Accepted

## Context

MonitorMe requires an on-premises data storage and processing option that supports high-performance writes and reads, is secure, and maintains data accuracy/integrity.

## Decision

The decision is to use AWS RDS PostgreSQL based on data storage and access patterns for nurse station dashboards.

Data will be partitioned by Nurse Station Identifier and Patient Identifier.

## Consequences
Satisfy storage requirements for data at rest and transit. Satisfy requirements for providing secure data to EHR integrations.

**Positive:**

- ACID-compliant data - a requirement for data integrity, consistency, and reliability
- Supports various data formats including JSON and integrates with full-text search
- Compared to alternatives compared (SQL Server and MongoDB), PostgreSQL provides lower latency
- Supports vertical scalability

**Negative:**
Maintainability may be more compared to NoSQL database options like MongoDB.
Horizontal scalability limited


[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](010-Interoperability.md)  |  [Next >](./5.%20Proposed%20Solution/README.md)
