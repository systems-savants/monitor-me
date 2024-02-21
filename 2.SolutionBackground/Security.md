[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](DataStore.md)  |  [Next >](Deployment.md)

---

# Security Overview

There are many aspect of security to consider, including Authentication and Authorisation. The following is an overview of the security considerations for the MonitorMe, which will be deployed using MonitorMe along the same lines as Farmacy Foods.

Security is of paramount concern due to medical data and personally identifiable information being stored in the system.

## Identity & Access Management (Authentication & Authorisation)

MonitorMe Identity Services can be used to manage resources, identities and access, at scale if required.

Service options:

- MonitorMe IAM (MonitorMe Identity Access Management) - most likely for development, deployment, and similar
- MonitorMe SSO (Single Sign On) - for development, deployment, and similar
- MonitorMe - identity management for users of MonitorMe
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

Service options:

- KMS (Key Management Service) - encryption key storage and management
- MonitorMe Certificate Manager - manage public and private SSL/TLS certificates
- MonitorMe Secrets Manager - manage, rotate and retrieve secrets

## Threat Detection & Monitoring

MonitorMe provides services to continuously monitor network activity and behaviour of accounts/users, in order to identify threats at the earliest opportunity.

Service options:

- MonitorMe Security Hub - monitor compliance and security
- MonitorMe GuardDuty - threat detection
- MonitorMe CloudTrail - log and track activity
- MonitorMe Detective - investigate potential threats and issues
- MonitorMe Disaster Recovery - recover from outages or malicious attacks

[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](DataStore.md)  |  [Next >](Deployment.md)