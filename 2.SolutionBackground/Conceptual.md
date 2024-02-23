[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](ArchitecturePatterns.md)  |  [Next >](DataStore.md)

---

# Conceptual System Design

The following show the conceptual design for the MonitorMe system. More information about C4 modelling can be found in the [C4 Models section](../3.ViewsAndPerspectives/C4Models/README.md) of this documentation.

## Capacity Planning

![CapacityPlanning](../assets/images/CapacityPlanningData.png)

## MonitorMe Context Diagram

The Context diagram shows how the MonitorMe system interacts with patients and systems outside of the MonitorMe system, and how it fits in to the overall landscape.

Four types of user have been identified; Patient Vital Signs, Medical Professionals, and Pending. These are further defined in [Actors, Actions & Components](../1.ProblemBackground/ActorsActionsAndComponents.md), with full definitions in the [Glossary](../Glossary.md).

- The Administrator is required in order to manage other users, settings and data within the system. These privileges should only be given to specific, trusted employees of MonitorMe.
- The Medical Professionals is a user .... It is expected that there will be fine-grained authorisation controls so that a Medical Professional can be authorised to have this access, partial access, or not have access at all.
- Patient's Vital Signs are onboarded to MonitorMe.

![Context Diagram](../assets/diagrams/ContextDiagram.png)

## MonitorMe Container Diagram

The Container diagram shows elements/domains (containers) within the MonitorMe system and how they relate to each other and to patients and systems outside of the MonitorMe system. Domains within the system are further broken down into Component diagrams at the next level, and so the Container diagram hides implementation details in order to see the larger picture.

![Container Diagram](../assets/diagrams/ContainerDiagram.png)

## Architecturally Significant Component Diagrams

The following are the most architecturally significant Component diagrams for the MonitorMe system. Further Component diagrams can be created when other domains in the system are required to be developed in the [Roadmap](Roadmap.md).

### Medical Management

#### Relevant ADRs

- [005 use-crypto-shredding](../../4.ADRs/005-use-crypto-shredding.md)
- [010 We-will-use-a-secure-data-solution](../../4.ADRs/010-We-will-use-a-secure-data-solution.md)
- [017 Separate the Medical domain](../../4.ADRs/017-We-will-split-medical-domain.md)

![Medical Component Diagram](../assets/diagrams/MedicalComponentDiagram.png)

### User Management

#### Relevant ADRs

- [011 Separate the User domain](../../4.ADRs/011-We-will-separate-the-user-domain.md)
- [019 Use Authentication and Authorisation for human-system integration](../../4.ADRs/019-use-auth-for-human-system-integration.md)

![User Component Diagram](../assets/diagrams/UserComponentDiagram.png)

### Analytics

#### Relevant ADRs

- [008 Use a graph store for analytics](../../4.ADRs/008-We-will-use-a-graph-store-for-analytics.md)
- [015 Separate the Analytics domain](../../4.ADRs/015-We-will-split-analytics-domain.md)

![AnalyticsComponentDiagram](../assets/diagrams/AnalyticsComponentDiagram.png)

---

[> Home](../README.md)    [> Solution Background](README.md)
[< Prev](ArchitecturePatterns.md)  |  [Next >](DataStore.md)
