.. Adding labels to the beginning of your lab is helpful for linking to the lab from other pages
.. _endpoints:

-------------
Endpoints
-------------

Overview
++++++++

This Lab will show you how to create an Endpoint for Linux VMs. Endpoints are used by Runbooks to connect to the VM and execute the defined tasks. In the example below we will be using SSH keys for authentication, Endpoints can also be configured to use a username and password for authentication. Endpoints are also available within Calm Blueprints now, this gives the abiltity to address non local services as shown in the exersise below.

Get Started
++++++++++++++++++++++

Open \https://<*NUTANIX-CLUSTER-IP*>:9440 in your browser to access Prism. Log in as the admin HPOC user.

Click |hamburger_menu| **> Services > Calm >** |app_menu|


.. |hamburger_menu| image:: images/hamburger_menu.png

.. |app_menu| image:: images/app_menu.png

Here you can see two Applications that are being used in this exercise:

- linux_vms
- windows_vms

Create Endpoint 
++++++++++++++++++++++

First we will create an Endpoint for our Linux VMs.
You will need to collect the Private Key and IP addresses for the VMs first.

**Private Key**:
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

**IP Addresses**:

Click **linux_vms** in the App Menu.

Click **Services** in the top Menu and expand the VMs by clicking |expand|.

.. |expand| image:: images/expand.png

Click on each Service and note down the IP Address which will be displayed on the right hand side. 

-----------------------------------------------------

Click |endpoints_menu| **+ Create Endpoint**.

.. |endpoints_menu| image:: images/endpoints_menu.png

Fill out the following fields:

  - **Name** - *initials*_endpoint
  - **Description** - Endpoint for all Linux VMs
  - **IP Addresses** - *Insert the IPs you noted down earlier*
  - **Credentials - Username** - centos
  - **Credentials - Secret Type** - SSH Private Key
  - **Credentials - SSH Private Key** - *Copy & Paste the Key listed earlier*

.. image:: images/endpoint_linux_create.png

Click **Save**.

.. note::

  The Public Key needs to be defined in the Blueprint and added to the ssh-authorized-keys file, this is already done and not part of this exercise, but still important to know.

We now have an Endpoint which can be used by a Runbook to access all Linux VMs. 


Takeaways
+++++++++

- It is easy to create Endpoints for any VM simply by specifying its IP Address
- We could re-use the IP multiple times and create seperate Endpoints for Prod and non Prod environments
