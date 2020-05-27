*Script Provided Below*.. _blueprint:

-----------------------------------------
Using Endpoints in Blueprints and creating Endpoints by API
-----------------------------------------

Overview
++++++++


In the :ref:`endpoints` lab you have explored how to create Endpoints as Destination for Runbooks.
When working with Calm Blueprints there are use cases where you need to execute code on Machines not part of the Calm-Blueprint.

To fill this need, Calm 3.0 is now able to run Tasks not only against the Service where it is defined but also against Endpoints.

Additonally it may be very useful to create an Endpoint together with a new Service in a Blueprint. As this is actual not integrated we will leverage API to create an Endpoint for our Services.


**In this lab you will leverage Set Variable to fetch Data from an existing Endpoint, your Linux Tools VM.**

Lab Setup
+++++++++

This lab assumes basic familiarity with Nutanix Calm.

You will create a new, blank Blueprint.

#. In **Prism Central**, select :fa:`bars` **> Services > Calm > Blueprints**.

#. Click **+ Create Blueprint > Multi VM/Pod Blueprint**.

   .. figure:: images/create_blueprint.png

#. Fill out the following fields and click **Proceed**:

   - **Name** - MyVM-*Initials*
   - **Description** - My First Endpoint Blueprint
   - **Project** - *Initials*-Calm


#. From the toolbar along the top of the blueprint, click **Credentials**.

#. Click **Credentials** :fa:`plus-circle` and fill out the following fields:

   - **Credential Name** - CENTOS
   - **Username** - centos
   - **Secret Type** - SSH Private Key
   - **Key** - Paste in your own private key, or use:

   ::

     -----BEGIN RSA PRIVATE KEY-----
     MIIEowIBAAKCAQEAii7qFDhVadLx5lULAG/ooCUTA/ATSmXbArs+GdHxbUWd/bNG
     ZCXnaQ2L1mSVVGDxfTbSaTJ3En3tVlMtD2RjZPdhqWESCaoj2kXLYSiNDS9qz3SK
     6h822je/f9O9CzCTrw2XGhnDVwmNraUvO5wmQObCDthTXc72PcBOd6oa4ENsnuY9
     HtiETg29TZXgCYPFXipLBHSZYkBmGgccAeY9dq5ywiywBJLuoSovXkkRJk3cd7Gy
     hCRIwYzqfdgSmiAMYgJLrz/UuLxatPqXts2D8v1xqR9EPNZNzgd4QHK4of1lqsNR
     uz2SxkwqLcXSw0mGcAL8mIwVpzhPzwmENC5OrwIBJQKCAQB++q2WCkCmbtByyrAp
     6ktiukjTL6MGGGhjX/PgYA5IvINX1SvtU0NZnb7FAntiSz7GFrODQyFPQ0jL3bq0
     MrwzRDA6x+cPzMb/7RvBEIGdadfFjbAVaMqfAsul5SpBokKFLxU6lDb2CMdhS67c
     1K2Hv0qKLpHL0vAdEZQ2nFAMWETvVMzl0o1dQmyGzA0GTY8VYdCRsUbwNgvFMvBj
     8T/svzjpASDifa7IXlGaLrXfCH584zt7y+qjJ05O1G0NFslQ9n2wi7F93N8rHxgl
     JDE4OhfyaDyLL1UdBlBpjYPSUbX7D5NExLggWEVFEwx4JRaK6+aDdFDKbSBIidHf
     h45NAoGBANjANRKLBtcxmW4foK5ILTuFkOaowqj+2AIgT1ezCVpErHDFg0bkuvDk
     QVdsAJRX5//luSO30dI0OWWGjgmIUXD7iej0sjAPJjRAv8ai+MYyaLfkdqv1Oj5c
     oDC3KjmSdXTuWSYNvarsW+Uf2v7zlZlWesTnpV6gkZH3tX86iuiZAoGBAKM0mKX0
     EjFkJH65Ym7gIED2CUyuFqq4WsCUD2RakpYZyIBKZGr8MRni3I4z6Hqm+rxVW6Dj
     uFGQe5GhgPvO23UG1Y6nm0VkYgZq81TraZc/oMzignSC95w7OsLaLn6qp32Fje1M
     Ez2Yn0T3dDcu1twY8OoDuvWx5LFMJ3NoRJaHAoGBAJ4rZP+xj17DVElxBo0EPK7k
     7TKygDYhwDjnJSRSN0HfFg0agmQqXucjGuzEbyAkeN1Um9vLU+xrTHqEyIN/Jqxk
     hztKxzfTtBhK7M84p7M5iq+0jfMau8ykdOVHZAB/odHeXLrnbrr/gVQsAKw1NdDC
     kPCNXP/c9JrzB+c4juEVAoGBAJGPxmp/vTL4c5OebIxnCAKWP6VBUnyWliFhdYME
     rECvNkjoZ2ZWjKhijVw8Il+OAjlFNgwJXzP9Z0qJIAMuHa2QeUfhmFKlo4ku9LOF
     2rdUbNJpKD5m+IRsLX1az4W6zLwPVRHp56WjzFJEfGiRjzMBfOxkMSBSjbLjDm3Z
     iUf7AoGBALjvtjapDwlEa5/CFvzOVGFq4L/OJTBEBGx/SA4HUc3TFTtlY2hvTDPZ
     dQr/JBzLBUjCOBVuUuH3uW7hGhW+DnlzrfbfJATaRR8Ht6VU651T+Gbrr8EqNpCP
     gmznERCNf9Kaxl/hlyV5dZBe/2LIK+/jLGNu9EJLoraaCBFshJKF
     -----END RSA PRIVATE KEY-----

   .. figure:: images/4.png

