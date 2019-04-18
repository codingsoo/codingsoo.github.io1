---
title: Introduction of Software Architecture
keywords: SA, Sorftware Architecture, Introduction of Software Architecture
last_updated: April 17, 2019
tags: [introduction, software_architecture]
summary: "This article is an introduction of software architecture. Let's study why this is necessary and why it is important. All this information is from Prof. Eunmi Choi at Kookmin University and Software Architecture in Practice, 3rd Edition."
sidebar: home_sidebar
permalink: intro-software-architecture.html
folder: software_architecture
---

## Components and Objectives of Software Architecture (SA)

### Why do we need SA?

![compare_architectures](https://wardballoon.github.io/images/compare_architectures.png)

 SA is usually compared to drawing blueprint in construct architecture. If you build dog's house, it doesn't matter you have coworkers, blueprints, complex tools, or well-defined process. However, if you want to build your home, you need them all. When it comes to tall buildings, a lot of professionals from various area is needed and we need a central control. Same here, as the software grows in size, so does the software design. Learning SA teaches us how to draw the design of the software by taking into account a variety of things such as scale, Cost, Schedule, Stake holders, Skills and development teams, Materials and technologies, Risks, Development Process, and so on. As software in modern society is becoming more advanced, the importance of software architecture is also being highlighted.

### Definition and Objectives of SA

 Software Architecture is the fundamental organization of a system embodied in its components, their relationships to each other and to the environment and the principles guiding its design and evolution. [IEEE Standard on the Recommended Practice for Architectural Descriptions, 2000]

![sa_goal](https://wardballoon.github.io/images/sa_goal.png)

 The goal of SA is setting certain parameters (design variables) to achieve the best measurable performance (objective function) under given constraints.

### Common Aspects in Software Architecture Problem

- There are multiple solutions to the problem; and the optimal solution is to be identified.
- There exist one or more objectives to accomplish and a measure of how well these objectives are accomplished (measurable performance).
- Constraints of different forms (hard, soft) are imposed.
- There are several key influencing variables. The change of their values will influence (either improve or worsen) the measurable performance and the degree of violation of the constraints.

## Software Modeling

### Objectives of Software Modeling

![software_pl_shift](https://wardballoon.github.io/images/software_pl_shift.png)

 Why do we need software modeling? It makes team members to understand software clearly and in common, and helps improve the functionality and quality of the software system. These advantages have led to a lot of research and use of modelling languages.

### 4+1 Modeling Views

 4 + 1 Modeling View is an example of the software architecture model.

![modeling_view](https://wardballoon.github.io/images/modeling_view.png)

 It is composed of four views (4) and the use case (1) affects participation in all four views.

- Logical
    + Focus: Functional requirements of the system. It describes the requirements expressed in Use Case View to the structure and behavior of the system.
    + Contents: Class diagrams, Sequence diagrams, Layer diagrams.
- Implementation
    + Focus: Static organization of the software in its development environment. It is used by software developers to present UML model elements (Class and Interface) designed in Logical View and Process View as physical software modules.
    + Contents: Component diagram, Package diagrams.
- Process
    + Focus: Runtime behavior of the system, such as the system processes and communication, concurrency, performance and scalability (Focusing on the behavior by Thread and Process).
    + Contents: Activity diagrams.
- Deployment
    + Focus: System Engineer’s perspective, looking at the system topology, deployment and communication. It indicates the hardware to place the UML model elements (Component, Interface) defined in View.
    + Contents: Deployment diagrams.
- Scenarios
    + Focus: Use cases for illustrating and validating the architecture.
    + Contents: Use case diagrams.

### Software development process and modeling

![development_process](https://wardballoon.github.io/images/development_process.png)

 In this process, we need to consider how to design the optimal SW architecture to meet the required functionality and quality/constraints. Thus, it is important to set our mission first. For example, let's consider the SA of a Web Server. What should we consider?

1. What is the goal?
2. What is the requirement?
3.  What is the major concern?
4.  What are the design variables?
5.  What are the constraints?
6.  What are the influence factors?

Maybe, there are more than these. Let's discuss it.

## Architecture Design

### What is it?

![sa_design_when](https://wardballoon.github.io/images/sa_design_when.png)

 The mission of Architecture Design is to build a model that meets all customer's requirements and leads to successful implementation. It defines the relationship between major structural elements of the software. SRS (Requirement modeling and description which have functional / non-functional requirements) should be well-defined so that Elements, Connectors, Constraints, Attributes (advantages and disadvantages of the chosen structure) could be set precisely.

### Who does it for what?

Software architects and designers participate into Architecture Design using the software system requirements. During the translation process, they apply various design strategies to divide and conquer  the complexities of an application domain and resolve the software architecture. By doing this, they reduce risks, helps development teams work together in an orderly fashion, makes the system traceable for implementation and testing, and leads to software products that have higher quality attributes.

### Quality attributes

- Implementation attributes (not observable at runtime)
    + Interoperability: universal accessibility and the ability to exchange data among internal components
    + Maintainability and (functional) extensibility: the ability to modify the system and conveniently extend it.
    + Testability: the degree to which the system facilitates the establishment of test cases.
    + Portability: the system's level of independence on software and hardware platforms.
    + Scalability: a system's ability to adapt to an increase in user requests.
    + Flexibility: the ease of system modification to cater to different environments or problems for which the system was not originally designed.

- Runtime attributes (observable at runtime)
    + Availability: a system's capability to be available 24/7.
    + Security: a system's ability to cope with malicious attacks from outside or inside the system.
    + Performance: increasing a system's efficiency with regard to response time, throughput, and resource utilization
    + Usability: the level of human satisfaction from using the system.
    + Reliability: the failure frequency, the accuracy of output results, the Mean-Time-to-Failure (MTTF), the ability to recover from failure, and the failure predictability.
    + Maintainability(extensibility, adaptability, serviceability, testability, compatibility, and configurability): the ease of software system change.

- Business attributes
    + Time to market: the time it takes from requirements analysis to the date a product is released.
    + Cost: the expense of building, maintaining, and operating the system.
    + Lifetime: the period of time that the product is live before retirement.

### Software Architecture Design Guidelines

 This guideline is from Software Architecture and Design Illuminated written by Kai Qian, Xiang Fu, Lixin Tao, Chong-wei Xu.

- Think of what to do before thinking of how to do it: Functional and nonfunctional requirements should be identified, verified, and validated before architecture and detailed design work is done
- Think of abstract design before thinking of concrete design: Always start with an abstract design that specifies interfaces of components and abstract data types.
- Think of nonfunctional requirements early in the design process:When you map functional requirements to an architecture design, you should consider nonfunctional requirements as well.
- Think of software reusability and extensibility as much as possible: consider how to reuse existing software components to increase the reliability and cost-effectiveness of new systems.
- Try to promote high cohesion within each element and loose coupling between elements.
- Tolerate refinement of design: You may need to use prototyping and iteration to refine the design.
- Avoid ambiguous design and over-detailed design: Ambiguous design lacks constraints and over-detailed design restricts implementation.

### Ways to describe Software Architecture

 Software architecture specifies a high level of software system abstraction. It should be able to describe its collection of components and the connections, interact among these components, specify the deployment configuration of all components and connections, and conform to the project's functional and nonfunctional requirements.

- Box-and-line diagram: Boxes=> business concept diagram / Lines=> relationship among components
- UML: Structural (Static) Diagrams=> Behavioral (Dynamic) Diagrams
- Architecture View Models: 4+1 view model (logical view, process view, development view, physical view, and the user interface view)
- Architecture Description Language (ADL): describe software architecture formally and semantically.
