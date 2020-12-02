# Notes on AWS
## General Topics
### What is Cloud
### What is AWS
### What is EC2
## Specific Topics
### What is a SG? How do you open a port to your IP, or to the world?
- Security groups control who can see what
### Why should we not have port 22 open to all ips
### Where do you keep your ssh keys?
- Together in local machine's .ssh folder
### How to ssh into a remote server
- General command is
```bash
ssh -i <path_to_key>/<key_name> <user>@<public_ip>
```
- An example for my machine would be
```bash
ssh -i eng74-jamie-aws-key.pem ubuntu@3.251.91.166
```
### How to send in one file to a remote server
- General command is
```bash
scp -i <path_to_key>/<key_name> <source_path>/<file_name> <user>@<public_ip>:<destination_path>/<file_name>
````
- A specific example for copying in a provision file for the sparta nodejs app
would be
```bash
scp -i ~/.ssh/eng74-jamie-aws-key.pem provision.sh ubuntu@3.251.91.166:~/provision.sh
```
### How to send in multiple files to a remote server
- General command is
```bash
scp -i <path_to_key>/<key_name> -r <folder> <user>@<public_ip>:<destination_path>
```
- A specific example for copying in the app code for the sparta nodejs app would
be
```bash
scp -i ~/.ssh/eng74-jamie-aws-key.pem -r app ubuntu@3.251.91.166:~/app
```
### General outline of how to get the app running on the server in Ireland
### Pictures of app running
- Port 3000

- Port 80
