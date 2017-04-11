# Setting up a remote server using Ubuntu

Create an instance on your VPS of choice, Amazon Lightsail is what I'll be using.

Lightsail comes with an in-browser ssh interface, so start by logging in with that.

## Getting started

First, let's update by using ``` sudo apt-get update``` and ```sudo apt-get upgrade```

Create a new user named grader ```sudo adduser grader```

### Give the user sudo access 

```
sudo touch etc/sudoers.d/grader
sudo nano etc/sudoers.d/grader
```
This creates a file and then brings you to an editing screen. Here, you will write: 
```
grader ALL=(ALL) NOPASSWD:ALL
```

### Enforcing SSH as only authentication method

```sudo nano etc/ssh/sshd_config```

Find the line ```Password Authentication yes``` change the yes to no and save the file.

```sudo service ssh restart```

### Create SSH keys

On your local machine run ```ssh key-gen``` it will then prompt you for a location and filename. Open that file and copy the entire contents. 

In your remote command line, log in to your grader user ```sudo su - grader```

Create your file for key and paste the key into using:

```
mkdir .ssh
touch .ssh/authorized_keys
nano .ssh/authorized_keys
```
Paste the ssh key into that file and save it.

Next, change the file permissions using:
```
sudo chmod 700 .ssh
sudo chmod 644 .ssh/authorized_keys
```
