---
title: GRASP design principle
keywords: GRASP,  Architecture
last_updated: April 19, 2019
tags: [software_architecture, grasp]
summary: "It it an article that introduces GRASP. It is a concept of object oriented analysis design. In fact, this job should be done before the software architecture design, but it's a necessary process, so I've put it in software architecture category. All this information is from Prof. Eunmi Choi at Kookmin University and Software Architecture in Practice, 3rd Edition."
sidebar: home_sidebar
permalink: grasp.html
folder: software_architecture
---

## General Responsibility Assignment Software Patterns (GRASP)

### What is GRASP

GRASP is a fundamental and universal object oriented design principles in the form of patterns. It provides direction for assigning responsibilities to the classes, identify the objects and responsibilities from the problem domain, and also identify how objects interact with each other. A contract or obligation of a class is determined in this process.

### Why we need it?

The skillful assignment of responsibilities is very important for changeability and reusability. It is usually expressed through interaction diagrams.

### Types

## GRASP patterns

### Low Coupling
It is a measurement of how strongly one class is connected to the other classes. If a class has high coupling, the class change force to change related classes. It is also hard to understand and reuse. Lower coupling has the benefit of low dependency and high reusability.

### High Cohesion
It is a measurement of how strongly related and focused the responsibilities of a class are. A class with highly related responsibilities, and which does not do a tremendous amount of work, has high cohesion. If a class has low cohesion, it does a lot of unrelated things or does too much work. It makes hard to comprehend, reuse, and maintain. If there are lots of high cohesion classes, it means the classses in the projects are low coupling.


### Expert

### Creator

### Controller

### Don’t talk to Stranger
