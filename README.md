# Ansible Practice
echo "*************************************************************************"
echo "This is a pratice of ansible"

## Features
-multiple virtual machines defined in one vagrantfile, "ansible-host" as ansible machine and "web1" as Remote machine
-a script for ssh-keygen
-a bootstrap script for password authentication and ansible installation

## Prerequistes
-vagrant
-vm

##Installation
```bash
echo "Step1: Clone this repository"
git clone https://github.com/PradishTamrkar/ansible-practice.git

echo "Step2: Go to he cloned directory"
cd ../ansible

echo "Step3: Start your vagrant machine"
Vagrant up

echo "Step4: Get inside the ansible-host machine"
vagrant ssh ansible-host

echo "step5: check if this machine is connected to web1"
ping web1.demo.com
echo "If this command doesnot give any results check back if any configurations have failed"

echo "step6: try to enter web1 machine form ansible-host"
ssh vagrant@web1

echo "Password will be asked for eneter web1.0 machine, this is becasue we have not copied the ssh-keygen values of ansible-host to the web1"

echo "For Passwordless Authentication"
echo "Step7: change the copied key_gen.sh mode to executable mode"
chmod +x key_gen.sh

echo "Step8:  Now execute the shell script"
./key_gen.sh

echo "Now again repeat Step6 and password mighjt not be asked"
echo "---------NOTE: YOU CAN SKIP THE SSH KEYGEN PROCESS, BUT YOU HAVE TO ENETER PASSWORD ANYTIME YOU WANT TO ACESS WEB1----------"
```

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
