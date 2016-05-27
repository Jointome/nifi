
Table of Contents
=================

  1. [Installation](#installation)
  2. [Execution](#execution) 

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


