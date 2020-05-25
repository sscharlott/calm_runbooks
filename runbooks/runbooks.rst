.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _runbooks:

-------------
Runbooks
-------------

Overview
++++++++

This Lab will show you how to create a Runbook for Linux and Windows VMs. We will create a simple Runbook that can trigger Windows Updates and a more complex Runbook for the Linux Endpoints which includes the decision making process.

Get Started
++++++++++++++++++++++

Open \https://<*NUTANIX-CLUSTER-IP*>:9440 in your browser to access Prism. Log in as the admin HPOC user.

Click |hamburger_menu| **> Services > Calm >** |endpoints_menu|


.. |hamburger_menu| image:: images/hamburger_menu.png

.. |endpoints_menu| image:: images/endpoints_menu.png

Here you can see the endpoints we create in the previous exercise, we will be using both of them for our Runbooks.

Create Runbook for Windows VMs
++++++++++++++++++++++


Create Runbook for Linux VMs
+++++++++++++++++++++

+ Add Task

Task Name: Check OpenSSH installed
Type: Decision
Script Type: Shell
Endpoint: *leave empty*
Credential: *leave empty*
Script: rpm -qa | grep -i openssh-server

current Release: 13
new Release: 21


False

Add Task
Task Name: Check OpenSSH installed false
Type: Execute
Script Type: EScript
Endpoint: *leave empty*
Credential: *leave empty*
Script: print "no openssh installed, nothing to do"


True

Add Task
Task Name: Check OpenSSH installed true
Type: Decision
Script Type: Shell
Endpoint: *leave empty*
Credential: *leave empty*
Script: current=`rpm -qi openssh | grep Release | awk '{print $3}' | sed -e s/.el7_4//g`; if [ $current -ge "14" ]; then echo "Version is OK"; else (exit 1) fi



Takeaways
+++++++++

- Here is where we summarize any key takeaways from the module
- Such as how a Nutanix feature used in the lab delivers value