#. Click **Save** and then **Back**, ensuring no errors or warnings appear.

Create a basic Virtual Machine
+++++++++++++++++++++++++++++++

We will now create a basic Service which is needed for the next steps

.............................

#. In **Application Overview > Service**, click :fa:`plus-circle` to add a new Service.

   
   .. figure:: images/7.png

   
#. Fill out the following fields:

   - **Service Name** - MyVM
   - **Name** - VM1
   - **Cloud** - Nutanix
   - **OS** - Linux
   - **VM Name** -*Initials*-MyVM
   - **Image** - CentOS7Cloud
   - **Device Type** - Disk
   - **Device Bus** - SCSI
   - Select **Bootable**
   - **vCPUs** - 2
   - **Cores per vCPU** - 1
   - **Memory (GiB)** - 4
   - Select **Guest Customization**

     - **Type** - Cloud-init
     - **Script** -

       .. code-block:: bash

         #cloud-config
         users:
           - name: centos
             ssh-authorized-keys:
               - @@{CENTOS.public_key}@@
             sudo: ['ALL=(ALL) NOPASSWD:ALL']


   - Select :fa:`plus-circle` under **Network Adapters (NICs)**
   - **NIC 1** - Primary
   - **Credential** - CENTOS

#. Click **Save**.


   Now that you have completed the deployment details for the VM associated with the service, the next step is to leverage a Script on an Endpoint to collect additional Data for the VM.

#. Select the **MyVM** service. In the **Configuration Pane**, select the **Service** tab. Add a variable named **MYVAR**, leaving all other fields blank.

   .. figure:: images/myvar.png

Now that you have completed the deployment details for the VM associated with the service, the next step is to run a Set Variable against an Endpoint to fetch some needed Data.

#. With the **MyVM** service icon selected in the Workspace pane, scroll to the top of the **Configuration Panel**, and select the **Package** tab.

#. Specify **MyVM_PACKAGE** as the **Package Name** and click **Configure install**.

   - **Package Name** - MYVM_PACKAGE

   .. figure:: images/9.png

   Note the **Package install** field that appears on the MyVM service in the Workspace pane.

#. Select **+ Task**, and fill out the following fields in the **Configuration Panel** to define the script that Calm will remotely execute on the Endpoint:

   - **Task Name** - fetch_Mastertoken
   - **Type** - Set Variable
   - **Script Type** - Shell
   - **Enpoint** - Endpoint_LinuxToolsVM
   - **Script** -

     .. code-block:: bash

        echo "MYVAR=$(cat /etc/myservice/MasterToken)"

   .. figure:: images/fetchToken.png

  
   Reviewing the script you can see the package will fetch the content of a file on the Endpoint and store it in our MYVAR Variable



Testing the Endpoint-Task
++++++++++++++++++++++++++

#. **Launch** the blueprint. Name the application *Initials*\ **-EndpointCall**, and then click **Create**.

#. Once the application reaches **Running** status, select the **Services** tab.

#. Review the Variable by selecting the Service **MyVM > Services **

.. figure:: images/variableset.png

As you can see the Content of the File is pushed into the Variable.


Create Endpoints Automatically leveraging our API
++++++++++++++++++++++++++

Go back into the Blueprint Menu Clicking |blueprint_menu| > **MyVM**-*initials*

.. |blueprint_menu| image:: images/blueprint_menu.png

Click **Services** > **MyVM** > **Package** > **Install**
Now add another Task by clicking the **+ Task** and add the following info:
   - **Task Name** - create_endpoint
   - **Type** - Set Variable

Click **Browse Library**, select **api_create_endpoint**, click **Select** and click **Copy** in the next window.

.. figure:: images/add_task_create_endpoint.png

.. note::

  When you look at the script field you can see a comment that asks you to update two Variables if required, always check Library scripts for those.. we can leave the defaults for our use case as we are using Linux and the cred_user we created earlier is called centos as well.

We will now add another script under **Package** > **Uninstall** to make sure the endpoints get removed during delete.
Click **+ Task** in the Package Uninstall section just below the Install section and complete the following fields:
   - **Task Name** - remove_endpoint
   - **Type** - Execute 

Click **Browse Library**, select **api_remove_endpoint**, click **Select** and click **Copy** in the next window.

.. figure:: images/remove_endpoint.png

Click |save| and then |launch|

.. |save| image:: images/save.png

.. |launch| image:: images/launch.png

**Name of the Application** - *initials*_VM_wihtEndpoints

Calm will now Provision your VM, you can watch the progress in the **Audit** tab.

.............................

Once completed and the App shows |running| go into the Endpoint Menu by clicking |endpoint_menu|.

.. |endpoint_menu| image:: images/endpoints_menu.png

.. |running| image:: images/running.png


Here you can now see that the Endpoint **Endpoint**-*initials*-myvm was created automatically.

.............................

Now let us check if the Endpoint get deleted automatically as well.

Click |app_menu| and select the App you just deployed, now click **Action** > **Delete** and **Confirm**.

Once the delete has completed go back into the Endpoints Menu, as you can see the Endpoint was removed as well.

.. |app_menu| image:: images/app_menu.png


Takeaways
+++++++++
