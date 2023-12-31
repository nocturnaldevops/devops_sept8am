# Maven Basics
**Maven** is a Java Based Build tool  
**Maven** is written in Java  
**Maven** is OpenSource  
**Maven** is from Apache Software Foundation  

## What is a build process?  
Software Build in simpler terms is an activity to translate the human-readable source code into the efficient executable program.  
Basically, Build is the process of creating the application program for a software release, by taking all the relevant source code files and compiling them and then creating a build artefact, such as binaries or executable program, etc.
# Build Tools
1) Maven
2) Ant
3) Gradle
4) Nant
5) Msbuild
6) Rake
7) npm

# Lifecycle of Maven
Maven Lifecycle comprises of three stages  
1) default -  lifecycle handles your project deployment
2) site -  handles the creation of your project's web site.
3) clean -  handles project cleaning

# Phases of Maven default Lifecyle  
1) validate -  validate the project is correct and all necessary information is available
2) compile - compile the source code of the project
3) test - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
4) package - take the compiled code and package it in its distributable format, such as a JAR.
5) verify - run any checks on results of integration tests to ensure quality criteria are met
6) install - install the package into the local repository, for use as a dependency in other projects locally
7) deploy - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

# What is POM?  
A Project Object Model or POM is the fundamental unit of work in Maven. It is an XML file that contains information about the project and configuration details used by Maven to build the project. It contains default values for most projects. Examples for this is the build directory, which is target; the source directory, which is src/main/java; the test source directory, which is src/test/java; and so on. When executing a task or goal, Maven looks for the POM in the current directory. It reads the POM, gets the needed configuration information, then executes the goal.

## Assignment:
Create an EC2 instance (ubuntu22.04)  
update the apt repo: sudo apt-get update  
Install maven: sudo apt-get install -y maven  
clone the repo: https://github.com/nocturnaldevops/Project1.git  
build the artifact : mvn package (make sure you run the command from the location where pom.xml is present).  
Identify the build (mark down the location)  

Other repos: https://github.com/koddas/war-web-project.git   
             https://github.com/jenkins-docs/simple-java-maven-app.git

Create an EC2 instance (ubuntu 22.04)  
update the apt repo: sudo apt-get update  
Install tomcat9 : sudo apt-get install -y tomcat9
Verify tomcat installation by running the command : sudo systemctl status tomcat9  
Verify tomcat availability by reaching to the url: http://publicipserver:8080  

## Copy the artifact from Server1 to Server2  
#### use scp command
server1: /home/ubuntu/Project1/target/devops.war  
server2: /var/lib/tomcat9/webapps/


# Solution  
BuildServer Ec2 Instance1  
userdata: include shell script  
#!/bin/bash  
sudo apt-get update  
sudo apt-get install -y maven  


TestServer Ec2 Instance2  
Edit network and open port 8080  
userdata: include shell script  
#!/bin/bash  
sudo apt-get update  
sudo apt-get install -y tomcat9

To change the hostnames of servers:  
**buildserver:** sudo hostnamectl set-hostname buildserver  
**testserver:** sudo hostnamectl set-hostname testserver  


clone repository into ec2instance1 (buildserver)  
git clone https://github.com/koddas/war-web-project.git  
mvn package  
copy the artifact  
scp devops.war ubuntu@172.31.33.143:/var/lib/tomcat9/webapps/app1.war  (fails!)

on the build server  
ssh-keygen  (hit enther thrice)
cat /home/ubuntu/.ssh/id_rsa.pub and copy the content  



On the test server  
change the permission of tomcat9 directory  
sudo chmod o+w -R /var/lib/tomcat9
echo "copied content id_rsa.pub from buildserver"  >> /home/ubuntu/.ssh/authorized_keys

From the build server again  
scp devops.war ubuntu@privIPtest:/var/lib/tomcat9/artifact.war  
open a browser: http://publicipoftest:artifact