# CBA Challenge
=========

   1. Create a Security Group (on the existing VPC) which only allows access from the following:
	- Inbound - Your IP address (SSH, HTTP); Ansible IP address (SSH)
	- Outbound – HTTPS & HTTP to any IP address
   2. Launches a Linux instance from an AMI (select t2.micro for type of instance) and assign it with the Security Group that you created in (1).
	- You can select which flavor of Linux to launch
   3. Add a tag EnvName with the value “Test Environment”
   4. Deploy a Linux web-application (you can choose a web-application that you like)
   5. Present a web-page that is showing the IP address of the local IP address of machine on which it is running and have the web-app to listen on port 80
 

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
$ ansible-playbook run.yml --vault-password-file vault-pass.txt --extra-vars "my_ip=<IP of my workstation>/32" 

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
