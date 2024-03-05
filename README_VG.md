# Architectural Katas Winter 2024 - Systems Savants

<!-- <img src="assets/images/gold-medal.png" width="150" height="150"/> **1st Place Winners of the O'Reilly Architecture Katas Winter 2024** -->

> This documentation repository is hosted on GitHub here: [https://github.com/systems-savants/monitor-me](https://github.com/systems-savants/monitor-me)

Welcome to the System Savant's entry to the O'Reilly Winter 2024 Architectural Katas. We, the System Savants group, are a team of engineers from the health insurance and health services sector. With common objectives of learning and having fun, the team embarked on journey to create a solution for the stated problem. The aim of this documentation git repository is to communicate our design for the problem described for technical and non-technical team audiences alike.

Here's our [five-minute video presentation](https://www.linkedin.com/in/vishalgamji/) for the O'Reilly Architectural Kata.


<img src="assets/images/syst_savants_logo.png" alt="The Systems Savants logo" style="zoom:50%;" height="250" width="250" />

## Members
- Gibran Castillo [[LinkedIn](https://www.linkedin.com/in/gibran-castillo/)]
- Vishal Gamji [[LinkedIn](https://www.linkedin.com/in/vishalgamji/)]
- Harshada Kandalgaonkar [[LinkedIn](https://www.linkedin.com/in/harshada-kandalgaonkar/)]
- Subodh Gupta [[LinkedIn](https://www.linkedin.com/in/pending/)]


## Table of Contents 
```
1. Problem Background
  StayHealthy Inc. and MonitorMe
  Functional Requirements
  Glossary 
2. Problem Analysis
  Business Goals
  Business Drivers
  Engagement Model
  Other Considerations
3. Architecture Analysis
  Architecturally Significant Requirements
  Constraints
  Assumptions
  Actors, Actions, and Components
  Key Architecture Characteristics
IV. Use Cases
  Customer Journey
  Case 1. Customer orders via PoS
  Case 2. Customer orders online
  Maintenance and Failure Operations
V. Requirements
  Prioritized Architecture Characteristics
    1. Enable Discovery - Agility
    2. Affordable DevSecOps - Viability
    3. Easy to Pivot - Flexibility
    4. Availability
    5. Security
    6. Scalability
    7. Performance
  Design Constraints
VI. High-Level Architecture
  Web/Mobile Experience
  Offline Strategy for Smart Fridges
```
  
## Problem Background

### StayHealthy, Inc.

StayHealthy, Inc. is a large and highly successful medical software company located in San Francisco, CA, US. They currently have two popular cloud-based SaaS products: MonitorThem and MyMedicalData.

*MonitorThem* a comprehensive data analytics platform that is used for hospital trend and performance analytics—alert response times, patient health problem analytics, patient recovery analysis, and so on.

*MyMedicalData* is a comprehensive cloud-based patient medical records system used by doctors, nurses, and other heath professionals to record and track a patients heath records with guaranteed partitioning between patient records.

### MonitorMe - The Architecture Katas Challenge
MonitorMe is a new system (designed by Systems Savants) for StayHealthy, Inc. MonitorMe is a packaged hardware and software solution that must be installed on-premises at hospital locations, within the (IT) security bounds of the hospital organization, with means to integrate with external systems like MyMedicalData for Electronic Health Record (EHR) integration.  

### Functional Requirements
MonitorMe reads data from eight different patient-monitoring equipment vital sign input sources: heart rate, blood pressure, oxygen level, blood sugar, respiration rate, electrocardiogram (ECG), body temperature, and
sleep status (sleep or awake). It then sends the data to a consolidated monitoring screen (per nurses station) with an average response time of 1 second or less. The consolidated monitoring screen displays each patients
vital signs, rotating between patients every 5 seconds. There is a maximum of 20 patients per nurses station. 

* For each vital sign, MonitorMe must record and store the past 24 hours of all vital sign readings. A medical professional can review this history, filtering on time range as well as vital sign.
  
* In addition to recording raw monitoring data, the MonitorMe software must also analyze each patient’s vital signs and alert a medical professional if it detects an issue (e.g., decrease in oxygen level) or reaches a preset threshold (e.g., temperature has reached 104 degrees F).
  
* Some trend and threshold analysis is dependent on whether the patient is awake or asleep. For example, if the blood pressure drops, the system should notice that the patient is asleep and adjust its alerts accordingly.
The same is true with the respiration rate and heart rate. For example, all of these vital signs are reduced when the patient is asleep, but if awake something might be wrong.

* Medical professionals receive alert push notifications of a potential problem based on raw data analysis to a StayHeathy mobile app on their smart phone as well as the consolidated monitoring screen in each nurses
station.

* If any of vital sign device (or software) fails, MonitorMe must still function for other vital sign monitoring (monitor, record, analyze, and alert).
  
* Medical staff can generate holistic snapshots from a patients consolidated vital signs at any time. Medical staff can then upload the patient snapshot to MyMedicalData. The upload functionality is within the scope of the MonitorMe functionality and is done through a secure HTTP API call within MyMedicalData.
  
* Each patient monitoring device transmits vital sign readings at a different rate:
  Heart rate: every 500ms
  Blood pressure: every hour
  Oxygen level: every 5 seconds
  Blood sugar: every 2 minutes
  Respiration: every second
  ECG: every second
  Body temperature: every 5 minutes
  Sleep status: every 2 minutes

* MonitorMe will be deployed as an on-premises system. Each physical hospital location will have its own
installation of the complete MonitorMe system (including the recorded raw monitoring data).

* Maximum number of patients per physical MonitorMe instance: 500

* StayHealthy. Inc. will be providing a comprehensive hardware and software for this system. The platform, data
stores, databases, and other technical tools and products are unspecified at this time and will be based on your
on-prem architectural solution.

MonitorMe's architecture should also consider the following:
* StayHealthy, Inc. is looking towards adding more vital sign monitoring devices for MonitorMe in the future.

* Vital sign data analyzed and recorded through MonitorMe must be as accurate as possible. After all, human lives are at stake.

* As this is a new line of business for StayHealthy, they expect a lot of change as they learn more about this new market.
  
* StayHealthy, Inc. has always taken patient confidentially seriously. MonitorMe should be no exception to this rule. While patient monitoring data must be secure, MonitorMe does not have to meet any government
regulatory requirements (e.g., HIPPA).

[> Home](../README.md)  |  [< Prev](../1.ProblemBackground/StayHealthy.md)  |  [Next >](FunctionalRequirements.md)

## Glossary

The following are terms used in this documentation that may not be clear to all readers, and so are defined below.

| Term                   | Definition                                                   |
| ---------------------- | ------------------------------------------------------------ |
| IT Staff  | An IT user associated with the Hospital, employed by the hospital, who has means to observe, monitor, and troubleshoot MonitorMe's IoT devices, software, and hardware on-premises for L0 support. |
| Patient                | person who is receiving medical treatment from a doctor or hospital and using MonitorMe's proprietary IoT devices for health vital monitoring. |
| Medical Professional   | Doctors, Nurses, other medical staff that use MonitorMe systems. |
| MonitorMe         | The system to which this architecture documentation relates. |
| EHR Integration         | Electronic Health Record Integration in MonitorMe's scenario refers to integrating with MyMedicalData only. |


## Problem Analysis

### Business Goals

1. Ensure accurate and real-time patient monitoring for improved care decisions.

2. Reduce response times to critical events through timely and actionable alerts.

3. Enhance data-driven insights for better patient outcomes and preventative measures.

By achieving these goals, MonitorMe can help to improve the quality of care for patients, reduce costs for healthcare providers, and save lives.

### Business Drivers 

StayHealthy, Inc. is now expanding into the medical monitoring market, and is in need of a new medical patient monitoring system for hospitals that monitors a patients vital signs using proprietary medical monitoring devices built by StayHealthy, Inc.

### Engagement Model

MonitorMe's main personas are:

1. Individual Patients:
* Patients who require continuous monitoring due to chronic conditions like heart disease, sleep apnea, or diabetes.
* Patients recovering from surgery or other medical procedures who need close observation.
* Patients in critical care units where constant monitoring is essential.

2. Healthcare Providers & Staff:
* Hospitals and clinics looking to improve patient care and reduce costs.
* Nursing homes and long-term care facilities that need to monitor residents' health.
* Home healthcare agencies that provide remote monitoring services to patients in their homes.

Here's a table summarizing the key characteristics of MonitorMe's target clients:
| Client Type         | Key Characteristic           | Needs                                                        |
| ------------------- | ---------------------------- | ------------------------------------------------------------ |
| Individual Patients | Have chronic conditions, recovering from surgery, in critical care | Continuous monitoring, timely alerts, improved care outcomes. |
| Healthcare Providers & Staff| Hospitals, clinics, nursing homes, home healthcare agencies | Improved patient care, reduced costs, operational efficiency. |

### Other Considerations 

1. Intuitive and Easy-to-Use consolidated vital data screen for Nurses which makes easy to understand data patterns
2. Section 508 compliance: Section 508 of the Rehabilitation Act (29 U.S.C. 794d), as amended in 1998, is a federal law that requires agencies to provide individuals with disabilities equal access to electronic information and data comparable to those who do not have disabilities, unless an undue burden would be imposed on the agency.
3. HiTrust Certification: HITRUST provides a benchmark — a standardized compliance framework, assessment, and certification process — against which cloud service providers and covered health entities can measure compliance.
4. SOC2 Compliance: SOC 2, aka Service Organization Control Type 2, is a cybersecurity compliance framework developed by the American Institute of Certified Public Accountants (AICPA). The primary purpose of SOC 2 is to ensure that third-party service providers store and process client data in a secure manner.


## Architecturally Significant Requirements 

**Non-functional requirements are functional requirements! Say it a few more times and it will sink in.**  

| # | Requirement | Business Goal |
|----|----|----|
| 1 | Real-time processing | 1 |
| 2 | High throughput  | 1 |
| 3 | Low latency  | 1 |
| 4 | Horizontal scalability  | 2 |
| 5 | Vertical scalability  |  |
| 6 | High availability  | 3 |
| 7 | Fault tolerance  | 1 |
| 8 | Data encryption   | 2 |
| 9 | Support for diverse devices   | 1, 2 |
| 10 | Configurable analysis rules   |  2 |
| 11 | Future-proof design   |  2 |
| 12 | Data integrity   |  2 |
| 13 | Interoperability   |  2 |
| 14 | Maintainability and Operability   |  2 |


### 1. Patient profiles

Add a new system to manage patient profiles, allowing medical professionals, personalization around preferences and health care needs

### 2. Medical profile information

MonitorMe will provide the ability to upload holistic snapshots of a patient's consolidated vital signs at any time to then upload them into MyMedicalData.

### 3. Profile customization

MonitorMe users can customize patients vital sign threshold settings so that vital sign devices data analysis can be adjusted for each patient.

### 4. Third party Integrations

MonitorMe has integrations with systems that live outside of the hospital (IT) boundary party. Ex: MyMedicalData.

## Constraints

1. Ethical Considerations:
* Using AI and algorithms for patient monitoring raises ethical concerns about bias, transparency, and potential discrimination. Transparency in data collection, analysis, and decision-making is crucial.
* Informed consent and patient privacy need to be carefully addressed to ensure ethical data utilization.

2. Device Interoperability:
* Currently, the focus might be on StayHealthy devices, but future integration with diverse medical devices with varying data formats and communication protocols might pose challenges.
* Standardizing data formats and ensuring seamless interoperability can be complex and require collaboration across the healthcare industry.

3. Data Quality and Integrity:
* The accuracy of alerts and analysis heavily relies on the quality of data received from devices. Ensuring data integrity throughout the system is crucial.
* Factors like device calibration, data transmission errors, and missing data need to be addressed for reliable outcomes.

4. Human Factors:
* Healthcare professionals need proper training and ongoing support to effectively utilize and interpret information provided by MonitorMe.
* Alert fatigue and potential overreliance on the system can be risks, requiring clear guidelines and responsible use practices.

5. Security and Privacy:
* Protecting sensitive patient data from cyberattacks and unauthorized access is paramount. Robust security measures, encryption, and access control are essential.
* Regularly updating security protocols and monitoring system vulnerabilities are ongoing requirements.

6. Technology Limitations:
* AI algorithms might not be perfect, and potential biases or limitations need to be considered to avoid erroneous interpretations or missed critical events.
* Continuous innovation and adaptation of the system with evolving technologies and evolving patient needs are important.

7. The initial architecture in this repository must be completed by midnight US Eastern Time, 22nd February 2024.

## Assumptions

1. Technical Assumptions:
* Reliable network connectivity: Continuous and stable internet connection is crucial for data transmission and system operation.
* Standardized medical devices: MonitorMe might assume compatibility with standardized data formats and protocols used by most medical devices.
* Adequate computing resources: The system needs sufficient computational power and storage to handle real-time processing and data storage for all patients and devices.
* Availability of skilled IT personnel: Maintaining and operating the system efficiently requires skilled IT staff.

2. User Assumptions:
* Healthcare professionals are familiar with the system: User training and ongoing support might be needed to ensure proper utilization and interpretation of information.
* Patients understand and consent to data collection: Clear communication and informed consent are crucial for data privacy and ethical considerations.
* Alerts are promptly addressed: The system relies on healthcare professionals to respond to and investigate alerts in a timely manner.

3. Business Assumptions:
* Market demand for remote patient monitoring: The system's success depends on the demand for this type of technology in the healthcare market.
* Financial viability: Implementation and ongoing maintenance costs need to be balanced against the potential revenue and cost savings achieved through MonitorMe.
* Regulatory compliance: While MonitorMe doesn't have to comply with HIPAA, the team made an assumption to consider amd list out other regulations like SOC2, HiTrust, Section 508 for designing MonitorMe.

4. Additional Assumptions:
* Data quality and integrity: The accuracy of analysis and alerts depends on the quality of data received from devices.
* Cybersecurity threats: Measures need to be in place to mitigate potential security breaches and data leaks.
* Ethical considerations: The use of AI and data analysis in healthcare raises ethical questions that need to be addressed.
* The IT Staff at the hospital will serve as the first line of support for Level-0 troubleshooting and monitoring of MonitorMe as a self-serve system. StayHealthy, Inc. tech support will get involved in L1 and L2 escalations.



## Solution Structure

[Problem Background](1.ProblemBackground/README.md)

- [Business Goals, Drivers & Requirements](1.ProblemBackground/BusinessGoalsDriversAndRequirements.md)
- [Stakeholder Concerns](1.ProblemBackground/StakeholderConcerns.md)
- [Architecture Analysis](1.ProblemBackground/ArchitectureAnalysis.md)
- [Actors, Actions & Components](1.ProblemBackground/ActorsActionsAndComponents.md)
- [Constraints & Assumptions](1.ProblemBackground/ConstraintsAndAssumptions.md)
- [RAID Log](1.ProblemBackground/RAID.md)


[Solution Background](2.SolutionBackground/README.md)

- [Architecture Principles](2.SolutionBackground/ArchitecturePrinciples.md)
- [Overall Architecture Style Analysis](2.SolutionBackground/ArchitecturePatterns.md)
- [Conceptual System Design](2.SolutionBackground/Conceptual.md)
- [Data Store Solution](2.SolutionBackground/DataStore.md)
- [Security](2.SolutionBackground/Security.md)
- [Deployment](2.SolutionBackground/Deployment.md)
- [ADRs](4.ADRs/README.md)


[Views & Perspectives](3.ViewsAndPerspectives/README.md)

- [C4 Models](3.ViewsAndPerspectives/C4Models/README.md)

## Resources <a href='#' id='resources'></a>

- [2024 O'Reilly Architecture Katas Presentation](assets/docs/2024_oreilly_architectural_katas.pdf)
- [Carelon Architectural Katas Winter 2024](assets/docs/Architectual-Katas-Winter-2024.pdf)
- [Team Logo Generation by Dall-E](https://openai.com/dall-e-2)
- [Nurse Dashboard Image Generated by Dall-E](https://openai.com/dall-e-2)
- [Mobile App Image Generated by Dall-E](https://openai.com/dall-e-2)

## References

- [C4 Model](https://c4model.com/)
- [Amazon Web Services Outposts - Servers](https://aws.amazon.com/outposts/servers/?nc=sn&loc=3)
- [Ambassador API Gateway](https://www.getambassador.io/)
- [HiveMQ - MQTT Broker](https://www.hivemq.com/info/mqtt-broker)


---