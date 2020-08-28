.. ...........................................................................
.. © Copyright IBM Corporation 2020                                          .
.. ...........................................................................

-----------

FINDPLACEINDOC: When we install yum, if public internet access is unavailable, you make need to create a local repo. 
This is outside the scope in this guide, find more info at LINK.

Beginners Guide


Items needed for this guide: 

* A Controller Node to install ansilbe on.

* A Managed Node(s) to apply the <NEED TO CHOOSE WHICH PLAYBOOK TO RUN>
  
   .. warning::
      There are several os architectures/flavors to choose from when installing ansible to your controller node. AIX is not supported. It also is not an ideal choice for starting out. For this guide we will use Red Hat Enterprise Linux 7.                                        This guide has also been tested with CentOS 7. Check this link for possible controller node options: 			https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-rhel-centos-or-fedora  
      
Install Ansible with:

   .. code-block:: sh
   
       $ sudo yum install ansible

To install a build from the ansible-power-aix Git repository:

   #. Obtain a local copy from the Git repository:

      .. code-block:: sh

         $ curl -L https://github.com/IBM/ansible-power-aix/blob/dev-collection/builds/ibm-power_aix-1.0.2.tar.gz\?raw\=true -o ibm-power_aix-1.0.2.tar.gz

   #. Install the local collection archive:

      .. code-block:: sh

          $ ansible-galaxy collection install ibm-power_aix-1.0.2.tar.gz

      In the output of collection installation, note the installation path to access the sample playbook:

      .. code-block:: sh

         Process install dependency map
         Starting collection install process
         Installing 'ibm.power_aix:1.0.0' to '/Users/user/.ansible/collections/ansible_collections/ibm/power_aix'


   .. note:: There is a playbook LINK NEEDED to auto install python and yum on your managed nodes, however for this guide we will perform this step manually.
	Installing yum on AIX:
	
		#. Make sure rpm.rte is installed at a level of 4.13.0.10 or higher.
			To check this run 'lslpp -la rpm.rte'.
			If not installed you can download rpm.rte from"https://ftp.software.ibm.com/aix/freeSoftware/aixtoolbox/INSTALLP/rpm.rte"
			Then install it "install –d. –acgXY rpm.rte"
			
		#. Download yum_bundle.tar from: https://public.dhe.ibm.com/aix/freeSoftware/aixtoolbox/ezinstall/ppc/ (it's recommended to Download the latest version)
			This bundle contains yum and all of it's dependency rpms.  Extract the yum packages from the yum_bundle.tar using tar (e.g. tar -xvf yum_bundle.tar).
			Install the each of the rpm packages using the rpm command (e.g. rpm -Uvh (packagename).rpm).
			
		#. yum conf file:
			yum.conf file will be installed under the path /opt/freeware/etc/yum.conf
			By default with yum-3.4.3-1 only ppc repository is enabled.with yum-3.4.3-2 or higher version, ppc, noarch & any one of the ppc-6.1/ppc-7.1/ppc-7.2 repository is enabled.
			If you faced ssl error while installing with yum, <baseurl> use http instead of https.


