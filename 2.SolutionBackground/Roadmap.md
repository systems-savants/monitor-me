[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](Deployment.md)  |  [Next >](../4.ADRs/README.md)

---

# Project Roadmap

The following roadmap assumes MonitorMe is already in existence. If both systems were developed in parallel it is suggested that they could be more closely linked within AWS, possibly using the same event log and therefore not requiring specific interfaces between MonitorMe and Farmacy Family.

## Current System

The following diagram shows the conceptual design of the MonitorMe system, expected to be in existence:

![monitor-me-services](../assets/images/Monitorme_Overview_v1.png)


## First Iteration

**Aim**: Implement interfaces between MonitorMe and Patient vital sign devices and MyMedicalData, identifying if any unexpected changes are required to MonitorMe other than adding an interface.

### Main Tasks

1. Real-time data acquisition and processing: Continuously collect vital sign data from various patient-monitoring devices, ensuring efficient and accurate transmission, processing, and buffering for further analysis.
2. Vital sign analysis and alert generation: Analyze real-time and historical data for anomalies, compare with sleep status and context, trigger alerts based on pre-defined rules or AI models, and prioritize them based on severity and urgency.
3. Secure data storage and retrieval: Securely store and archive all vital sign data for historical analysis, reporting, and potential research purposes, ensuring data integrity and access control compliance.
4. Information dissemination and notification: Deliver alerts and patient snapshots to relevant healthcare professionals (nurses, doctors) through various channels like the consolidated monitoring screen, mobile app notifications, and visual cues.
5. System monitoring and maintenance: Continuously monitor system health, performance, and security, identify and address issues promptly, manage configurations and deployments, and ensure overall system reliability and uptime.

## (Suggested) Second Iteration

**Aim**: Implement Analytics and the Analytics Datastore (data to analyse and storage of analytics results), so that analytics can be run on MonitorMe data.

### Main Tasks

- Develop graph datastore for analytics data and results
- Develop Analytics component
  - Elements for MonitorMe only
- Any additional authentication and authorisation development required
- Integration testing, in line with testing developed for first iteration

### Considerations

- Development could be done in tandem for different components (including those in iteration one and two).
- Tandem development should be planned with consideration for when other components will be required
  - Especially in relation to the format of event messages in order to avoid volatility in interface contract code
- Mocks and test data should be used for integration with other components within the system when developing, and for testing in general.

### Suggested Prioritisation

1. Data Security and Privacy:
* Implement robust security measures like encryption, access control, and regular security audits to safeguard sensitive patient data.
* Ensure compliance with relevant healthcare data privacy regulations (e.g., HIPAA) to build trust and maintain ethical data practices.

2. Real-time Performance and Reliability:
* Prioritize real-time data processing and low latency alert delivery to ensure timely intervention for critical events.
* Implement high availability and fault tolerance mechanisms to guarantee minimal downtime and uninterrupted patient monitoring.

3. Accurate and Contextualized Alerts:
* Focus on refining algorithms and analysis rules for accurate anomaly detection and alert generation, considering factors like sleep status and patient history.
* Implement clear and actionable alert messages with severity levels and prioritization based on context for efficient response.

4. Healthcare Professional Integration:
* Prioritize user-friendly interfaces and clear information presentation on the monitoring screen and mobile app for intuitive use by nurses and doctors.
* Provide adequate training and support to healthcare professionals on system functionality and effective interpretation of alerts and data.

5. Scalability and Interoperability:
* Design the system with scalability in mind to accommodate future growth in patients and devices without compromising performance.
* Explore and potentially prioritize seamless integration with diverse medical devices beyond StayHealthy offerings, considering industry standards and data format compatibility.

## Intended System

The following diagram shows the intended conceptual design of the MonitorMe system, including the interface to MonitorMe:

![ContainerDiagram](../assets/diagrams/ContainerDiagram.png)

---

[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](Deployment.md)  |  [Next >](../4.ADRs/README.md)