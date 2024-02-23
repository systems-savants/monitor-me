[> Home](../README.md)    [> ADRs](README.md)

---

# Use API Gateway in self-hosted mode
Date: 2024-02-22

## Status

Accepted

## Context

Here we were looking for a component that will be the one stop solution for any data coming in or going out of the MonitorMe ecosystem.
Data going out of MonitorMe would be snpshot uploads to MyMedicalData.
Alerts and push notifications going out to StayHealty Mobile App.
Incoming data in future could be from MyMedicalData or from MonitorThem.
Options Considered - Ambassador api gateway , Mulesoft, Axway

## Decision

We decided to with Ambassador API gateway as it provides a secure and real-time communication option without having to provision or manage any servers to manage connections or large-scale data exchanges.
Given the requirement for integrating with EHR systems securely is via secure HTTP ,API Gateway made more sense.
## Consequences

**Positive:**

- Ease of setup and maintainability.
- Security


---

[> Home](../README.md)    [> ADRs](README.md)
