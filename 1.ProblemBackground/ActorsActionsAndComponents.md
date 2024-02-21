[> Home](../README.md)  [> Problem Background](README.md)
[< Prev](ArchitectureAnalysis.md)  |  [Next >](ConstraintsAndAssumptions.md)

---
# Actors, Actions & Components

The Actors on the system (typically the human users but can also include other systems) and the actions they take help to form the key scenarios, or flows, of the system. The following identifies the significant actors, actions and key scenarios that will inform the architecture of the MonitorMe system.

## Actors & Actions

The identified actors of MonitorMe and their actions are as follows:

| Actor                  | Actions                                                      |
| ---------------------- | ------------------------------------------------------------ |
| Patient                | * Places meal order on Farmacy Foods<br />* Registers on Farmacy Family to become an engaged customer<br /> |
| Nurse Station          | * Creates Farmacy Family profile/account (onboarding) <br />* Shares medical profile with Clinic/Dietician<br />* Interacts with fellow Engaged Customer <br />* Interacts with Dietician<br />* Registers for Event<br />* Registers for Class |
| System (MonitorMe)     | * Interacts with Engaged Customer<br />* Accesses health data of the Engaged Customer<br />* Gives customized diet plan to the Engaged Customer |

## Architecturally Components

The following are the most architecturally significant scenarios/flows, derived from the Actors and Actions above, which will shape the architecture of the MonitorMe system.

### 01  Onboard Patient to MonitorMe

A patient is hock up to all the patient-monitoring devices to collect the patient's vital signs.

![Scenario-OnboardMonitorMePatient](../assets/diagrams/Scenario-OnboardMonitorMePatient.png)

### 02 Share Patient's Vital Signs Data with MonitorMe and Nurse's station

The patient's vital signs data is stream to MonitorMe to be analyze and then send to a consolidated monitoring screen per nurse station.

![Scenario-SendVitalSignsToMonitorMe](../assets/diagrams/Scenario-SendVitalSignsToMonitorMe.png)

### 03 Medical Professionals receive alert push notifications

If any of vital sign device (or software) fails, MonitorMe must still function and sent alert push notifications to a StayHealthy mobile app as well as to the consolidated monitoring screen in each nurses station.

![Scenario-AlertNotifications](../assets/diagrams/Scenario-AlertNotifications.png)

### 04 Medical Professionals can generate holistic snapshots

Medical professionals can generate holistic snapshots from a patient's consolidated vital signs at any time and then upload the patient's holistic snapshot to MyMedicalData.

![Scenario-UploadHolisticSnapshot](../assets/diagrams/Scenario-UploadHolisticSnapshot.png)

------

[> Home](../README.md)  [> Problem Background](README.md)
[< Prev](ArchitectureAnalysis.md)  |  [Next >](ConstraintsAndAssumptions.md)