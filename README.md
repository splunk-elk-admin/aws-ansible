# Ansible for AWS EC2 instance deployment 
## Prerequisites
Latest version of ansible on a linux distro 
AWS credentials for programmatic access with appropriate privileges 

## Pre Work 
### AWS Specific 
Create .aws folder in your home directory 
```
$ mkdir ~/.aws 
```

Create a config file to specify the default AWS region to use 
```
$ cat ~/.aws/config 
[default]
region = us-west-1
$
```
Create a credentials file to store AWS crednetials 
```
$ cat ~/.aws/credentials 
[default]
AWS_ACCESS_KEY_ID=<Your access key goes here>
AWS_SECRET_ACCESS_KEY=<Your secret access key goes here>
$ 
```  
  
### Ansible Specific 
Create ansible.cfg in the directory where your playbook will reside 
```
$ cat ansible.cfg 
[defaults]
inventory = ./hosts 
host_key_checking = False
$ 
```

Create a hosts file to be used as inventory 
```
$ cat hosts 
[local]
localhost
$
```

Create a files folder to store the index.html 
```
$ cat files/index.html 
Ping Pong
$ 
```
## Playbook 
deploy-http.yml does the following 
- Creates a new EC2 key
- Save private key in the local folder 
- Creates security group 
- Launches new ec2 instance 
- Adds the new instance to host group
- Tags the instance 
- Waits for ssh to come up 
- Installs http
- Updates http content
- Starts and enables http service 

## Deployment 
```
$ ansible-playbook deploy-http.yml  
```
