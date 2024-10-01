# Ansible Sample

```yaml
---
- name: Example Playbook
  hosts: all  # This will get the hosts from the inventory file
  become: yes  # This allows privilege escalation (sudo)

  tasks:
    - name: Hello World Task
      debug:
        msg: "Hello, World!"

    - name: Modify /etc/hosts file
      lineinfile:
        path: /etc/hosts
        line: "127.0.0.1   myhost.example.com"
        state: present
```
