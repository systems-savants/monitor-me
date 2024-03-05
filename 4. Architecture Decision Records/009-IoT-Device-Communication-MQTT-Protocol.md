[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](008-Use-of-Infrastructure-as-Code-(IaC).md)  |  [Next >](010-Interoperability.md)

---

# 009 - IoT Device Communication

Date: 2024-02-22

## Status

Accepted

## Context

Here we are looking for a mechanism to handle the incoming messages from multiple devices efficiently without any data loss.
Choices considered : Eclipse Mosquitto, AWS IoT Core, AWS IoT Green Grass, Rabbit MQ (with MQTT) 

## Decision

As the data collection and analysis is happening on premises we decide to go with HiveMQ MQTT Broker.
Each vital sign will have its own topic and the corresponding microservice will subscribe to that topic

## Consequences

**Positive:**

- Enterprise grade, high availibility, and ability to deploy via Kubernetes

---

[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](008-Use-of-Infrastructure-as-Code-(IaC).md)  |  [Next >](010-Interoperability.md)
