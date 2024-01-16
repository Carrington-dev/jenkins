# Distributed systems

## Switching Users To Jenkins

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
root@<slave-ip>
```
This will work just fine