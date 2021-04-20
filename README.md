- ansible-inventory --list -y
	- to list host and its variables in a tree
- ansible all -u root -m ping [-l test]
	- to check connection and basic configuration
- ansible-playbook create_user.yml -l test [--check]
	- to run a playbook
- ansible-playbook create_user.yml -l test --tags "delete_users"
	- to run a specific task here. you need to add tag into your task as following.
