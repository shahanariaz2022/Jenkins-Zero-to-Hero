# Jenkins Master and Agent on Same Machine
how to set up one machine architecture where jenkins and agents both are on same machine?

let's setup the machine

1. Create AWS EC2 machine
2. Install java
3. Install jenkins
4. As we are using Containers as agents install Docker
   ##Docker Agent Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
5. ### Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
