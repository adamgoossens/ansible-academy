# Lab 4: Configure AWS Network Infrastructure

So far, you have:

* Provisioned two virtual machines into AWS.
* Configured those virtual machines with a simple web application.

But you are unable to access them and view the results of your efforts. 

To do this, we have provided an existing job template that you will need to run.

## The Lab

This will be a fairly quick lab.

Go to your list of job templates ("Templates" under "Resources" in the left menu).

In that list there is a job template labelled "Configure Load Balancer". Click the rocket icon to launch that job template:

![Load Balancer Job](/student_guide/images/lab4_lb.png)

This automation specifically adjusts the network load balancer in Amazon Web Servers to include your two virtual machines as a target. This is an example of using 
Ansible's large collection of modules to adjust a variety of infrastructure - not just virtual machines, but network infrastructure as well.

Once the job completes, you will be able to see a message printed in the window. This message will give you a web URL to access:

![LB URL](/student_guide/images/lab4_url.png)

Open another web browser tab and type in the URL you are provided. What you should see will look something like this:

![Application](/student_guide/images/lab4_accessing_app.png)

Refresh the screen. Each time you refresh you should see the server change - it will switch between the two virtual machines you have provisioned.

## Summing up

You have now:

* Provisioned two virtual machines in Amazon Web Services
* Refreshed your dynamic inventory to include those new VMs in Ansible Automation Platform.
* Created a job template to configure the virtual machines with a simple web page.
* Ran another job template to configure network infrastructure in AWS.
* Accessed your service via a web browser.

Currently, you would need to run each of your job templates manually, one after the other, to achieve the outcome you have now. This isn't ideal.

Instead, in the next lab we are going to:

* Tear down everything we just created in AWS.
* Link all of the job templates together into a Workflow.
* Run the workflow again, and view the results.

[On to the fifth and final Lab!](/student_guide/Lab_5_Creating_a_job_workflow.md)
