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

## An overview of the roles being used:

## References:

