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
5. docker typically run on a deamon process that asingle process or single source of truth for docker. this deamon process is bu default not accessible to other users. so i installed docker as root user so only root user can access docker deamon. so i have to grant access to this deamon so to do that what i will do, basically jenkins comes with the user called jenkins. so i will grant the permission to jenkins as well as ubuntu user.
   ### Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```
after this switch to jenkins user

```
su - jenkins
```
jenkins user is by default created when you install jenkins.

now run this command

```
docker run hello-world
```
you will get error
```
docker: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied

Run 'docker run --help' for more information
```
solution to the error
logout from jenkins and grant permission again and then again login and run the command it will work.
```
logout
sudo su - 
usermod -aG docker jenkins
su - jenkins
docker run hello-world
```
