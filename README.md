# ansible

## On  master
##### Login as `root` user
```
sudo su -
```
Perform all the commands as root user unless otherwise specified

```
sudo apt-get update -y
sudo apt-get install python-minimal -y
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



