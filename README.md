# learn-linux-tv-ansible

## Notes

`ansible all --key-file ~/.ssh/ansible -i inventory -m ping`

* ansible: This is the command used to run Ansible tasks.
* all: This argument specifies that the command should be run on all hosts specified in the inventory file.
* --key-file ~/.ssh/ansible: This option specifies the path to the SSH private key file that should be used to authenticate the connection to the managed hosts.
* -i inventory: This option specifies the path to the inventory file, which is a list of hostnames or IP addresses of the managed hosts.
* -m ping: This option specifies the name of the module to be executed. In this case, the ping module is being used to test connectivity to the managed hosts.