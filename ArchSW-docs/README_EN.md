#Arquitetura de Software

Table of Contents
=================

 1. [Introduction](#introduction)
 2. [NiFi](#NiFi)
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
 4. [Conclusion](#conclusion)
 5. [References](#references)


##Introduction

It is intended with this report to describe a study done to an application chosen by the group, within the Software Architecture discipline.

In an environment which we may find various systems, where some of them create and others consume data, often these systems differ in some aspects, it becomes necessary to create something that simplify communication between these systems.

NiFi was built to automate the flow of data between systems. It supports powerful and scalable directed graphs of data routing, transformation, and system mediation logic.  NiFi has a web-based user interface for design, control, feedback, and monitoring of dataflows.

To study the application architecture we use a set of Unified Modeling Language (UML) diagrams.   As soon, to define the logical view we use class diagram, for the process view we use  the activity diagram, for the development view we use two diagrams, component and package diagram, for the physical view we use a deployment diagram, and for scenarios we use the use cases diagram.

Due to the fact the application is very wide, in the diagrams construction we used only a few classes, these classes which are considered of great importance for the application.


#NiFi

NiFi is a graphical interface designed to automatic data flows between different computer, networks, even when the protocols differ.
Apache NiFi is a dataflow system based on the concepts of flow-based programming. It supports powerful and scalable directed graphs of data routing, transformation, and system mediation logic. NiFi has a web-based user interface for design, control, feedback, and monitoring of dataflows [1].


###Diagrams

Since NiFi is a real complex system, in some diagrams we had to focus on the most interesting part of the system, witch will be highlighted.

####Logical View
#####Class Diagram

![alt tag](https://github.com/Jointome/NiFi/blob/master/ArchSW-docs/Images/classdiagram.jpg)

As the class diagram is the most complex of all diagrams, we just focused on the Processor API. The Processor is the most important part of NiFi, because is the only Component to which access is given to create, remove, modify, or inspect FlowFiles (data and attributes). So next come the classes on the Processor API and what they do.

- The AbstractProcessor is the base class for all Processor Implementation, it provides several methods that will be of interest to Processor developers.

- The ProcessSession class, provides a mechanism by which FlowFiles can be created, destroyed, examined, cloned, and transferred to other Processors. 

- The ProcessContext provides information about how the Processor is currently configured making a connection between a Processor and the framework. Furthermore it allows the processor to perform Framework-specific tasks, such as controlling other Processors resources, to avoid consuming unnecessary resources.

- The ProcessSessionFactory creates the ProcessSession from the AbstractProcessor or the Processor classes.

- The Relationships define the routes to which a FlowFile may be transfered from a Processor. 

- The ProcessorInitializationContext exposes configuration to the Processor that doesn't change throughout the Processor life, like the unique identifier of the Processor.

####Development View
#####Component Diagram

![alt tag](https://github.com/Jointome/NiFi/blob/master/ArchSW-docs/Images/component.png)

NiFi has a lot of components which are difficult to understand. As so the component diagram can easily help to comprehend how the components fit together. Next we will explain what each component does and which components relate to each other and who.

- NiFi has the FlowFile. It represents structured data, such as a JSON or XML message, or may represent unstructured data, such as an image. The FlowFile is made up of content and attributes, in witch the content is a stream of bytes and the content is stored as a reference to the content itself, that is stored in the Content Repository. The content is accessed only by means of the Process Session, which is capable of communicating with the Content repository itself. These allows the data to be efficiently routed and reasoned about without parsing the content.

- Then it has the Processor, the most used and important component in NiFi. It is responsible for bringing data into the system, pushing data out to other systems, or performing some sort of enrichment, extraction, transformation, splitting, merging, or routing logic for a particular piece of data.


- The Processor Node is a wrapper around a Processor, it maintains the Processor state, the configured properties, settings, the Processor scheduled state, and the annotations that are used to describe the Processor. 

- A Reporting Task is a NiFi extension point, producing reports and analyzing NiFi's internal metrics providing information as bulletins that appear directly in the NiFi User Interface. It doesn't have access to individual FlowFiles, instead it has access to all Provenance Events, bulletins, and the metrics shown for components on the graph, such as FlowFiles in Bytes Read, and Bytes Written.

- The Controller Service is a mechanism that allows state or resources to be shared across multiple components in the flow. For example, if a very large dataset needs to be loaded, it will generally make sense to use a Controller Service to load it. This allows multiple Processors to make use of this dataset without having to load it multiple times.

- The Process Session makes a connection between Processors and FlowFiles and provides transactional behavior across the tasks that are performed by a Processor. It provides methods to read, write contents to FlowFiles, add and remove FlowFiles from the flow, add and remove attributes from a FlowFile, and route a FlowFile to a particular relationship.

- The Process Context provides a bridge between a Processor and its associated Processor Node, providing information about the Processor's current configuration. It also provides mechanisms for accessing the Controller Services that are available, so that Processors are able to take advantage of shared logic or shared resources.

- The FlowFile Repository is responsible for storing the FlowFiles attributes and state, it's considered a 'private API'.

- The Content Repository is responsible for storing the content of FlowFiles and providing mechanisms for reading the contents of a FlowFile. It is considered a 'private API'.

- The Provenance Repository is responsible for storing, retrieving, and querying all Data Provenance Events. Each time that a FlowFile is received, routed, cloned, forked, modified, sent, or dropped, a Provenance Event is generated that details this information. 

- The Provenance Repository allows this information to be stored about each FlowFile as it wonders through the system and provides a mechanism for assembling a "Lineage view" of a FlowFile, so that a graphical representation can be shown of exactly how the FlowFile was handled. It is considered a 'private API'.

- The Process Scheduler invokes the Processor or a Reporting Task by scheduling it. The scheduler is also responsible for scheduling framework tasks to run at periodic intervals and maintaining the schedule state of each component, as well as the current number of active threads. 

- FlowFile Queue is responsible for implementing quite a bit of logic. In addition to queuing the FlowFiles for another component to pull from, the FlowFile Queue must also be able to prioritize the data following the user's prioritization rules.

- FlowFile Prioritizer. The user has the ability to prioritize the data in whatever order makes sense for a particular dataflow at a particular point in time. 
 The FlowFile Queue is responsible for ensuring the data is ordered in the way that the user has chosen. This is accomplished by applying FlowFile Prioritizers to the queue. A FlowFile Prioritizer has access to all FlowFile information but does not have access to the data that it points to. The Prioritizer can then compare two FlowFiles in order to determine which should be made available first.

- The Flow Controller can be thought of as the bridge between the Web Tier and the back end components of a NiFi node. It is largely responsible for the initialization of the flow, the creation of components in the flow, and the coordination between those components. In a more general sense, the Flow Controller is responsible for maintaining system-wide state. This includes the state of the flow itself, and is responsible for coordinating connection and participation in a NiFi cluster.

- The Cluster Manager is responsible for maintaining system-wide state about an entire cluster. This includes information such as which nodes are in the cluster and the states of those nodes. Additionally, the Cluster Manager is responsible for acting as the bridge between the Web Tier and the cluster state. This includes replicating requests from the user to all nodes in the cluster and merging their responses.
An instance of NiFi will create either a Cluster Manager or a Flow Controller but never both.

- The Authority Provider is responsible for determining which users have access to perform which operations. It accomplishes this by providing a list of Authorities, or Roles, that a given user is allowed to possess. In this way, a central authority service can be used to dictate which Roles a given user is allowed to have, but just because a user is allowed to be granted the ADMIN role, for example, does not mean that the user should have the ADMIN role for a particular instance.

- Resources
NiFi's User Interface shows only information that is available via the NiFi RESTful API. This is accomplished by accessing the different end points that are defined in the *-Resource classes. For example, the ProcessorResource class is responsible for defining the end points that are used to interact with the different Processors in the flow, including the addition and removal of Processors. The ProvenanceResource class is responsible for defining the end points that are used to interact with the Provenance Repository, such as executing queries.

- The Bootstrap allows the user to easily configure how the NiFi JVM will be started by relying on the configuration provided in the bootstrap.properties file. This allows the application to easily be started with Remote Debugging enabled, with specified minimum and maximum heap sizes, and with other important JVM options.
Once the NiFi application has been started, the bootstrap is then responsible for monitoring NiFi and restarting the service as needed in order to ensure that the application continues to provide reliable dataflow.

- NarClassLoader
In a containerized environment like NiFi, it is important to allow different extension points to have arbitrary dependencies without those dependencies affecting other, unrelated extension points. In Java, the mechanism for doing this is the ClassLoader. NiFi defines its own implementation of the ClassLoader, the NarClassLoader. Each NiFi Archive (NAR) has its own NarClassLoader that is responsible for loading the classes defined in that NAR. Additionally, it is responsible for providing native library isolation, so that a Processor, for example, can depend on native libraries that are not shared with other components. This is accomplished by placing those native libraries in the NAR's native directory.



#####Package Diagram

![alt tag](https://github.com/Jointome/NiFi/blob/master/ArchSW-docs/Images/packagediagram.jpg)

The Package Diagram is complex, so we opted for studying only the API section. Following the definitions and explanations on the Component Diagram and the Class Diagram we can easily understand what is happening in the API package.
As we can see in the diagram the processor is the most solicited package, it can manipulate the FlowFile, annotations, reports, interact with components. Therefore we can see they all focus in the Processor in the end.
This Api allows the user to control a NiFi instance in real time.

####Process  View
#####Activity Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/process.JPG)

####Physical View
#####Deployment Diagram

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/deployment.png)

NiFi executes within a JVM living within a host operating system, and the NiFi components lives within the JVM. 

- **Web Server:** hosts NiFi’s HTTP-based command and control API.

- **Flow Controller:** is the brains of the operation. It provides threads for extensions to run on and manages their schedule of when they’ll receive resources to execute.

- **Extensions:** are operate/execute within the JVM. 

- **FlowFile Repository:** is where NiFi keeps track of the state of what it knows about a given FlowFile that is presently active in the flow. The implementation of the repository is pluggable. The default approach is a persistent Write-Ahead Log that lives on a specified disk partition.

- **Content Repository:** is where the actual content bytes of a given FlowFile live. The implementation of the repository is pluggable. The default approach is a fairly simple mechanism, which stores blocks of data in the file system. More than one file system storage location can be specified so as to get different physical partitions engaged to reduce contention on any single volume.

- **Provenance Repository:** is where all provenance event data is stored. The repository construct is pluggable with the default implementation being to use one or more physical disk volumes. Within each location event data is indexed and searchable.


####Scenarios
#####Use Cases

In order to use nifi, it's necessary to use a dataflow. The user can create one dataflow, use one template, or edit a previously used one.
When the user has te dataflow ready, the next step is to create a processor, or in case of using a template, configure. When the processor is in the dataflow, it's time to add the components, which can be of two types, input or output. After we can connect the components with themselves and with and the processor/processors. When all it's configured the dataflow can start and the user can also stop it.

![alt tag](https://github.com/Jointome/nifi/blob/master/ArchSW-docs/Images/scenarios.png)



##Conclusion


##References
