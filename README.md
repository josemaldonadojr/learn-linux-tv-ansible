# learn-linux-tv-ansible

## Notes

`ansible all --key-file ~/.ssh/ansible -i inventory -m ping`

* ansible: This is the command used to run Ansible tasks.
* all: This argument specifies that the command should be run on all hosts specified in the inventory file.
* --key-file ~/.ssh/ansible: This option specifies the path to the SSH private key file that should be used to authenticate the connection to the managed hosts.
* -i inventory: This option specifies the path to the inventory file, which is a list of hostnames or IP addresses of the managed hosts.
* -m ping: This option specifies the name of the module to be executed. In this case, the ping module is being used to test connectivity to the managed hosts.

If you set the *inventory* and *private_key_file* options in the *ansible.cfg* file, you can shorten the command to just `ansible all -m ping`, because the -I and --key-file options are not needed. The ansible command will use the default values specified in the configuration file instead.

`ansible all --list-hosts`

Lists all the hosts in the inventory file specified in the ansible.cfg configuration file.