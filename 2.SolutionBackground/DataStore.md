[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](SystemApproach.md)  |  [Next >](Security.md)

---

# Datastore Solution Overview

When considering the MonitorMe system there are three needs for storing data

- raw patient vital signs
- analyze patient vital signs
- holistic consolidated patient vital signs

The need for analytics of some data stored in MonitorMe, and for potentially large files, means that more than one type of data store could be optimal for the system (polyglot persistence).

## Considered Data Store Approaches

### Relational

This type of data store is optimal for data that is not highly connected. The need to create relationships via extra tables and joins slows down the storage and retrieval of data and makes the design and maintenance more complex. **Simplicity is an inherent architecture characteristic.**

Relational is an option for data that is not highly connected and not involved in analytics.

[ADR: 012-Postgre-SQL-for-Data-Storage.md](../4.ADRs/012-Postgre-SQL-for-Data-Storage.md)

<img src="../assets/images/relational.png" width="150" height="150"/>

### MonitorMe Vital Sign Analysis

- The Patient vital sign input sources: heart rate, blood pressure, oxygen level, blood sugar, respiration rate, electrocardiogram (ECG), body temperature, and
sleep status (sleep or awake).
- Analyze each patient’s vital signs and alert a medical professional if it detects an issue (e.g., decrease in oxygen level) or reaches a preset
threshold (e.g., temperature has reached 104 degrees F).
- Some trend and threshold analysis is dependent on whether the patient is awake or asleep.

<img src="../assets/diagrams/GraphDatastoreModel-VitalSignsAnalysis.png" width="500"/>

### Uploading

- Medical staff can generate holistic snapshots from a patients consolidated vital signs at any time. 
- Medical staff can then upload the patient snapshot to MyMedicalData. 
- The upload functionality is within the scope of the MonitorMe functionality and is done through a secure HTTP API call within MyMedicalData
  


[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](SystemApproach.md)  |  [Next >](Security.md)

---
