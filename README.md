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



