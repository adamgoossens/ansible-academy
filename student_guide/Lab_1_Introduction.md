# Lab 1: Introduction to the Automation Platform

In this lab we'll introduce you to the broad structure of the Automation platform. 

By the end of this lab you will have:

* Logged in to Ansible Automation Platform with your own user account.
* Taken a quick tour of the interface to see what you have access to.

## The structure of the Automation Platform

We won't go into deep detail about how Ansible Automation Platform is implemented.

For now, let's use the following diagram:

<<<< IMAGE GOES HERE >>>>

Let's discuss a few of these components in turn.

### Automation Controller

You will be working with the Automation Controller exclusively in this session. This is the user interface and application programming interface
to Ansible Automation Platform.

The **Automation Controller** is responsible for:

* User authentication
* Logging
* Credential management, or integration with 3rd party credential providers
* Tasking "execution nodes" to run desired automation
* Users, Teams and multi-tenancy management
* Application Programming Interface

We can have more than one automation controller in an environment. In this lab we only have one, but in a production environment you would deploy at least two for high availability.

### Execution Nodes

Ansible Automation Platform executes automation - your playbooks - on **execution nodes**. This is the only function these nodes perform.

When you ask the platform to launch a job, the platform will select an appropriate execution node and then send a task to that node.

The node will run your automation job and send results back to the Controller for you to view.

Execution nodes allow the platform to scale: as you start managing more and more equipment, you can add more execution nodes to handle the increased workload.

We also use execution nodes to allow the platform to manage workloads in different security domains - for example, using execution node "A" for workload in security domain "A", and execution node "B" for workload in security domain "B".

### Automation Mesh

A technical implementation detail that we won't go into in great depth - this connects the various nodes in the automation platform together. The mesh serves as 
transportation for automation jobs and their results, from controllers to execution nodes and back again.

## Logging in

Your instructor will have given you a URL to enter the 
