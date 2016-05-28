#Arquitetura de Software
=================

Table of Contents
=================

 1. [Introduction](#introduction)
 2. [NIFI](#nifi)
 3. [Diagrams](#diagrams)
    1. [Logical View](#logical-view)
          1. [Class Diagram](#class-diagram)
    2. [Development View](#development-view)
          1. [Component Diagram](#component-diagram)
          2. [Package Diagram](#package-diagram)
    3. [Process  View](#process--view)
          1. [Activity Diagram](#activity-diagram)
    4. [Physical View](#physical-view)
          1. [Deployment Diagram](#deployment-diagram)
    5. [Scenarios](#scenarios)
          1. [Use Cases](#use-cases)


##Introduction

It is intended with this report to describe a study done to an application chosen by the group, within the Software Architecture discipline.

In an environment which we may find various systems, where some of them create and others consume data, often these systems differ in somes aspects, it becomes necessary to create something that simplifys communication between these systems.

NiFi was built to automate the flow of data between systems. It supports powerful and scalable directed graphs of data routing, transformation, and system mediation logic.  NiFi has a web-based user interface for design, control, feedback, and monitoring of dataflows.

To study the application architecture we use a set of Unified Modelling Language (UML) diagrams.   As soon, to define the logical view we use class diagram, for the process view we use  the activity diagram, for the development view we use two diagrams, component and package diagram, for the physical view we use a deployment diagram, and for senarios we use the use cases diagram.


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

Has the class diagram is the most complex of all diagrams, we just focused on the Processor API. The Processor is the most important part of nifi, because is the only Component to which access is given to create, remove, modify, or inspect FlowFiles (data and attributes). So next come the classes on the Processor API and what they do.

- The AbstractProcessor is the base class for all Processor Implementation, it provides several methods that will be of interest to Processor developers.

- The ProcessSession class, provides a mechanism by which FlowFiles can be created, destroyed, examined, cloned, and transferred to other Processors. 

- The ProcessContext provides information about how the Processor is currently configured making a connection between a Processor and the framework. Furthermore it allows the processor to perform Framework-specific tasks, has controling other Processors resoucers, to avoid consumig unnecessary resources.

- The ProcessSessionFactory creates the ProcessSession from the AbstractProcessor or the Processor classes.

- The Relationships define the routes to which a FlowFile may be transfered from a Processor. 

- The ProcessorInitializationContext exposes configuration to the Processor that doesn't change throughout the Processor life, like the unique identifier of the Processor.

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/classdiagram.jpg)


####Process  View
######Activity Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/process.JPG)


####Development View

The component diagram is used to represent components, ports, interfaces and relationships between all of the previously mentioned to form larger components and/or software systems. 

######Component Diagram
![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/component.png)

######Package Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/packagediagram.jpg)


####Physical View
######Deployment Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/deployment.png)


####Scenarios
######Use Cases
![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/scenarios.png)
