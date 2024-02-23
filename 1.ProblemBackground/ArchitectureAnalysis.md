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
|       | Data Integrity               | Vital sign data analyzed and recorded through MonitorMe must be as accurate as possible as the human lives are at stake. |
|       | Scalability/Elasticity       | StayHealthy, Inc. is looking towards adding more vital sign monitoring devices for MonitorMe in the future. |
| Y     | [Real-Time] Performance      | Vital signs data is send to consolidated monitoring screen with an average response time of 1 second or less. |
| Y     | High Availability            | System needs to be available all the times as the medical professional need to monitor patients vitals and take decision based on them. |
|       | Deployability                | We are proposing a micro service architecture with a service for each device ,being able to deploy the whole system seemlessly is important. |

### Implicit Architecture Characteristics

The following are a bedrock of architecture characteristics. They may not affect the *structure* but will feed into the overall architecture.

- Usability
- Security, authentication and authorization
- Maintainability
- Simplicity or observability?

Note that Configurability was considered for patients.

![Architectural Characteristics](../assets/images/Architectural-characteristics-WS.png)

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
| Messaging                                             | Email, Message, Notification, Subscription?                  | - Workflow                                                   | Supportive       |
| Interface                                             |                                                              | - Interoperability<br />- Authorisation<br />- Data-Integrity | Supportive       |



## System Granularity

A breakdown of the key granularity analysis and links to ADRs.

### Users

| Functionality | Volatility | Scalability             | Fault Tolerance                | Data Security | Data Transactions              | Data Dependencies            | Workflow             |
| ------------- | ---------- | ----------------------- | ------------------------------ | ------------- | ------------------------------ | ---------------------------- | -------------------- |
| Patient       | Low        | Unlikely to be required | Split required                 | High          | Patient Vital Signs            | Security, Messages           | Separate             |
| Doctor        | Low        | Unlikely to be required | Could be merged with Nursen    | High          | Patient Vital Signs           | Profile, Messages            | Similar to Clinic    |
| Nurse         | Low        | Unlikely to be required | Could be merged with Doctor    | High          | Patient Vital Signs           | Vital Signs, Messages        | Similar to Dietician |
| MonitorMe     | Low        | Unlikely to be required | Split required                 | High          | Patient Vital Signs            | (all above)                  | Separate             |
| IT Staff      | Low        | Unlikely to be required | Split required                  | High          |                               | Security                  | Separate             |


### Security

| Functionality  | Volatility | Scalability             | Fault Tolerance                                              | Data Security | Data Transactions                                    | Data Dependencies | Workflow |
| -------------- | ---------- | ----------------------- | ------------------------------------------------------------ | ------------- | ---------------------------------------------------- | ----------------- | -------- |
| Authentication | Low        | Unlikely to be required | Don't want one without the other, could be merged with Authorisation | High          | User email/username, User password (hashed/salted)   | User              | Separate |
| Authorisation  | Low        | Unlikely to be required | Don't want one without the other, could be merged with Authentication | High          | User Roles / Permissions, User authentication status | User              | Separate |



### Messaging

| Functionality             | Volatility | Scalability  | Fault Tolerance                                   | Data Security | Data Transactions                                            | Data Dependencies                         | Workflow |
| ------------------------- | ---------- | ------------ | ------------------------------------------------- | ------------- | ------------------------------------------------------------ | ----------------------------------------- | -------- |
| Notification              | Low        | Medium usage | Split required from Subscription                  | Low           | Notification (inc. status), Message status, Subscription event | User, Subscription, Message, Notification | Separate |
| Message                   | Low        | Medium usage | Split required from Subscription                  | High          | User Id, Message, Message Id                                 | User (Customer, Dietician), Message       | Separate |
| Email                     | Low        | Medium usage | Split required from Subscription                  | Medium        | User email address                                           | User                                      | Separate |
| Subscription (add/remove) | Medium     | Low usage    | Split required from Notification, Message & Email | Low           | User Id, Forum/Event/Class Id, Subscription                  | User, Forum, Event, Class, Subscription   | Separate |

[ADR: MQTT Broker](../4.ADRs/011-MQTT-broker.md)

### Data Store

See [Datastore Solution Overview](../4.ADRs/013-Postgre-SQL-for-Data-Storage.md).

---

## Integration points for MonitorMe

| System        | Direction           | Elements         | Reasoning                                                    | Managed Through                                              |
| ------------- | ------------------- | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MonitorMe     | 2-way               | Patient          | So that MonitorMe can identify patients that are not pluck into their vital signs. | Interface, Authentication, Authorisation                     |
| MyMedicalData | Patient to Doctor   | Patient Snapshot | Medical professionals can generate holistic snapshots from a patient's consolidated vital signs at any time and then upload the patient holistic snapshot to MyMedicalData cloud-base app. | User (Medical Staff), Authentication, Authorisation |

[ADR: An Interface will be used for system-system integration](../4.ADRs/002-Use-API-Gateway-in-self-hosted-mode.md)

---

## Architectural Governance

Compliance with Architectural decisions and designs is as important as compliance with security and code structure best practices. The latter are typically monitored using automated testing, audits, code reviews, acceptance criteria and penetration tests. The former is often forgotten and not even included in the acceptance criteria in a user story.

---


[> Home](../README.md)   [> Problem Background](README.md)
[< Prev](BusinessGoalsDriversAndRequirements.md)  |  [Next >](ActorsActionsAndComponents.md)
