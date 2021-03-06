**Ansible roles creating users and deploying apache web server**

This repository has been prepared for creating a number of users, allowing ssh key authorization, configuring ssh server and deploying apache server. There are basically 2 roles such as creating users and deploying apache that we can increase the number of roles in a standard way.

The following command is sufficient to setup users accound and deploy apache for a newly launched server. 
- **ansible-playbook playbook.yml -l web_server**
	- not only create listed users and setup ssh configuration but also install and deploy apache2. Simple website can be reached by http://server1.

These are the common other ansible commands useful.
- ansible-inventory --list -y
	- to list host and its variables in a tree
- ansible all -u root -m ping [-l test]
	- to check connection and basic configuration
- ansible-playbook create_user.yml -l web_server [--check]
	- to run a playbook for creating users. --check is for dry run.
- ansible-playbook create_user.yml -l web_server --tags "delete_users"
	- to run a specific task here. you need to add tag into your task as following.
* * *
## to create ansible user via ssh remotely
- put passwd and ssh_pubkey in content of the create_ansible_user.sh and run the following command.

`cat create_ansible_user.sh | ssh <username>@<remote_server_ip>`

```
#add service group/user
addgroup ansible
useradd ansible --create-home --shell /bin/bash --gid ansible
usermod -aG sudo ansible
echo "ansible:mypasswd" | sudo chpasswd
mkdir /home/ansible/.ssh
chmod 700 /home/ansible/.ssh
echo "<ssh_pubkey>" >> /home/ansible/.ssh/authorized_keys
chown ansible:ansible /home/ansible -R
echo "ansible ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/ansible
```
