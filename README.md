#### ansible_basics
  * Ansible is flexible and easy to set up as far as configuration deployment management system go
  * Ansible doesn't require any server component. There is no daemon that needs to be running. It does all of its work over SSH.
  * Where-ever you are going to run your playbooks from, you need to have ansible installed. But your resulting nodes which you may be running commands on do not need to have ansible installed (they just need to be accessible with the help of SSH). 
  
#### Commands
  * sudo su --first go to root
#### How do I enable the EPEL repository for my Amazon EC2 instance running CentOS, RHEL, or Amazon Linux?
  * https://aws.amazon.com/premiumsupport/knowledge-center/ec2-enable-epel/
#### update local caches
  * yum update 
#### Once will intall epel-release and update caches, we are going to need git  because git is the very common components for promoting builds. You need to have python, development and libraries, python pip -- which is the module manager for python, open ssl and ansible. 
  * yum install git python python-devel python-pip openssl ansible
#### check if ansible is installed
  * ansible --version
#### Edit ansible config
  * vim /etc/ansible/ansible.cfg
    * umcomment inventory and sudo_user
#### Note: when we run ansible commands or ansible playbooks, we run them against nodes. Nodes are identified by their name. They are listed in /etc/ansible host
  * cd /etc/ansible 
  * cat hosts
#### Set up a very basic host file
  * mv hosts hosts.original 
  * vim hosts
#### Set up 3 groups, you can set up as many groups as you want. 
     [local]
     localhost
     
     [centos]
     rbn.mylabserver.com
     
     [ubuntu]
     rbn1.mylabserver.com
#### On 1 group I am identifying myself as a node called localhost. Typically, you are going to run ansible as a not privilaged user. But that non-previlaged user should have sudo rights
  * adduser ansible 
  * passwd ansible
#### vi sudo
  * just below root ALL=(ALL) ALL
  * add ansible ALL=(ALL) NOPASSWD: ALL 
#### GO to centos machine
  * do adduser ansible 
  * passwd ansible
  * visudo and same process as on top
#### Go to ubuntu machine 
  * same process repeated 
#### So, on our system we can do sudo apt-get update 
#### Come back to localhost
#### Note: Since we operate over ssh and and since we will not be passing in a password, we don't have to add a password when we run a playbook either. This is because most of the time when you develop a playbook, you will be running in a cron jobs or jenkins jobs
#### In that case, we should set up ssh key exchange. So,
  * su ansible -
  * ssh-keygen
  * ssh-copy-id ansible@rbn.mylabserver.com
#### Once that's done, you can ssh to rbn.mylabserver.com
#### Same thing with ubuntu
  * ssh-copy-id ansible@rbn1.mylabserver.com
  * now you are able to ssh rbn1.mylabserver.com
#### ssh-copy-id localhost
  * now you can do ssh localhost to have connection without having to login
## You are now ready to use ansible environment
