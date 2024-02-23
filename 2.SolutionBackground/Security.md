[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](DataStore.md)  |  [Next >](Deployment.md)

---

# Security Overview

There are many aspects of security to consider, including Authentication (Identity) and Authorisation (Access Management). The following is an overview of the security considerations for the MonitorMe.

Security is of paramount concern due to medical data and personally identifiable information being stored in the system.

## Identity & Access Management (Authentication & Authorisation)

MonitorMe Identity Services can be used to manage resources, identities and access, at scale if required.

Service options:

- MonitorMe IAM (MonitorMe Identity & Access Management) - most likely for development, deployment, and similar
- MonitorMe SSO (Single Sign On) - for development, deployment, and similar
- MonitorMe Organisations - option for managing identity and access across Foods and Family

## Data Law & Compliance

Compliance status and monitoring are part of MonitorMe services, so MonitorMe can choose which standards and best practices to adhere to and have these automatically monitored.

Service options:

- MonitorMe Audit Manager - audit MonitorMe usage for risk assessment and compliance
- MonitorMe Artifact - compliance reporting

## Network & Infrastructure

Fine-grained security policies can be enforced on network traffic, particularly important when interfacing with other systems. Within MonitorMe we can use these controls to create a Zero Trust infrastructure to help protect against intruders who may manage to circumnavigate authentication controls.

Service options:

- MonitorMe Shield - DDoS protection
- MonitorMe WAF (Web Application Firewall), MonitorMe Network Firewall, & MonitorMe Firewall Manager - filter malicious traffic and implement zero-trust

## Data Protection

MonitorMe includes services such as Encryption and Key Management, allowing services to have their own authentication and authorisation, rather than storing secrets in code.

Data will be encrypted when at rest (e.g. in a database) and in transit (within the MonitorMe system and also when entering and exiting the system), with appropriately strong encryption.

Passwords will be stored only as salted hashes and the policy for length and complexity will follow current best practice (e.g. 10+ characters, at least 256 character higher length limit, NO need to include specific character types, check hacked/common password lists, NO need to change every x months, etc), and best practice password tips will be displayed.

**Please reference the below ADRs about security**

[MonitorMe Zero Trust Architecture](../4.ADRs/006-MonitorMe-Zero-Trust-Architecture.md) 

[MonitorMe Layered approach to security](../4.ADRs/007-MonitorMe-Layered-approach-to-security.md) 


[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](DataStore.md)  |  [Next >](Deployment.md)
