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
###Change root password: passwd root
```/etc/ssh/sshd_config 
Change PasswordAuthentication Yes, PermitRootLogin yes
systemctl restart sshd, service sshd restart 
```
![image](https://github.com/raja4dev/ansible/assets/41365862/b0305056-b732-4fc0-93cf-b39897f59c0d)

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



