# Distributed systems

This tutorial will take you through how to set up a distributed system in jenkins but the concept is actually applicable in many techniques as it allows access through an public-key setup. Insatances where this is relatable are ansible servers, aws-instances, etc

# Text Direction : Create and Configure Jenkins Slave

## Switching Users To Jenkins
switch from default instance user to jenkins user e.g from ubuntu@<ip-adress> to jenkins@<ip-address>
```bash
sudo -iu jenkins
```

## Accessing Slaves From Master Server
There are several steps to follow

### Generate Public Key
Hit enter for all prompts
```bash
ssh-keygen -t rsa
```
### Create the same directory in the slave node
Use the following commands
```
ssh root@<slave-ip> mkdir -p .ssh
```

### Copy the public key from master to slave using

```
cat /var/lib/jenkins/.ssh/id_rsa.pub | ssh root@<slave-ip> 'cat >> .ssh/authorized_keys'
```

### Note Setup complete

__You can now ssh to slave node from master node without keys__

e.g

```
ssh root@<slave-ip>
```
This will work just fine

###  To exit
Exiting takes you back to the master node
```bash
exit
```

### Create bin directory

```bash 
mkdir bin
```
```bash
ls
```
```bash
cd bin
```
```bash
pwd
```

### Running on slave node:
 
```
wget http://<master_ip>:8080/jnlpJars/slave.jar

```

### Verify and Install Java:

```bash
java -version
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt install openjdk-8-jdk
```

### Start Slave Agent Command:

```bash

ssh root@<slave_ip> java -jar /root/bin/slave.jar

```