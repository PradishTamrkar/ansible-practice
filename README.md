# Ansible Practice
******************************************************************************************************************************
This is a pratice of ansible

## Features
-multiple virtual machines defined in one vagrantfile, "ansible-host" as ansible machine and "web1" as Remote machine
-a script for ssh-keygen
-a bootstrap script for password authentication and ansible installation

## Prerequistes
-vagrant
-vm

##Installation
```bash
Step1: Clone this repository
git clone https://github.com/PradishTamrkar/ansible-practice.git
```
```bash
Step2: Go to he cloned directory
cd ../ansible
```
```bash
Step3: Start your vagrant machine
Vagrant up
```
```bash
Step4: Get inside the ansible-host machine
vagrant ssh ansible-host
```
```bash
Step5: check if this machine is connected to web1
ping web1.demo.com
If this command doesnot give any results check back if any configurations have failed
```
```bash
Step6: try to enter web1 machine form ansible-host
ssh vagrant@web1
```
Password will be asked for eneter web1.0 machine, this is becasue we have not copied the ssh-keygen values of ansible-host to the web1

For Passwordless Authentication
```bash
Step7: change the copied key_gen.sh mode to executable mode
chmod +x key_gen.sh
```
```bash
Step8:  Now execute the shell script
./key_gen.sh
Now again repeat Step6 and password mighjt not be asked
```
```bash
Step9: Now, create a directory for example ansible-proj and get inside the directory
mkdir ansible-proj 
cd ansible-proj
```
```bash
Step10: Create an inventory file where we will work
vim Inventory
```
```bash
Step11: Inside the inventory file add:
web1 ansible_host=192.168.56.15 ansible_user=vagrant
```
---NOTE: since ssh keygen is used so we do not need to add ansible_password---
else we have to write the following inside inventory file
```bash
web1 ansible_host=192.168.56.15 ansible_user=vagrant ansible_password=vagrant(or any other password that you have kept manually)
```
---------NOTE: YOU CAN SKIP THE SSH KEYGEN PROCESS, BUT YOU HAVE TO ENETER PASSWORD ANYTIME YOU WANT TO ACESS WEB1----------
```bash
Step12: Now to using the inventory to install apache2 on another machine
ansible -i inventory -m apt -a "name=apache2 state=present" web1 --become
```
"-- become" acts like sudo giving the user permission to act as root
## Debugging Issues
If password authentication is not working:
```bash
sudo grep -r PasswordAuthentication /etc/ssh/
sudo sshd -T | grep authentication
```
Ensure `PasswordAuthentication yes` is set correctly and restart SSH:
```bash
sudo systemctl restart sshd
```
