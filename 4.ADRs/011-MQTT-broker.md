[> Home](../README.md)    [> ADRs](README.md)

---

# MQTT Broker

Date: 2024-02-15

## Status

Accepted

## Context

Here we are looking for a mechanism to handle the incoming messages from multiple devices efficiently without any data loss.

## Decision

we decided on using a MQMT broker which will use MQTT protocol to recieve data from the devices.
Each device will have its seperate topic and the corresponding microservice will subscribe to that topic

## Consequences

**Positive:**

- Avoid data loss even, if the subscriber service is down ,messages from devices will not be lost.
- Having seperate topics and subscriber will ensure that in case of any issues in any of the components ,data from other devices is still available for consolidation.


---

[> Home](../README.md)    [> ADRs](README.md)