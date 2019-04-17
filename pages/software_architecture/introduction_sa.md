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

### Why Do we need SA?

![compare_architectures](https://wardballoon.github.io/images/compare_architectures.png)
SA is usually compared to drawing blueprint in architecture. If you build dog's house, it doesn't matter you have coworkers, blueprint, complex tools, or well-defined process. However, if you want to build your home, you need them all. When it comes to tall buildings, a lot of professionals from various area is needed and we need a central control. Software is the same as architecture. As the software grows in size, so does the software design. Learning SA teaches us how to draw the design of the software by taking into account a variety of things such as scale, Cost, Schedule, Stake holders, Skills and development teams, Materials and technologies, Risks, Development Process, and so on. As software in modern society is becoming more advanced, the importance of software architecture is also being highlighted.

### Definition of SA
Architecture is the fundamental organization of a system embodied in its components, their relationships to each other and to the environment and the principles guiding its design and evolution. [IEEE Standard on the Recommended Practice for Architectural Descriptions, 2000]

### Objectives of SA
![sa_goal](https://wardballoon.github.io/images/sa_goal.png)
The goal of SA is setting certain parameters (design variables) needed to be determined and achieve the best measurable performance (objective function) under given constraints.

### Common Aspects in Software Architecture Problem

- There are multiple solutions to the problem; and the optimal solution is to be identified.
- There exist one or more objectives to accomplish and a measure of how well these objectives are accomplished (measurable performance).
- Constraints of different forms (hard, soft) are imposed.
- There are several key influencing variables. The change of their values will influence (either improve or worsen) the “measurable performance” and the degree of violation of the “constraints.

## Software Modeling

### Objectives of Software Modeling

![software_pl_shift](https://wardballoon.github.io/images/software_pl_shift.png)

Why do we need software modeling? It makes it easier for team members to understand software clearly and in common, and helps improve the functionality and quality of the software system. These advantages have led to a lot of research and use of modelling languages.

## 4+1 Modeling Views

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

## Software development process and modeling

![development_process](https://wardballoon.github.io/images/development_process.png)
In this process, we need to consider the how to design the optimal SW architecture to meet the required functionality and quality/constraints. Thus, it is important to set our mission first. For example, let's consider the SA of a Web Server. What should we consider?

1. What is the goal?
2. What is the requirement?
3.  What is the major concern?
4.  What are the design variables?
5.  What are the constraints?
6.  What are the influence factors?

Maybe, there are more than these. Let's discuss it.
