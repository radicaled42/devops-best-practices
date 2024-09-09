# Ansible Command Line

A Thread of 10 key Ansible commands and concepts all DevOps and Linux Administrators should focus on.

1) Check Ansible Version

Command:
ansible --version

Explanation:
Verify your Ansible installation and check version details.

2) Ping All Hosts

Command:
ansible all -m ping

Explanation:
Ping all hosts in your inventory to ensure they are reachable.

3) Run Command on Remote Hosts

Command:
ansible all -a "uptime"

Explanation:
Use ad-hoc commands to execute tasks like checking uptime on all remote hosts.

4) Target Specific Hosts

Command:
ansible webservers -m ping

Explanation:
Run commands for a specific group of hosts (e.g., webservers).

5) Execute Shell Commands

Command:
ansible all -m shell -a "ls -l /var/www/"

Explanation:
Run shell commands on remote hosts using the shell module.

6) Copy Files to Remote Hosts

Command:
ansible all -m copy -a "src=/local/file dest=/remote/path"

Explanation:
Transfer files from the control node to remote machines.

7) Gather Facts from Remote Hosts

Command:
ansible all -m setup

Explanation:
Collect detailed system facts (OS info, IP address) from remote hosts.

8) Run Playbook

Command:
ansible-playbook site.yml

Explanation:
Execute tasks defined in the site.yml playbook file.

9) Check Playbook Syntax

Command:
ansible-playbook site.yml --syntax-check

Explanation:
Ensure your playbook has no syntax errors before running it.

10) Simulate Playbook Changes

Command:
ansible-playbook site.yml --check

Explanation:
Run in "check" mode to preview changes without making them.

11) Limit Playbook to Specific Hosts

Command:
ansible-playbook site.yml --limit webservers

Explanation:
Run your playbook on a specific group of hosts only.

12) Use Privilege Escalation (sudo)

Command:
ansible all -b -m yum -a "name=nginx state=present"

Explanation:
Use the -b (become) flag to run tasks with elevated privileges.

13) Run Specific Tasks via Tags

Command:
ansible-playbook site.yml --tags "install"

Explanation:
Use tags to execute specific parts of the playbook, like installations.

14) Use Custom Inventory File

Command:
ansible-playbook -i /path/to/inventory site.yml

Explanation:
Specify a custom inventory file instead of using the default one.

15) Check Host Connectivity Before Running

Command:
ansible-playbook -i inventory.yml site.yml --list-hosts

Explanation:
List the hosts that the playbook will be applied to without executing it.

**Bibliography**:
- https://twitter.com/devops_tech/status/1833140071760830687