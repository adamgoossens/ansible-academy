# Lab 2: Launching a job

In the previous lab we toured the user interface. In this lab we are going to launch one of the pre-defined job templates we created for you.

## The Lab

Click on "Templates" under "Resources" in the left menu.

Then click on your "Provision Virtual Machines" job template; you will see a screen like this:

![Provision Virtual Machines](/student_guide/images/lab1_pvm_view.png)

We saw this in the previous lab. Note again that this job requires a credential - it is using your AWS Infrastructure Credential. You have permissions to **use** the credential in a job template, but no permissions to modify or view the credential.

When Automation Controller executes this job template it will inject the credential into the running playbook. Credentials may be injected as environment variables 
that can be used by the automation, or as files that the automation may access.

There are three buttons at the bottom of that screen: "Edit", "Launch" and "Delete".

Click "Launch". This is all you need to do to start the automation. You will be sent to a screen that looks like this:

![Job running screen](/student_guide/images/lab2_job_running.png)

Gradually you will see the box in the middle fill with the output of the Ansible automation that is running.

A "Job" is an execution of a given Job Template. We executed the "Provision Virtual Machines" job template, and now we are viewing the "Job" that results.

Give the job a minute or so to complete. Once complete, it will look something like this:

![Job complete](/student_guide/images/lab2_job_complete.png)

The automation has provisioned two virtual machines for you into Amazon Web Services.

In the top right of the job you will see the following:

![Job detail](/student_guide/images/lab2_job_buttons.png)

This tells us that within this job we executed:

* One Ansible "play". A play is a defined sequence of tasks that are run against one or more target hosts or devices.
* One Ansible "task". In this case, the automation has one task only: a task to provision virtual machines into AWS.
* Against one "host". This task was executed locally on the controller.
* The job ran for approximately 1 minute.

The two buttons to the right allow us to relaunch the job, or download the output of the job.

Feel free to go ahead and click the rocket icon to re-launch the job. Ansible is idempotent and so it will not create more virtual machines when the two we 
need are already there. If you launch it again, you will find it completes much faster and has zero changes.

## Reviewing the Job list

Click "Jobs" under "Views" in the left side menu. You will see the following:

![Job list](/student_guide/images/lab2_job_list.png)

In the example above there have been three jobs run - remember, all students are using this platform so the platform has actually run considerably more than
one job, but you only see the jobs that you have permission to see.

You can click the rocket icon to the right of any job to relaunch it again with exactly the same parameters as last time.

## Summing up

This is a very short lab. You have:

* Launched a piece of Ansible automation through a single click in the Controller.
* Provisioned two virtual machines into AWS, using a credential.
* Watched the output of that Job, then optionally relaunched it to see that it is *idempotent*.
* Reviewed the list of Jobs, noting that you can only view the Jobs your user has permission to see.

In the next lab we're going to create some new Job Templates and execute them, using automation that already exists in your project.
