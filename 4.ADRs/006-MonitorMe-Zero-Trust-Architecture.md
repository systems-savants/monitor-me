[> Home](../README.md)    [> ADRs](README.md)

---

# MonitorMe Zero Trust Architecture

Date: 2024-02-15

## Status

Accepted

## Context

Here we were looking for a component and/or functionality that provides tight and hardened security in the MonitorMe ecosystem
1. Enhanced Security: Zero Trust principles like continuous verification and least privilege access could strengthen data security and minimize unauthorized access risks.
2. Improved Patient Privacy: By minimizing trust assumptions and implementing stricter access controls, patient data privacy could be better protected.
3. Scalability and Flexibility: A Zero Trust architecture can be adaptable to accommodate diverse devices, users, and data flows, aligning with MonitorMe's potential growth plans.
4. Regulatory Compliance: Zero Trust principles can help meet compliance requirements for data privacy regulations like HIPAA.

## Decision

We decided to implement and apply the zero-trust methodology which verifies explicitly, has the least privileged access, and assumes breach.
- Identities may be users, services, or devices.
- Devices create a large attack surface as data flows.
- Applications are the way that data is consumed.
- Networks should be segmented.
- Infrastructure on-premises represents a threat vector.
- Data should be classified, labelled, and encrypted based on its attributes.

## Consequences

**Positive:**

- Security
- Easy to access decisions.
- Easy to find out why a decision was made.
- Quick to learn how to create and use ADRs.

---

[> Home](../README.md)    [> ADRs](README.md)
