[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](007-Deployment-Strategy.md)  |  [Next >](009-IoT-Device-Communication-MQTT-Protocol.md)

---

# 008 - Use of Infrastructure as Code (IaC)

Date: 2024-02-22

## Status

Accepted

## Context
Infrastructure deployment get complex and repeatable and time consuming and  boring it gets more error prone in the traditional imperative way, is prone to oversights and errors that can end with hogging most of server resources  and while other application are starved for server resources. Hunting down a small deviation from the design, such as having accidentally added a public IP to a machine, which can spell disaster. 

we can make good use of infrastructure as code languages and tool assisted generators to create infrastcuce and deployment more reliableThese declarative specifications describe the desired state in favour of the steps to reach such a state. Infrastructure as code is a way to script the declarative specification using a Domain Specific Language or a General Programming Language.

## Decision
Infrastructure as Code to build infrastructure and prevent drift and allows us to run architectural fitness functions on the specification instead of the run-time environment. This in turn allows us to test many scenarios without actually setting the deployment of the infrastructure in motion. We are guaranteed to run the tests against what will in fact be deployed when we decide to execute the specification. Therefore, creating a very agile and evolvable ecosystem. 

We can recommend Terraform to deploy kubernetes cluster, since it's declarative means what you want to build rather than how, it's multi vendor and also support kubernetes cluster to rollout container to deploy micro service features that assist the infrastructure engineer using visual designers but also checks on valid configurations. 

This will also help deploy 3rd party components like the Ambassador API Gateway and the MQTT component in containers, which supports the packaged deployment model for MonitorMe. 

## Consequences
The team will lose the ability to make ad-hoc changes without causing drift. Depending on the drift detection settings this may result in operational issues. Possibly even worse, you may assume the desired state while not being aware of the drift.

**Positive:**
small deployment make cost effective,faster & reliable,reconstitute infrastructure rapidly
Infrastructure code files can be checked into source control.
Can be integrated into CI/CD
IaC can be used to promote DevOps.
Repeatable due to idempotency
Drift detection
Remediation

**Negative:**
IaC APIs can be daunting at first.
IaC API documentation can be less mature than desired. This depends on the provider of the resource you want to provision.
Manual tweaks to the infrastructure at run-time cause drift.
- Need to on-board everyone on the project to understand ADRs.

**Risks:**
Incorrect policies set on the provisioning role (the role that executes the IaC) can result in escalated privileges on the run-time infrastructure environment. Even though this is not a problem specific to IaC it is, however, more prevalent.

---

[> Home](../README.md)  |  [> Architecture Decision Records](README.md) |  [< Prev](007-Deployment-Strategy.md)  |  [Next >](009-IoT-Device-Communication-MQTT-Protocol.md)
