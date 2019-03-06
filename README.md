# CBA Challenge
===============

   1. Create a Security Group (on the existing VPC) which only allows access from the following:
	- Inbound - Your IP address (SSH, HTTP); Ansible IP address (SSH)
	- Outbound – HTTPS & HTTP to any IP address
   2. Launches a Linux instance from an AMI (select t2.micro for type of instance) and assign it with the Security Group that you created in (1).
	- You can select which flavor of Linux to launch
   3. Add a tag EnvName with the value “Test Environment”
   4. Deploy a Linux web-application (you can choose a web-application that you like)
   5. Present a web-page that is showing the IP address of the local IP address of machine on which it is running and have the web-app to listen on port 80
 

Given
-----
The **vpc_id** and the **subnet_id** are given. 
	
Assuming, the subnet_id is a public subnet, i.e. routable to the Internet. 

Not given
--------- 
You will need to create your own aws_keys.yml vault file with the appropriate credentials.

Requirements
------------

Ansible installed and an AWS account with appropriate credentials.

Also: **boto and boto3** must be installed as well, either system wide or by using a **virtualenv & pip**.
 
git is required to download the Ansible code.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Running the Playbook 
--------------------
	$ cd ~ 
	$ git clone https://github.com/MeirDukhan/cba.git
	$ cd ~/cba 

	$ Setup an ansible vault with file name: aws_keys.yml 
	ansible-vault create aws_keys.yml 
	echo 'my-ansible-vault-password' > vault-pass.txt && chmod 400 vault-pass.txt  


	$ ansible-playbook run.yml --vault-password-file vault-pass.txt --extra-vars 'my_ip=\<IP of my workstation>/32'

A log is available in ~/ansible.log 

Checking 
--------
	- The key pair created is cba-challenge-key and is stored into ~/.ssh/cba-challenge-key.pem

	Get the instance public IP 
	- aws ec2 describe-instances --filters Name=instance.group-name,Values='CBA_SG' | grep PublicIpAddress 

	- ssh -i ~/.ssh/cba-challenge-key.pem ec2-user@<IP Address> 
	- curl <IP Address> should give you the **private IP address** of the created instance 

	Filter on the security group description to check its setup: 
	- aws ec2 describe-security-groups --filters Name=description,Values='CBA Challenge security group'

IMPORTANT
---------
The EC2 instance created is an Amazon one, so login using the ec2-user@<IP address> 
	- **ssh -i ~/.ssh/cba-challenge-key.pem ec2-user@\<IP Address>**

Running a specific role
-----------------------
You can also run each role individualy. 

However the order of running matter: the EC2 instance must created last, after the key pair and the security croup have been created. 

### Key pair creation 

	ansible localhost -m include_role -a name=create_KP --vault-password-file vault-pass.txt

### Security Group creation. 
Note that creation of the security group requires the IP of your workstation as an extra parameter, to allow SSH and HTTP.

	ansible localhost -m include_role -a name=create_SG --vault-password-file vault-pass.txt --extra-vars "my_ip=<IP of my workstation>/32"

### EC2 instance creation

	ansible localhost -m include_role -a name=create_EC2_instance  --vault-password-file vault-pass.txt

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
