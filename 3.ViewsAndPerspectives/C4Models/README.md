[> Home](../../README.md)    [> Views & Perspectives](../README.md)
[< Prev](../scenarios/README.md)  |  [Next >](../CommunicationView/README.md)

---

# C4 Models

A C4 model is a common set of abstractions used to describe the static structure of a software system; these abstractions having four levels: **software system**, **containers**, **components** and **code**. **People** use the software system.

The following diagrams use the standard C4 notation.

## Context Diagram (Level 1 - top level)

A **System Context** diagram provides a starting point, showing how the software system in scope fits into the world around it.[^](#expl) 
This diagram shows how the main users of MonitorMe interact with the system, and the other systems that MonitorMe system interacts with.

**Simplified Context Diagram:**
![MonitorMe C4 model - C1-ContextDiagram](../../assets/images/Diagrams/MonitorMe_C4_model-C1-ContextDiagram.png)

## Container Diagram (Level 2)

A Container diagram zooms into the software system in scope, showing the high-level technical building blocks.[^](#exp1) The following diagram breaks down the MonitorMe system into groups of related functionality, or domains, and shows how they interact with each other and how the users of the system interact with the functionality.

**Simplified Container Diagram:**
![MonitorMe C4 model - C2-Container-Simplified](../../assets/images/Diagrams/MonitorMe_C4_model-C2-Container-Simplified.png)

**(Microservices) Expanded Containter Diagram:**
![MonitorMe C4 model - C2-Container-Expanded](../../assets/images/Diagrams/MonitorMe_C4_model-C2-Container-Expanded.png)

## Component Diagrams (Level 3)

A **Component** diagram zooms into an individual container, showing the components inside it.[^](#expl)

In our scenario, we decided to keep the perspectives limited to C1-System Context and C2-Container based.

C3 (Component) and C4 (Code) views/perspectives are excluded intentionally from our architecture approach given the extensive complexity and scale (in terms of number of components) of the solution .