[> Home](../README.md)   [> Problem Background](README.md)
[< Prev](BusinessGoalsDriversAndRequirements.md)  |  [Next >](ActorsActionsAndComponents.md)

---

# Architecture Analysis

## Key Architecture Characteristics

By identifying the key architecture characteristics (capabilities) for this solution we can then identify the toward which *architecture style we are push toward* hence our *best* solution. Best practice is to identify seven or less architecture characteristics (capabilities). These, along with the implicit architecture characteristics, will then feed into the overall architecture of the MonitorMe system.

### Candidate Architecture Characteristics

performance    responsiveness    availability    fault-tolerance    scalability/elasticity    data integrity    data consistency    adaptability    extensibility    interoperability    concurrency    deployability    testability    abstraction    workflow    configurability    recoverability    reliability    authorisation    agility    cost    domain-partitioning    evolvability    integration

### Selected Architecture Characteristics

| Top 3 | Characteristic               | Source                                                       |
| ----- | ---------------------------- | ------------------------------------------------------------ |
| Y     | Interoperability/Integration | Integration of patient's vital sign devices with MonitorMe (analyzing streaming data), and with MyMedicalData. |
|       | Data Integrity               | Pending. |
|       | Scalability/Elasticity       | ....., likely to require more resources (especially computational and storage) at different times. |
| Y     | [Real-Time] Performance      | Vital signs data is send to consolidated monitoring screen with an average response time of 1 second or less. |
| Y     | High Availability            | Pending. |
|       | Deployability                | Pending. |

### Implicit Architecture Characteristics

The following are a bedrock of architecture characteristics. They may not affect the *structure* but will feed into the overall architecture.

- Usability
- Security, authentication and authorization
- Maintainability
- Simplicity or observability?

Note that Configurability was considered for patients.

---

## Architectural Quanta

Of the characteristics identified above, do they apply to the whole system or are there clear sets applying to different parts of the system?

### Table View

| Identified Domains                                    | Sub-domains and Considerations                               | Applicable Architectural Characteristics                     | Strategic Domain |
| ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------- |
| Users                                                 | Patient, Preferences, Profile (Personal & Medical), Nurse, Doctor, Administrator?, Onboarding, Integration (MonitorMe) | - Interoperability (moved to Interface)<br />- Configurability<br />- Authorisation<br />- Workflow<br />- Fault-Tolerance<br />- Data-Integrity | Supportive       |
| Security                                              | Authentication, Authorisation                                | - Authorisation<br />- Data Integrity<br />-Interoperability (moved to Interface) | Generic          |
| Data Store                                            | Database, Interface                                          | - Data Integrity<br />- Authorisation                        | Generic          |
| Class (localised, temporal)                           |                                                              | - Configurability<br />- Fault Tolerance                     | Core             |
| Event (in-person, localised, temporal)                |                                                              | - Configurability<br />Fault Tolerance                       | Core             |
| Forum (localised, temporal)                           |                                                              | - Configurability<br />- Fault Tolerance                     | Core             |
| Reference Material / Media (global, reference/static) | Media Library, Vital Signs                              | - Scalability/Elasticity                                     | Generic          |
| Messaging                                             | Email, Message, Notification, Subscription?                  | - Workflow                                                   | Supportive       |
| Interface                                             |                                                              | - Interoperability<br />- Authorisation<br />- Data-Integrity | Supportive       |

### Venn Diagram

This diagram illustrates that although there are many shared characteristics, even those that are shared are shared by domains that do not themselves overlap. This leads us to a distributed architecture with deployment, backup and disaster recovery needing to take into account these characteristics. These characteristics may also inform further granularity of these domains.

![CharacteristicsVennDiagram](../assets/diagrams/CharacteristicsVennDiagram.png)

---

## System Granularity

A breakdown of the key granularity analysis and links to ADRs.

### Users

| Functionality | Volatility | Scalability             | Fault Tolerance                | Data Security | Data Transactions              | Data Dependencies            | Workflow             |
| ------------- | ---------- | ----------------------- | ------------------------------ | ------------- | ------------------------------ | ---------------------------- | -------------------- |
| Patient       | Low        | Unlikely to be required | Split required                 | High          | Profile, Onboarding, Message   | Security, Messages           | Separate             |
| Doctor        | Low        | Unlikely to be required | Could be merged with Nursen    | High          | Vital Signs, Message           | Profile, Messages            | Similar to Clinic    |
| Nurse         | Low        | Unlikely to be required | Could be merged with Doctor    | High          | Vital Signs, Message           | Vital Signs, Messages        | Similar to Dietician |
| MonitorMe     | Low        | Unlikely to be required | Split required                 | High          | Manage patients, data, alerts  | (all above)                  | Separate             |

