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

* Lists all the hosts in the inventory file specified in the ansible.cfg configuration file.

`ansible all -m gather_facts`

* Gathers information about managed hosts

`ansible all -m gather_facts --limit 10.211.55.3`

* --limit: Option that can be used with the ansible command to specify a subset of hosts to run the command on.

### Running elevated ad-hoc Commands

`ansible all -m apt -a update_cache=true --become --ask-become-pass`

* The command runs the apt module with the update_cache=true argument on all of the hosts specified in the Ansible inventory file.
* The --become flag indicates that the task should be run with escalated privileges.
* The --ask-become-pass flag prompts the user to enter the password for the privilege escalation method (e.g., sudo) when running the command.
* The apt module will update the package cache on the target host(s), which is a local repository of package files used to speed up the installation of new packages.

<img width="427" alt="image" src="https://user-images.githubusercontent.com/47704702/208181960-cdf08c55-4e47-42f0-8015-3b4832ab16cb.png">

`ansible all -m apt -a name=vim-nox --become --ask-become-pass`

* Install a package via the apt module

`ansible all -m apt -a "name=linux-headers-arm64 state=latest" --become --ask-become-pass`

* Install a package via the apt module, and also make sure it’s the latest version available

`ansible all -m apt -a "upgrade=dist" --become --ask-become-pass`

* Upgrade all the package updates that are available

### Playbook

A playbook is YAML file that describes a set of tasks that need to be executed on a remote host or a group of hosts. It is used to automate and manage the configuration of a system or a set of systems in an organized and easy-to-use way.

A playbook consists of a list of one or more plays, and each play specifies a set of tasks that are executed on a particular host or group of hosts. Each task is a simple action, such as installing a package or copying a file.

> playbook.yml
```
- name: Update db servers
  hosts: all

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.apt:
      name: postgresql
      state: latest
  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started
```

`ansible-playbook playbook.yml  --become --ask-become-pass`

* Running a playbook