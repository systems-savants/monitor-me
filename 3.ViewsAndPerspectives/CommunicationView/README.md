[> Home](../../README.md)    [> Views & Perspectives](../README.md)
[< Prev](../C4Models/README.md)  |  [Next >](../../README.md#resources)

---

# View of Component Communication Between Patient, MyMedicalData, and MonitorMe

This gives an overview of how data is being passed between the existing MonitorMe system and MyMedicalData and Patients.

The existing solution already leverages a log stream as a means of async communication between its boundaries. This will mean integration events can be easily introduced.
This will require extending the current solution to emit events that must include more information such as the source of the event and payload type etc.
As a result of this we should use cloud events. See [ADR003- Component Communication](../../4.ADRs/003-component-communication.md)


![View Of Comunication](../../assets/diagrams/ffood-communication.png)

---

## Interesting integration points

1. **Home Healthcare Integration**:
  * Integrate with home-based medical devices and platforms to expand monitoring capabilities beyond hospital settings.
  * Enable remote patient monitoring at home, facilitating early intervention and potentially reducing hospital readmissions.
  * Provide personalized care plans and medication reminders directly through the MonitorMe platform.

2. **AI-powered Predictive Analytics**:
  * Integrate with advanced AI algorithms for predictive analysis of vital signs and health trends.
  * Proactively identify potential health risks and complications before they occur, enabling preventative measures.
  * Personalize patient care based on individual risk factors and predicted health outcomes.

3. **Telehealth and Remote Consultation**:
  * Integrate with telehealth platforms for remote consultations with specialists based on triggered alerts or specific patient needs.
  * Enable real-time data sharing and expert consultations directly through the MonitorMe platform, streamlining care coordination.
  * Improve access to specialist care for patients in remote locations or with limited mobility.


[> Home](../../README.md)    [> Views & Perspectives](../README.md)
[< Prev](../C4Models/README.md)  |  [Next >](../../README.md#resources)