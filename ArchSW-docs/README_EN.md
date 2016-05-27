#Arquitetura de Software

Table of Contents
=================

  1) [Description](#description)
  2) [Installation](#installation)
  3) [Execution](#execution)
  4) [REPORT](#report)
    4.1) [Basics of NIFI](#basics-of-nifi)
        a) [Processor](#processor)
        b) [Component](#component)
        c) [Fileflow](#fileflow)
    5) [Diagrams](#diagrams)
        5.1) [Logical View](#logical-view)
            a) [Class Diagram](#class-diagram)
        5.2) [Development View](#development-view)
            a) [Component Diagram](#component-diagram)
            b) [Package Diagram](#package-diagram)
        5.3) [Process  View](#process--view)
            a) [Activity Diagram](#activity-diagram)
        5.4) [Physical View](#physical-view)
            a) [Deployment Diagram](#deployment-diagram)
        5.5) [Scenarios](#scenarios)
            a) [Use Cases](#use-cases)



#Description
Nifi is a graphical interface designed to automatic data flows between different computer, networks, even when the protocols differ.
  
#Installation
In order to install the project it is necessary to install the maven. We start by using the command 

`sudo apt-get install maven`

 which may result in the installation of an older version (check with `mvn -version command`). If the version is less than 3.1.0, you should go to https://maven.apache.org/download.cgi in order to download and follow the steps in the following link https://maven.apache.org/install.html . Then through the command line, access to the project directory and run the 
 
 `mvn clean install`
 
 command and wait for the end, wich may take a while. At the end you should access the NIFI-assembly directory that is in the project main folder. Run
 
`ls -lhd target/nifi*`

to check which version of NIFI is present, and then the command 

`mkdir ~/example-nifi-deploy`

`tar xzf target/nifi-*-bin.tar.gz -C ~/example-nifi-deploy`

`ls .l ~/example-nifi-deploy/".`

  
#Execution 
Once NiFi has been installed, it can be started by using the following mechanism appropriate for Linux/Mac OSX users.
In the terminal, navigate to the directory where NiFi was installed. And there are two ways to run NiFi: 

In the foreground using the command 
  
`./bin/nifi.sh run`

This will leave the application running until the user presses Ctrl-C.

Or in the background using the command

`./bin/nifi.sh start`

This will initiate the application to begin running.

After the NiFi has been started, for create and monitor dataflow we open a web browser and navigate to

http://localhost:8080/nifi/


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
<<<<<<< HEAD
Since Nifi is a real complex system, in some diagrams we had to focus on the most interesting part of the system, witch will be highlighted.
=======


>>>>>>> ef3041607052b3acd593f0b9c7dbd0783213f63b
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
