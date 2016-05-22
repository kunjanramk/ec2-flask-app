# ec2-flask-app
This will automatically launch an ec2 instance, install nginx, flask &amp; other requirements, pull latest flask application code and deploy it

## Pre-requisites:
### Packages:
    ansible
    python
    python-boto # For AWS EC2 provisioning
    git
###  AWS Requirements:
    AWS account
    Gather the following information for this project
      instance_type:
        Type of EC2 instance, default we are using t2.micro
      image:
        AMI image for the EC2 instance, default we are using ami-25c00c46 which is ubuntu 14.02 free tier eligible
      region:
        AWS region where you need to install the application, default we have selected Singapore which is ap-southeast-1
      keypair:
        SSH keys for accessing EC2 instance, here we need to use an existing keypair. You can also customize the playbook to add code for creating new keypair and use the same for application deployment.
      aws keys:
        You need to create an IAM user with appropriate permissions to create EC2 instances. Download the access and secret keys for the user. We need to pass these keys to create EC2 instance. There are different ways 
## Synopsis:
     ansible-playbook -i ec2-inv site.yml --private-key path/to/private-key
       This private key will be used for ssh to ec2 instance by ansible
## An overview of the roles being used:
   1. init:
      This will add nginx repositories to apt-get sources and does apt-get update
      and apt-get upgrade. This will also install are required packages like python,
      build-essential, python-dev, python-virtualenv, git, etc..
   2. nginx-install:
      This will just install nginx package on the instance
   3. venv:
      In this role, we create a folder for the application. Create and activate
      virtual environment and install flask in it. It will also install uwsgi, which
      is a method for deploying python or flask applications with nginx server
   4. app-repo:
      This will be used to pull your application code from git repo and store
      it locally.
   5. nginx-conf:
      Here we remove nginx default configuration and create new configuration
      for our application and link appropriately. At the end we restart nginx
      service to pick new configurations
   6. uwsgi:
      This will configure uwsgi for our application. We will also configure uwsgi
      emperor to automatically spawn uwsgi processes to execute our application.

## Useful Resources:
1. [Ansible Introduction] (http://docs.ansible.com/ansible/intro.html)
2. [Playbooks Tutorial] (http://docs.ansible.com/ansible/playbooks.html)
3. [BOTO ec2_group Module] (http://docs.ansible.com/ansible/ec2_group_module.html)
4. [BOTO ec2 Module] (http://docs.ansible.com/ansible/ec2_module.html)
5. [nginx wiki] (https://www.nginx.com/resources/wiki/)
6. [Flask Quickstart] (http://flask.pocoo.org/docs/0.10/quickstart/)
7. [Flask deployment with nginx and uwsgi] (http://flask.pocoo.org/docs/0.10/deploying/uwsgi/)
8. [uWSGI Quickstart] (https://uwsgi-docs.readthedocs.io/en/latest/WSGIquickstart.html)

