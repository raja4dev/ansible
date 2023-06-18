# ansible

## On  master
##### Login as `root` user
```
sudo su -
```
Perform all the commands as root user unless otherwise specified

```
sudo apt-get update -y
sudo apt-get install python2-minimal -y
sudo apt-get install python3-pip python3 -y
sudo apt-get install software-properties-common -y
sudo apt-add-repository ppa:ansible/ansible -y
sudo apt-get update -y
sudo apt-get install ansible -y
which ansible
ansible --version

```


# Server/Worker node side changes
##### Copy the id-rsa.pub (from Ansible master) to authorized_keys (worker nodes)
```
vi authorized_keys

```
```
vi /etc/ansible/hosts

[web]
target-ip

:wq
```

###test the connection from ansible master to worker using below command
```
#ansible-master$ ssh root@<node-ip>

```
##### If you are still getting access issue follow the below steps to fix
```
###Change/add the below entries 
vi /etc/ssh/sshd_config 
 
PasswordAuthentication Yes
PermitRootLogin yes
```

###### After changing the file we need to save the file and restart systemctl using below command
```
systemctl restart sshd
```

###### Add the node IP/host entry /etc/ansible/hosts
```
vi /etc/ansible/hosts

[web]
<node1-ip>

[app]
<node2-ip>

......
etc
```

##### Ping Module to test the connection 
```
ansible all -m ping
```
#### Output 

```
10.10.0.3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    }, 
    "changed": false, 
    "ping": "pong"
}
```







### To create an Ansible role directory structure using Ansible Galaxy, you can use the ansible-galaxy command-line tool. Here's how you can do it:

##### Install Ansible Galaxy (if not already installed):
```
pip install ansible-galaxy
```

#### Create a new role with the desired name:
```
ansible-galaxy init myrole
```

This will create a directory named myrole with the required role structure.

##### The directory structure will look like this:
```
myrole/
  ├── defaults/
  │   └── main.yml
  ├── files/
  ├── handlers/
  │   └── main.yml
  ├── meta/
  │   └── main.yml
  ├── tasks/
  │   └── main.yml
  ├── templates/
  ├── tests/
  │   ├── inventory/
  │   └── test.yml
  └── vars/
      └── main.yml
```      
###### Here's a brief description of each directory:
```
defaults/: This directory is used to store default variables for the role.
files/: This directory is used to store files that will be copied to the target system.
handlers/: This directory is used to store handlers for the role.
meta/: This directory is used to store metadata for the role, such as dependencies and supported platforms.
tasks/: This directory is used to store the main tasks file for the role.
templates/: This directory is used to store template files that can be customized during deployment.
tests/: This directory is used for testing the role.
vars/: This directory is used to store variables specific to the role.
You can add your role-specific tasks, variables, handlers, and other files within these directories as needed.

Remember to adjust the role name (myrole in this example) to match the name of your desired role.

```


