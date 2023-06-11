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
