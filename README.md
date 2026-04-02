we will have 1 master node and one agent node.
machines can be ec2 or vmware ubuntu

# Set up Master Node

Jenkins is a java based application.   
So first we need to install java on ubuntu machine. Run following commands to install java.
```
sudo apt update
sudo apt install openjdk-17-jre
```
Verify Java is Installed

```
java -version
```

Now, you can proceed with installing Jenkins

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

- EC2 > Instances > Click on <Instance-ID>
- In the bottom tabs -> Click on Security
- Security groups
- Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed `All traffic`).

 # Jenkins Architecture

 Usually jenkins has one master node and 1 and more worker nodes(agent) architecture. master node has jenkins installed on it. There are multiple developers, multiple project teams and multiple development teams. So jenkins get alot of load. To offload these things you should use jenkins master for only scheduling purpose. because all of the things canot run on single jenkins master. if everything runs on a single jenkins master then it will have conflicting packages.      
 let's say one team required java version 7 and other team required java version 8, someone requires python 2 some one requires python 3. it is technically not possible to run everything on one jenkins master. not good for the purpose of load and not good for the purpose of dependencies conflict.    
 so whats people do ,they create jenkins master and worker nodes. worker 1 should use by applications 1 -10. worker 2 should use by applications 11 - 20. worker 3 is for only windows applications, worker 4 only for specific team.  
 so devops engineers are responsible to categorize these machines.

 this architecture was good few years ago but with advancement of micreoservices, you have different type of applications.
 for example:   
 the worker node specific for windows application are just getting few request. so this machine always sitting idle. its a wastage of resources. so you have all these challanges with ec2 instances. to solve this problem we are going to adopt latest approach that is using jenkins as docker as agents. that means we try to run jenkins pipeline on dockers container. Docker containers are lightweight against vms. another thing is that for example if one team required nodejs 15 and another required node js 16 on vms it id difficult but on docker you can just go to dockerfile and change according to the requirments.  
 
 
