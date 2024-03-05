[> Home](../README.md)    [> ADRs](README.md)

---

# Layered approach to security

Date: 2024-02-22

## Status

Accepted

## Context

Here we are looking for a component, functionality, and governance that provides the most secure environment to the Hospital's internal data center and in the MonitorMe ecosystem.
1. Importance of Security: Given the sensitive nature of patient data and the potential consequences of security breaches, it is highly unlikely that MonitorMe relies on a single security measure. Layering different security controls provides more comprehensive protection.
2. Multifaceted Architecture: MonitorMe interacts with various components like devices, data storage, networks, and user interfaces, each requiring specific security considerations. A layered approach allows for tailored protection at different levels.
3. Industry Standards: Healthcare regulations and industry best practices often recommend layered security approaches for critical systems like patient monitoring.

## Decision

We decided to implement and apply a layered approach to security.
- Physical security such as limiting access to the hospital's internal data center to only authorized personnel.
- Identity and Access security controlling access to infrastructure and change control.
- Perimeter security including distributed denial of service (DDoS) protection to filter large-scale attacks before they can cause a denial of service for users (patients, medical professionals, IT staff, etc.)
- Network security can limit communication between resources using segmentation and access controls.
- The Computer layer can secure access to virtual machines on-premises by closing certain ports.
- Application security ensures that applications are secure and free of security vulnerabilities.
- Data layer security controls access to business and customer data, and encryption to protect data.

## Consequences

**Positive:**

- Security

---

[> Home](../README.md)    [> ADRs](README.md)
