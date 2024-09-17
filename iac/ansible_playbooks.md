# Ansible Playbooks

## What is an Ansible Playbook?

An Ansible playbook is a file that contains a set of instructions that Ansible can use to automate tasks on remote hosts. Playbooks are written in YAML, a human-readable markup language.

A playbook typically consists of one or more plays, a collection of tasks run in sequence. Each task is a single instruction that Ansible can execute, such as installing a package, configuring a service, or copying a file.

By using Ansible playbooks, IT operations teams can automate infrastructure provisioning, configuration management, application deployment, and other operational tasks. Playbooks provide a concise and human-readable way to describe the desired automation workflows, making managing and scaling infrastructure configurations easier.

# Ansible Playbook Example

This playbook installs Apache, ensures the service is running, and sets up a simple HTML file on both Debian-based and RedHat-based systems.

```yaml
---
# Playbook to install and configure Apache web server

- name: Install and configure Apache web server
  hosts: webservers
  become: yes  # Use sudo to execute commands

  tasks:
    # Task 1: Install Apache on Debian systems
    - name: Install Apache on Debian systems
      apt:
        name: apache2
        state: present
      when: ansible_os_family == 'Debian'  # Ensure it runs only on Debian-based systems

    - name: Install Apache on RedHat systems
      yum:
        name: httpd
        state: present
      when: ansible_os_family == 'RedHat'  # Ensure it runs only on RedHat-based systems

    # Task 2: Ensure Apache service is started and enabled at boot
    - name: Ensure Apache is running and enabled at boot
      service:
        name: "{{ ansible_os_family == 'Debian' | ternary('apache2', 'httpd') }}"
        state: started
        enabled: yes

    # Task 3: Create a simple index.html file
    - name: Create a simple index.html
      copy:
        content: "<h1>Welcome to Ansible-managed Apache Server!</h1>"
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'

    # Task 4: Ensure the firewall is configured to allow HTTP traffic
    - name: Allow HTTP traffic through the firewall (Debian systems)
      ufw:
        rule: allow
        name: 'Apache Full'
        state: enabled
      when: ansible_os_family == 'Debian'

    - name: Open HTTP port on RedHat systems
      firewalld:
        service: http
        state: enabled
        permanent: yes
      when: ansible_os_family == 'RedHat'
```

## Full Explanation of the Playbook
### How to Write an Ansible Playbook

The above example is simple and straightforward, but Ansible playbooks can potentially get much larger and more complex. Whether you’re creating a short and sweet playbook or a sweeping epic, here is how you put one together.

Every playbook breaks down into the same standard sections:

1. Playbook Start
    - Playbooks always begin with three hyphens: ---. This signals the start of the YAML document.

2. Hosts
    - The hosts section defines the target machines where the playbook will run. These machines are defined in the Ansible inventory file and can be grouped into categories (e.g., webservers).

3. Variables (optional)
    - The vars section is optional and includes any variables that the playbook requires. You can define variables for reusability, configuration, and more.

4. Tasks
    - The tasks section lists all the tasks that the target machine must execute. Each task specifies the module to use and includes a name (a short description of what the task does).
    For example, using the apt module to install a package:

    ```yaml
    - name: Install Apache
    apt:
        name: apache2
        state: present
    ```

5. End
    - Most playbooks end with three periods (...) to signal the end of the YAML file, although this is not strictly required.

### How to Run an Ansible Playbook

- Playbooks are written in the YAML format and have a .yml file extension.
    - Run the playbook using the command:
  
    ```bash
    $ ansible-playbook <playbook.yml>
    ```

    - Check the playbook for syntax errors using:
  
    ```bash
    $ ansible-playbook <playbook.yml> --syntax-check
    ```

### Useful Pointers for Writing Playbooks

Here are some useful tips and best practices when working with Ansible playbooks:

1. Use Lists
    - Lists define multiple elements within variables or tasks. Use the - symbol to create a list in YAML. For example:

    ```yaml
    vars:
      packages:
        - apache2
        - git
        - curl
    ```

2. Include Whitespaces
    - Add blank lines between each task or block to improve readability and make the playbook easier to scan.

3. Name Your Tasks
    - While task naming is optional, it is highly recommended. Task names make it easier to understand what each task does. For example:

    ```yaml
    - name: Install Apache
      apt:
        name: apache2
        state: present
    ```

4. Specify State
    - Although the state parameter is optional, it’s a good idea to include it for clarity. The state could be present, absent, started, etc. For example:

    ```yaml
    - name: Ensure Apache is running
      service:
        name: apache2
        state: started
    ```

5. Use Comments
    - Use comments (starting with #) to explain what a task does. This helps others (and yourself) understand the playbook later on. For example:

    ```yaml

        # Ensure Apache is installed
        - name: Install Apache
          apt:
            name: apache2
            state: present
    ```

### Playbook Breakdown
**Playbook Start**: ---

The playbook begins with three hyphens (---), marking the start of a YAML document.

**Hosts Section**: hosts

The hosts section defines which group of machines the playbook will run on, based on the inventory file. In this example:

```yaml
hosts: webservers
```

**Tasks Section**: tasks

Each task in a playbook performs a specific action on the managed nodes. Tasks consist of:

- A name (optional, but recommended) that describes the task.
- A module that performs the actual action, such as apt for package installation or service for managing services.
- Parameters for the module, such as the name of the package and the state.

For example:

```yaml
- name: Install Apache
  apt:
    name: apache2
    state: present
```

**Playbook End**: ...

While not required, many playbooks end with three periods (...) to mark the end of the YAML document.

### Example Inventory File (inventory)

An inventory file lists the servers (or nodes) Ansible will manage. These servers are grouped under headings (like [webservers]), and the playbook can target specific groups.

```ini
[webservers]
web1.example.com
web2.example.com
```

In this case, the playbook targets `web1.example.com` and `web2.example.com` under the `webservers` group.

### Running the Playbook

1. Save the playbook as install_apache.yml.
2. Run the playbook using the following command:

    ```bash
    ansible-playbook install_apache.yml -i inventory
    ```

### Extending the Playbook

This playbook can be extended by adding more tasks, variables, and handlers. Here are a few suggestions:

- Add more modules: Use additional Ansible modules to manage databases, configure network interfaces, or install other software packages.
- Add roles: Organize your playbook into roles for reusability and better structure.
- Use handlers: Handlers are triggered by other tasks and are useful for restarting services after changes. For example:

```yaml
handlers:
  - name: Restart Apache
    service:
      name: apache2
      state: restarted
```

**Bibliography**:
- https://www.simplilearn.com/what-is-ansible-playbook-article