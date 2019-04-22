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

After identifying the requirements and creating a domain model, this is necessary to add methods to the appropriate software class and to perform the requirements (functions). The skillful assignment of responsibilities is very important for changeability and reusability. It is usually expressed through interaction diagrams.

## GRASP patterns

### Low Coupling

Coupling is a measurement of how strongly one class is connected to the other classes. If a class has high coupling, a class change forces to change related classes. It is also hard to understand and reuse. Lower coupling has the benefit of low dependency and high reusability.

### High Cohesion

Cohesion is a measurement of how strongly related and focused the responsibilities of a class are. A class with highly related responsibilities, and which does not do a tremendous amount of work, has high cohesion. If a class has low cohesion, it does a lot of unrelated things or does too much work. It makes hard to comprehend, reuse, and maintain. If there are lots of high cohesion classes, it means the classses in the projects are low coupling.


### Expert

Expert means that you should assign responsibility to the information expert (the class that has the information necessary to fulfill the responsibility). In this mechanism, encapsulation is maintained by using their own info, and lower their coupling.

### Creator

It is about deciding who can be creator based on the objects association and their interaction. You should put the responsibility to create an instance of class A if one of the following is true:

1. B aggregates A objects
2. B containsA objects
3. B records instances of A objects
4. B closely uses A objects
5. B has the initializing data that will be passed to A when it is created(thus B is an Expert with respect to creating A)

### Controller

In order to indirect coupling between external event sources and internal event handler, you should make an object (called Controller) responsible for receiving external events and forwarding them to the appropriate internal eventhandling object.

### Don’t talk to Stranger

If two classes have no reason to be directly aware of each other or to be otherwise coupled, then the two classes should not directly interact to lower coupling. Instead of having a class call, you should call that method indirectly through another class.
