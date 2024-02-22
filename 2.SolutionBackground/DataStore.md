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

[ADR: 013-Postgre-SQL-for-Data-Storage.md](../4.ADRs/013-Postgre-SQL-for-Data-Storage.md)

<img src="../assets/images/relational.png" width="150" height="150"/>


### Document

This type of data store is also not optimal for data that is highly connected. It is good for data that is unstructured (not all the same), e.g. would not fit well into the tables in a relational database due to null entries in various columns in different rows.

Analysis of the data required for MonitorMe may show that a document store would be optimal for all or some of the non-analytical or highly connected data, e.g. patient's profiles.

<img src="../assets/images/diagram.png" width="150" height="150"/>

### Blob

Binary Large Object storage is optimised for unstructured binary files that are large in size, e.g. videos and images. This would be the optimal type of storage for static content for MonitorMe.

<img src="../assets/images/binary-data.png" width="150" height="150"/>

### Graph

A graph database is optimal for highly connected data and can be very fast for performing analytics. It is also optimal for unstructured data, in the same way as a document store.

Without further analysis it would seem that a graph database would be optimal for the data that requires analytics and for also storing analytics of that data.

<img src="../assets/images/nodes.png" width="150" height="150"/>

## Graph Datastore Design Overview

The following diagram shows the initial design for the graph data store model. 

### Design Notes

- Even if an element, e.g. a large media file, will be stored in another way (e.g. blob storage) it can still be referenced and linked to in the graph data model, in order to link data in the graph store to elements outside of the graph store (e.g. a media node in the graph database would hold an identifier and/or link to a video file in blob storage).
- Date a time could be stored either as properties on a node or relationship, or as relationships to date/time nodes, or a mixture of both. This can be altered to tune performance when required.
- Properties of nodes and relationships are not shown on this high-level diagram.

![GraphDatastoreModel](../assets/diagrams/GraphDatastoreModel.png)

### General Analysis

- The graph structure lends itself well to analytics due to the nature of matching patterns when querying the graph.
- Relationships between nodes can be tuned to allow different or faster analysis, e.g. a PREVIOUS_RESULT relationship is shown below, between two results, which makes ordering results much quicker than selecting all results for a test and then ordering by date.

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
  
  <img src="../assets/diagrams/GraphDatastoreModel-Uploading.png" width="650"/>

## Next Steps

- [x] Create initial model for analytical data in a graph database.
- [ ] Analyse data needs to decide upon storage of non-analytical data: document, relational, or graph.
- [ ] Analyse analytical data needs to decide initial properties for the graph database nodes and relationships.
- [ ] Create model for storing of analytical results once the structure is known.

---

[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](SystemApproach.md)  |  [Next >](Security.md)

---

[Above icons made by: relational: [ultimatearm](https://www.flaticon.com/authors/ultimatearm), diagram: [Becris](https://www.flaticon.com/authors/becris), binary-data: [Juicy-Fish](https://www.flaticon.com/authors/juicy-fish), nodes: [Vitaly Gorbachev](https://www.flaticon.com/authors/vitaly-gorbachev) from [www.flaticon.com](https://www.flaticon.com/)]