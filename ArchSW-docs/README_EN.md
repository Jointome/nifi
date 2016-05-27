#Arquitetura de Software
=================

Table of Contents
=================

 * [Description](#description)
  * [REPORT](#report)
    * [Introduction](#introduction)
    * [NIFI](#nifi)
    * [Diagrams](#diagrams)
        * [Logical View](#logical-view)
            * [Class Diagram](#class-diagram)
        * [Development View](#development-view)
            * [Component Diagram](#component-diagram)
            * [Package Diagram](#package-diagram)
        * [Process  View](#process--view)
            * [Activity Diagram](#activity-diagram)
        * [Physical View](#physical-view)
            * [Deployment Diagram](#deployment-diagram)
        * [Scenarios](#scenarios)
            * [Use Cases](#use-cases)


#Description
Nifi is a graphical interface designed to automatic data flows between different computer, networks, even when the protocols differ.

#REPORT

##Introduction

It is intended with this report to describe a study done to an application chosen by the group, within the Software Architecture discipline.

In an environment which we may find various systems, where some of them create and others consume data, often these systems differ in somes aspects, it becomes necessary to create something that simplifys communication between these systems.

NiFi was built to automate the flow of data between systems. It supports powerful and scalable directed graphs of data routing, transformation, and system mediation logic.  NiFi has a web-based user interface for design, control, feedback, and monitoring of dataflows.


##NIFI

//description of the program


->Processor: Processors actually perform the work. A processor does some combination of data Routing, Transformation, or Mediation between systems. Processors have access to attributes of a given FlowFile and its content stream. Processors can operate on zero or more FlowFiles in a given unit of work and either commit that work or rollback.

->Connection :  Connections provide the actual linkage between processors. These act as queues and allow various processes to interact at differing rates. These queues then can be prioritized dynamically and can have upper bounds on load, which enable back pressure.

->Flowfile: A FlowFile represents each object moving through the system and for each one, NiFi keeps track of a map of key/value pair attribute strings and its associated content of zero or more bytes.

->Flow Controller: The Flow Controller maintains the knowledge of how processes actually connect and manages the threads and allocations thereof which all processes use. The Flow Controller acts as the broker facilitating the exchange of FlowFiles between processors.

##Diagrams

Since Nifi is a real complex system, in some diagrams we had to focus on the most interesting part of the system, witch will be highlighted.

####Logical View
######Class Diagram

Has the class diagram is the moste complex of them all, we just focused on the processor api

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/classdiagram.jpg)

####Development View

The component diagram is used to represent components, ports, interfaces and relationships between all of the previously mentioned to form larger components and/or software systems. 

######Component Diagram
![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/component.png)

######Package Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/packagediagram.jpg)

####Process  View
######Activity Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/process.JPG)

####Physical View
######Deployment Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/deployment.png)


####Scenarios
######Use Cases
![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/scenarios.png)
