.. title:: Nutanix Calm Runbooks and Endpoints

.. toctree::
  :maxdepth: 3
  :caption: Labs
  :name: _labs
  :hidden:

  endpoints/endpoints
  runbooks/runbooks
  optionallabs/blueprint


.. _getting_started:

---------------
Getting Started
---------------

Welcome to the handson Workshop for Runbooks in CALM. This Workshop will cover the creation of an Endpoint for Linux and Windows VMs and a Runbook to execute specific tasks on those Endpoints. You will have to connect to a HPOC environment, the details for the HPOC are futher down. If any questions come up as part of the Workshop don't hesitate to ask.


Agenda
++++++

1. Create Endpoints for Linux VMs
2. Create RunBooks for log cleaning
3. Using Endpoints in Blueprints and creating Endpoints via API


Initial Setup
+++++++++++++

- Take note of the *Passwords* being used.
- Log into your virtual desktops (connection info below)


Environment Details
+++++++++++++++++++

Nutanix Workshops are intended to be run in the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises. You need to be connected to the VPN to access the Hosted POC environments.

.. raw:: html

   <iframe width="800" height="800" frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1oWRSgXdXJLDufiXRk0xShF83_iDxApZGwq7lLasAUfc/edit?userstoinvite=giridhar.shankar@nutanix.com&ts=5ed5f8bf&actionButton=1#gid=0">


Nutanix Version Info
++++++++++++++++++++

- **CALM Version** - 3.0.0
- **AOS Version** - 5.16.1.2
- **PC Version** - 5.17.0.2
