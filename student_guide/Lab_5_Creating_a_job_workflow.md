# Lab 5: Creating a Workflow

Up until now we have been working with individual job templates. Each of these follows the UNIX philosophy of doing one thing well.

But requiring people to run individual templates in sequence is tiresome and prone to error.

Instead, we are going to the Workflow function of Ansible Automation Platform to build out our own workflow that will execute our job templates in sequence.

## The Lab

### Tear down the infrastructure

To begin, let's tear down your virtual machines in Amazon Web Services. 

Go to your list of job templates ("Templates" under "Resources" in the left menu). Then, launch the "Teardown Environment" job template and wait for completion:

![Teardown complete](/student_guide/images/lab5_teardown_complete.png)

You will know this has worked by attempting to refresh the web browser to your application. Because the virtual machines have been deleted, you should instead 
see a page with an error message like this:

![503 Unavailable](/student_guide/images/lab5_service_unavailable.png)

### Create the workflow template

To create a workflow template, return to your Templates list ("Templates" under "Resources") and choose "Add", then "Add Workflow Template":

![Add Dropdown](/student_guide/images/lab3_add_dropdown.png)

Configure the workflow template with the below settings:

| Setting | Value |
| ------- | ----- |
| Name | Workflow - Deploy Web Application |
| Organization | Click the magnifying glass then select your organisation |

The result should look like this:

![Create Template](/student_guide/images/lab5_create_template.png)

Click "Save".

### Building the workflow

You will be immediately moved into the **Workflow Visualizer**, a graphical mechanism to create a workflow.

Being by clicking the "Start" button:

![Start](/student_guide/images/lab5_start.png)

Workflows are made up of **nodes**. Nodes can be of a few different types:

* Job template nodes will execute a job template.
* Inventory Source Sync nodes will sync the chosen dynamic inventory.
* Project Sync nodes will sync a project, i.e. pull down the latest Automation files from source control.
* Management Job nodes allow you to run Automation Platform management jobs.
* Workflow Job Template nodes allow you to run another workflow.

To begin, select "Job Template" as the node type, then choose the "Provision Virtual Machines" job template:

![Add Node](/student_guide/images/lab5_prov_vm_node.png)

You will see options for "Node Convergence" on this screen - ignore these for now. This allows you to control how the workflow behaves when several nodes 
link to a single node (i.e. do we wait for all previous tasks to complete, or start as soon as one of them completes?).

Click "Save". Your canvas will look like this:

![First Node](/student_guide/images/lab5_first_node.png)

So far, we have a workflow that will execute just our "Provision Virtual Machines" job template. If you recall from an earlier lab, we had to refresh our
dynamic inventory after provisioning the virtual machines. We will next add a node that will automatically refresh the dynamic inventory after the 
"Provision Virtual Machines" job completes successfully.

Hover your mouse over the "Provision Virtual Machines" node and click the plus icon:

![Add new node](/student_guide/images/lab5_add_sync_node.png)

You will bring up the "Add Node" screen:

![Add Node Screen](/student_guide/images/lab5_add_node.png)

Nodes may run on one of three conditions:

* **On success**, or only when the parent node completes successfully.
* **On Failure**, or when the parent node does not complete successfully.
* **Always**, always executes no matter what happens with the parent node.

You can use these conditions to create some complex workflows, e.g. including cleanup logic should parts of the workflow fail. We won't do that here;
instead, we will only be using the "On Success" condition.

Choose "On Success" and then click "Next".

On the next screen, change your "Node Type" to "Inventory Source Sync":

![Sync Node](/student_guide/images/lab5_sync_node.png)

You'll see that your dynamic inventory is listed. Click your "Amazon Web Services" inventory, then choose "Save". Your canvas will look like this:

![Canvas with sync node](/student_guide/images/lab5_canvas_sync_node.png)

**Note**: you can zoom in and out on the canvas using your scroll wheel on the mouse, and click and drag to move the canvas.

You now have a workflow that will provision your two virtual machines and then immediately trigger a dynamic inventory refresh from AWS.

### Complete the workflow

Next, go ahead and add the additional nodes yourself using the details in the table below:

| Node Type | Parent Node | Run Type | Job Template |
| --------- | ----------- | -------- |------------ |
| Job Template | Amazon Web Services | On Success | Configure Web Server |
| Job Template | Configure Web Server | On Success | Configure Load Balancer |

Your final canvas will look like this:

![Completed workflow](/student_guide/images/lab5_completed.png)

Once finished, click "Save" in the top right corner.

### Launch your workflow!

You will be returned to a familiar-looking job template screen. This will be the Workflow template you just created:

![Overview](/student_guide/images/lab5_workflow_overview.png)

The **Visualizer** tab along the top will allow you to re-enter the workflow visualiser that you were just in.

For now, let's test the workflow. Click "Launch":

![Running workflow](/student_guide/images/lab5_running_workflow.png)

Your workflow is running. Each of the nodes will be run in sequence. You can click on an individual node to see the progress of the job.

Give the workflow a few minutes to complete:

![Completed workflow](/student_guide/images/lab5_completed_worfklow.png)

Once it has completed, go back to your web browser to your personal URL that you used last time to access your application. If you need the URL again, click on 
the "Configure Load Balancer" node in the workflow you just ran and look at the output of the job.

If all went well, you will see a familiar looking page in your web browser:

![Working web app](/student_guide/images/lab5_working_app.png)

Congratulations! That concludes the main sequence of labs.

## Summing up

Over the last five labs, you have:

* Provisioned infrastructure into Amazon Web Services.
* Created your own job template to run automation through a single click.
* Used dynamic inventory provided through AWS integration.
* Used credentials without having access to those credentials to view or modify.
* Configured network infrastructure in AWS to allow you to access your web application.
* Destroyed your virtual machines.
* Created a workflow that sequences all of your job templates together.
* Verified that your application works by accessing your personal URL.
