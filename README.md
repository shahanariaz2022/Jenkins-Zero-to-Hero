we will have 1 master node and one agent node.
machines can be ec2 or vmware ubuntu

# Set up Master Node

Jenkins is a java based application. So first we need to install java on ubuntu machine.
```
sudo apt update
sudo apt install openjdk-17-jre
```
Verify Java is Installed

```
java -version
```

Now, you can proceed with installing Jenkins
