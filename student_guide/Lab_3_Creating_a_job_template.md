# Lab 3: Creating a Job Template

In this lab we will create a new job template that will configure your two resources in AWS as web servers.

By the end of the lab you will:

* Know how Job Templates are tied to projects and automation within.
* Have attached the correct credential to the template.
* Used privilege escalation to allow automation to complete.
* Run your new template against your virtual machines.

## The Lab

### Creating the template

Click "Templates" under "Resources" in the left menu. Then, click the blue "Add" dropdown button:

![Add Template Dropdown](/student_guide/images/lab3_add_dropdown.png)

Click "Add Job Template". You will create a new Workflow Template in a later lab.

You will be presented with a screen like this:

![New Template](/student_guide/images/lab3_create_template_form.png)

Configure your job template with the below settings:

| Setting | Value |
| ------- | ----- |
| Name    | Configure Web Server |
| Job Type | Run |
| Inventory | Click the magnifying glass icon and select your inventory |
| Project  | Academy Project - userX, where X is your number |
| Execution Environment | Click the magnifying glass icon and select "Academy Environment" |
| Playbook | configure-web-server.yml |

**Credentials**

Still on the same screen, click the magnifying glass next to Credentials. You will be presented with this screen:

![Select Credential](/student_guide/images/lab3_select_credential.png)

The **Machine** category is selected by default. Whilst on this screen, click the drop down arrow in the "Selected Category" box:

![Credential types](/student_guide/images/lab3_credential_types.png)

All of these entries are different systems that Ansible Automation Platform can manage credentials for. These are "Credential Types", and the ones shown here
come out of the box with the platform. You are able to create your own, custom Credential Types. We don't cover that in this workshop, however.

For now, select "Machine". Then select your "Virtual Machine Key (userX)" and click "Select":

![VM Key](/student_guide/images/lab3_vm_cred.png)

Your top half of the create job template form should look like this (replace "user2" with your own username):

![Job Template](/student_guide/images/lab3_half_complete_job_template.png)

Scroll down further to the options below the "Variables" section. We are only going to change one of these options - tick the box labelled "Privilege Escalation", then click "Save":

![Save Template](/student_guide/images/lab3_save.png)

**Privilege Escalation** is used to allow the automation to elevate privileges on the virtual machines. This is necessary to be able to install and configure 
software.

After saving, you should be presented with this screen:

![Job Template details](/student_guide/images/lab3_details.png)

### Launch!

Launch the job template - just like last time, click the "Launch" button and wait for the job to finish. You will see this:

![Skipped Hosts](/student_guide/images/lab3_skipped_hosts.png)

We have a problem - this automation should have run against your two virtual machines in AWS. Except it says "Skipping: no hosts matched".

What's going on?

### Slight Detour: Dynamic Inventory

In a previous lab we mentioned that we are using dynamic inventory - rather than manually add the hosts that Ansible Automation Platform will manage, instead 
we are going to use Ansible's ability to query Amazon Web Services to dynamically fetch host details.

What happened is that while you provisioned your two virtual machines in Lab 2, we haven't updated our dynamic inventory. We'll do this manually for now.

Click "Inventories" under "Resources" in the left menu.

Then, click on your inventory:

![Inventory](/student_guide/images/lab3_inventory.png)

Firsty, notice that we have a collection of variables specified in the inventory. This allows us to ensure that consistent parameters are provided to all
of the job templates you are building. In this workshop we're using this inventory file to provide a collection of details relating to provisioning resources 
into the right locations in AWS.

Along the top menu, select "Sources":

![Sources](/student_guide/images/lab3_sources_menu.png)

You will see the following:

![Source](/student_guide/images/lab3_sources.png)

**Sources** are dynamic inventory sources. These are **synchronised**, which causes them to query the source, fetch data about the hosts, and the automatically 
create the hosts and groups in your inventory.

Click the double arrows to the right of your "Amazon Web Services" inventory source, under the "Actions" heading - this will trigger a sync. Wait for it to complete:

![Sync successful](/student_guide/images/lab3_sync_successful.png)

Once completed, click "Hosts". You will now see your two AWS virtual machines listed (yours will look different to the below):

![Hosts](/student_guide/images/lab3_hosts.png)

Our inventory now has two hosts added, fetched dynamically from Amazon Web Services EC2. There are many possible sources for dynamic inventory, like Microsoft Azure, Red Hat Satellite, Red Hat OpenStack Platform, VMware vSphere, and more.

If you check under the "Groups" tab you will also now see two groups: "aws_ec2" and "webservers", and both of your hosts will be in the "webservers" group.

It is possible to require that dynamic inventory be re-synchronised before a job template is run, or to run the synchronisation on a schedule. In this workshop 
we will sync the inventory manually for now, and in a later lab you will include this step as part of an Automation Workflow.

Now we can go back and re-launch your job template.

### Launch attempt #2

Click "Templates" under "Resources" in the left menu.

Click the rocket icon to the right of your "Configure Web Server" job template to launch it again:

![Launch Template](/student_guide/images/lab3_cws_launch.png)

Wait for completion. This time you will see it will match your two hosts and proceed to configure them both. It will take a minute or two to complete:

![Configure Complete](/student_guide/images/lab3_configure_complete.png)

## Summing up

You have now:

* Created a new job template
* Attached a credential to this template
* Manually refreshed inventory from Amazon Web Services
* Successfully configured your two VMs as web servers

There's one step left to do - we are going to configure AWS network infrastructure to allow you to access your application.