[ADR: pending](../4.ADRs/pending.md)

### Security

| Functionality  | Volatility | Scalability             | Fault Tolerance                                              | Data Security | Data Transactions                                    | Data Dependencies | Workflow |
| -------------- | ---------- | ----------------------- | ------------------------------------------------------------ | ------------- | ---------------------------------------------------- | ----------------- | -------- |
| Authentication | Low        | Unlikely to be required | Don't want one without the other, could be merged with Authorisation | High          | User email/username, User password (hashed/salted)   | User              | Separate |
| Authorisation  | Low        | Unlikely to be required | Don't want one without the other, could be merged with Authentication | High          | User Roles / Permissions, User authentication status | User              | Separate |

[ADR: Combine Authentication and Authorisation into one Security Domain](../4.ADRs/012-We-will-combine-authentication-and-athorisation.md)


### Messaging

| Functionality             | Volatility | Scalability  | Fault Tolerance                                   | Data Security | Data Transactions                                            | Data Dependencies                         | Workflow |
| ------------------------- | ---------- | ------------ | ------------------------------------------------- | ------------- | ------------------------------------------------------------ | ----------------------------------------- | -------- |
| Notification              | Low        | Medium usage | Split required from Subscription                  | Low           | Notification (inc. status), Message status, Subscription event | User, Subscription, Message, Notification | Separate |
| Message                   | Low        | Medium usage | Split required from Subscription                  | High          | User Id, Message, Message Id                                 | User (Customer, Dietician), Message       | Separate |
| Email                     | Low        | Medium usage | Split required from Subscription                  | Medium        | User email address                                           | User                                      | Separate |
| Subscription (add/remove) | Medium     | Low usage    | Split required from Notification, Message & Email | Low           | User Id, Forum/Event/Class Id, Subscription                  | User, Forum, Event, Class, Subscription   | Separate |

[ADR: Messaging will be split into Subscription, Message, Notification and Email](../4.ADRs/016-We-will-split-messaging-domain.md)

### Data Store

See [Datastore Solution Overview](../2.SolutionBackground/DataStore.md).

---

## Integration points for MonitorMe

| System        | Direction           | Elements         | Reasoning                                                    | Managed Through                                              |
| ------------- | ------------------- | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MonitorMe     | 2-way               | Patient          | So that MonitorMe can identify patients that are not pluck into their vital signs. | Interface, Authentication, Authorisation                     |
| MyMedicalData | Patient to Doctor   | Patient Snapshot | Medical professionals can generate holistic snapshots from a patient's consolidated vital signs at any time and then upload the patient holistic snapshot to MyMedicalData cloud-base app. | User (Medical Staff), Authentication, Authorisation |

[ADR: An Interface will be used for system-system integration](../4.ADRs/018-use-interface-for-system-system-integration.md)

[ADR: Authentication and Authorisation of users will be used for human-system integration](../4.ADRs/019-use-auth-for-human-system-integration.md)

---

## Architectural Governance

Compliance with Architectural decisions and designs is as important as compliance with security and code structure best practices. The latter are typically monitored using automated testing, audits, code reviews, acceptance criteria and penetration tests. The former is often forgotten and not even included in the acceptance criteria in a user story.

### Fitness Functions

Architectural Fitness Functions will be implemented in the MonitorMe system in order to govern compliance to architectural decisions and designs. Non-compliance will need to be fixed (or if there is good reason the decision recorder in an ADR and the Fitness Functions updated), in the same way as a failing test.

There are various options for implementing these functions, and either one option or a mixture could be optimal for this system. In AWS the following are some of the options to investigate:

- CloudWatch - notifications of non-compliance can be sent as emails, etc
- Kibana - a data visualization and exploration tool used for log and time-series analytics, application monitoring, and operational intelligence use cases
- Lambdas - it may be optimal to write our own Fitness Functions as AWS Lambdas

---

## Next Steps:

- [x] Make decisions and record in ADRs about system granularity.
- [ ] Create diagrams of the granularity decided above.
- [ ] Investigate options for Fitness Functions.

---

[> Home](../README.md)   [> Problem Background](README.md)
[< Prev](BusinessGoalsDriversAndRequirements.md)  |  [Next >](ActorsActionsAndComponents.md)