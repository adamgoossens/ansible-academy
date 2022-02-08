# Lab 1: Introduction to the Automation Platform

In this lab we'll introduce you to the broad structure of the Automation platform. 

By the end of this lab you will have:

* Learned a little about how automation platform is structured.
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

The mesh creates a single flat "network" from the perspective of the Automation Controller. When the controller tasks an execution node, that task is passed along 
nodes in the mesh until it reaches the desired execution node. There may be intermediate "hop nodes" between the controller and execution node, but the Controller 
will be unaware of them.

## Logging in

Your instructor will have given you a URL to access the automation controller.

Open it in your web browser of choice.

You will see a screen like this:

![AAP Login](/student_guide/images/lab1_login.png)

Your credentials will be:

|Username|Password    |
|--------|------------|
| userX  | 1800redhat |

Where "X" is your student number the facilitator assigned to you.

Go ahead an log in with your username and password.

## The Dashboard

Upon logging in you will see the Automation Platform Dashboard. This gives you an 'at-a-glance' view of the state of automation that you have access to. All 
workshop attendees are using the same platform, but Automation Platform has been configured to keep you isolated from one another.

We do this using the Automation Platform's multi-tenancy capability, **Organizations**.

![AAP Dashboard](/student_guide/images/lab1_dashboard.png)

## The Side Menu

The side menu gives you access to the various interfaces of the Automation Platform. What you can see will change depending on your permissions; for example,
you are unable to view the links to modify Platform-wide configuration as you do not have the permissions to do so.

Feel free to poke around in those areas that you can access; we will also cover some of them as we go through the workshop.

## Job Templates

In the left menu, click "Resources -> Templates":

![Template menu entry](/student_guide/images/lab1_templates_menu.png)

You will see something like this:

![Job template list](/student_guide/images/lab1_templates_screen.png)

"Job Templates" are defined pieces of automation that can be launched through a single-click. A job template will define:

* Which organisation the job template belongs to
* The credentials that need to be provided to the job.
* The project used by the job template (more on Projects later).
* Other configuration for the job, such as the execution environment (more later), privilege escalation, additional parameters, etc.

You will see three job templates have been made for you by default. You will use those in later labs as we build out an automation workflow.

For now, click on "Provision Virtual Machines". You'll see the following:

![Provision Virtual Machine job template](/student_guide/images/lab1_pvm_view.png)

This shows us one job template that we have pre-defined for you. Note the following:

* This is unique to your organisation.
* This resides within your personal Project; more on this next.
* We use a custom execution environment, called the "Academy Environment"; more on this next.
* We're using a credential here. You can *use* the credential, but you can't *view* the sensitive parts of the credential.

## Projects

Click "Projects" in the side menu, under "Resources". You'll see the following:

![Project list](/student_guide/images/lab1_project_list.png)

We have pre-defined a project for you. Projects are a logical collection of Ansible automation, usually held in source control.

Click on your personal project that we have created. You will see the following:

![Project overview](/student_guide/images/lab1_project_overview.png)

You're using automation that we have written for you, hosted in a source code repository on GitHub.

