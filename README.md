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
