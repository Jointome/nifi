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

Apache NiFi is a dataflow system based on the concepts of flow-based programming. It supports powerful and scalable directed graphs of data routing, transformation, and system mediation logic. NiFi has a web-based user interface for design, control, feedback, and monitoring of dataflows [1].

###Istallation and Getting Started

To getting started is necessary that you have a NiFi, and you can be downloaded it from the NiFi [download page] (http://nifi.apache.org/download.html). In the page you can choose the appropriate package for your operating system.

To install NiFi is required a JDK 1.7 or higher and the Apache Maven 3.1.0 or higher in the operative system. And the way that it can be installed depend the OS.

In our system (Linux), in the shell we use the command `mvn clean install` to build the application. After it be done, to test the application we created a new folder and we unpack the directory "nifi-0.5.1-bin”  that's locate in the directory nifi-assembly, from it to deploy NiFi, with the command `tar xzf target/nifi-*-bin.tar.gz -C ~/example-nifi-deploy`.

In the testing folder created we run in the shell the command `./bin/nifi.sh start` to start NiFi.

After NiFi has been started we can bring up the User Interface in order to create and monitor our dataflow. To use the User Interface we redirect a web browser to `http://localhost:8080/nifi`. The port 8080 is the default port, but it can be changed. As the port, other instances of NiFi like, security or data storage, can be configured, and for help it can be used the [adimin guide] (https://nifi.apache.org/docs/nifi-docs/html/administration-guide.html). 


->Processor: Processors actually perform the work. A processor does some combination of data Routing, Transformation, or Mediation between systems. Processors have access to attributes of a given FlowFile and its content stream. Processors can operate on zero or more FlowFiles in a given unit of work and either commit that work or rollback.

->Connection :  Connections provide the actual linkage between processors. These act as queues and allow various processes to interact at differing rates. These queues then can be prioritized dynamically and can have upper bounds on load, which enable back pressure.

->Flowfile: A FlowFile represents each object moving through the system and for each one, NiFi keeps track of a map of key/value pair attribute strings and its associated content of zero or more bytes.

->Flow Controller: The Flow Controller maintains the knowledge of how processes actually connect and manages the threads and allocations thereof which all processes use. The Flow Controller acts as the broker facilitating the exchange of FlowFiles between processors.

###Diagrams

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
