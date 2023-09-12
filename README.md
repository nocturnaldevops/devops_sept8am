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

