# Notes on AWS
## General Topics
### What is Cloud
- Cloud computing refers to the utilisation of computational power or storage
over the internet
- This can be remote servers that run virtual machines, databases that store
your companies data for you
- Using cloud computing is often preferable to outright buying the necessary
hardware yourself as it is very expensive and requires maintenance
- The maintenance, security, and up front costs are all handled by the Cloud
providers, you simply pay for what you use
### What is AWS
- Amazon Web Servers is a widely used provider of Cloud Computing
- This service is flexible, allowing you to upscale or downscale your demands
as necessary
- They have regions and data centres all across the world, allowing for lower
latency
### What is EC2
- Elastic Compute Cloud
- Developers can use EC2 to create an Amazon Machine Image (AMI) to set up a
virtual machine that will run on Amazon's servers
- Data only remains on an EC2 while it's running
## Specific Topics
### What is a SG? How do you open a port to your IP, or to the world?
- Security Groups control who can see and access what, acting as a firewall to
incoming and outgoing traffic
- Can create your own SG's with specific rules, or use an existing group
- To open a port to your IP, create a "Custom TCP Rule", specify the desired port
in "Port Range", and then in the "Source" section choose the "My IP" option
- To open a port to the world, follow the same steps as opening it to your IP
but add 0.0.0.0/0 in the "Source" section
### Why should we not have port 22 open to all ips
- This is the port used to ssh into our virtual machine, if this isn't secured
then anyone can theoretically enter our virtual machine and commit malicious acts
### Where do you keep your ssh keys?
- All ssh keys are store together in the local machine's .ssh folder
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
#### Setting up the EC2 instance
- Start setting up an EC2 instance by clicking "Launch Instances"
- Select a free tier OS (we'll use Ubuntu 18.04) and click next
- Make sure the selected option is "free tier eligible", then click Next:
Configure Instance Details
- Make sure the Network is the default DevOpsStudents network, ensure that the
"Auto-assign Public IP" option is enabled, then click Next: Add Storage
- Click Next: Add Tags
- Click "Add tag", make the key "Name" and the value something that coincides
with your companies naming convention, and click Next: Configure Security Groups
- If you have an existing security group, select "Select an existing security
group" and choose the group from the dropdown. If not, you can create one by
adding rules as needed. For this, you'll need a HTTP rule, an SSH rule, and a
custom TCP rule set to port 3000, all with the source of your IP. Click Review
and Launch
- Make sure the configuration is correct and click Launch
- Choose an existing key pair or create a new one. If you create a new one, you
should move the downloaded key to your .ssh folder
- Click launch instance and we're live!
#### Moving the files over
- `Cd` to your .ssh folder and run the following command, where you will replace
the <key-name> with whatever your key is called (it should end in .pem) and
<public-ip> with the EC2's public ipv4 address
```bash
ssh -i <key_name> ubuntu@<public_ip>
```
- When prompted to continue connecting, type yes and we should be in the
virtual machine now!
- Open up another terminal and cd into the project directory containing the app
 folder
- Run the following command where the <destination_path> is where you want the
folder to be located within your virtual machine
```bash
scp -i <path_to_key>/<key_name> -r <folder> ubuntu@<public_ip>:<destination_path>
```
`scp -i ~/.ssh/eng74-jamie-aws-key.pem -r app ubuntu@34.247.160.37:~/app`
#### Setting up the virtual environment to run the app
- Manually go through all of the steps outlined in the provision.sh file for
the app, but replace the ip in the reverse-proxy.conf file to the public ipv4
address for the EC2 instance
- Once you finish the rest of the steps in the provision file and npm start, it
should work on port 3000!
### Pictures of app running
- Port 3000

- Port 80
