[> Home](../README.md)   [> Problem Background](README.md)
[< Prev](README.md)  |  [Next >](StakeholderConcerns.md)

---

# Business Goals, Drivers and Requirements

## Background

MonitorMe is a new system (designed by Systems Savants) from the Architectural Katas: winter 2024.

### StayHealthy, Inc.

StayHealthy, Inc. is a large and highly successful medical software company located in San Francisco, CA, US. They currently have two popular cloud-based SaaS products: MonitorThem and MyMedicalData.

*MonitorThem* a comprehensive data analytics platform that is used for hospital trend and performance analytics—alert response times, patient health problem analytics, patient recovery analysis, and so on.

*MyMedicalData* is a comprehensive cloud-based patient medical records system used by doctors, nurses, and other heath professionals to record and track a patients heath records with guaranteed partitioning between patient records.

## Business Goals

1. Ensure accurate and real-time patient monitoring for improved care decisions.

2. Reduce response times to critical events through timely and actionable alerts.

3. Enhance data-driven insights for better patient outcomes and preventative measures.

By achieving these goals, MonitorMe can help to improve the quality of care for patients, reduce costs for healthcare providers, and save lives.

## Business Drivers 

StayHealthy, Inc. is now expanding into the medical monitoring market, and is in need of a new medical patient monitoring system for hospitals that monitors a patients vital signs using proprietary medical monitoring devices built by StayHealthy, Inc.

# Requirements and Engagement model

## Engagement Models

### Clients

MonitorMe's target clients are two-fold:

1. Individual Patients:
* Patients who require continuous monitoring due to chronic conditions like heart disease, sleep apnea, or diabetes.
* Patients recovering from surgery or other medical procedures who need close observation.
* Patients in critical care units where constant monitoring is essential.

2. Healthcare Providers:
* Hospitals and clinics looking to improve patient care and reduce costs.
* Nursing homes and long-term care facilities that need to monitor residents' health.
* Home healthcare agencies that provide remote monitoring services to patients in their homes.

Here's a table summarizing the key characteristics of MonitorMe's target clients:
| Client Type         | Key Characteristic           | Needs                                                        |
| ------------------- | ---------------------------- | ------------------------------------------------------------ |
| Individual Patients | Have chronic conditions, recovering from surgery, in critical care | Continuous monitoring, timely alerts, improved care outcomes. |
| Healthcare Providers| Hospitals, clinics, nursing homes, home healthcare agencies | Improved patient care, reduced costs, operational efficiency. |

## Architecturally Significant Business Requirements

| # | Significant Architectural Requirements | Business Goal |
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

### 7. Profile customization

MonitorMe users can customize patients vital sign threshold settings so that vital sign devices data analysis can be adjusted for each patient.

### 8. Third party relationships

MonitorMe has relationships with MeMedicalData.


## Significant Non-Functional requirements 

1. Intuitive consolidated vital data screen for Nurses which makes easy to understand data patterns

------

[> Home](../README.md)   [> Problem Background](README.md) 
[< Prev](README.md)  |  [Next >](ArchitectureAnalysis.md)
