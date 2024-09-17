# What is Ansible?

Ansible is a software tool that enables cross-platform automation and orchestration at scale. Over the years, it has become the standard choice among enterprise automation solutions. 

Ansible is primarily designed for IT operators, administrators, and decision-makers, helping them achieve operational excellence across their entire infrastructure ecosystem.

Backed by RedHat and a loyal open-source community, it is considered an excellent option for configuration management, infrastructure provisioning, and application deployment. 

Its automation capabilities extend across hybrid clouds, on-prem infrastructure, and IoT, making it a versatile engine that greatly improves the efficiency and consistency of IT environments.

## How does Ansible work?

Ansible uses the concepts of **control nodes** and **managed nodes**. It connects from the control node (any machine with Ansible installed) to the managed nodes, sending commands and instructions to them.

The units of code that Ansible executes on the managed nodes are called **modules**. Each module is invoked by a **task**, and an ordered list of tasks together forms a **playbook**. Users write playbooks with tasks and modules to define the desired state of the system.

Managed machines are represented in a simple **inventory** file that groups nodes into different categories.

Ansible leverages a straightforward language, **YAML**, to define playbooks in a human-readable format that is easy to understand from day one.

Furthermore, Ansible doesn’t require the installation of any extra agents on the managed nodes, making it simple to start using. Typically, the only tools a user needs are a terminal to execute Ansible commands and a text editor to define configuration files.

## Benefits of using Ansible

- Free and open-source community project with a huge audience.
- Battle-tested over many years as the preferred tool for IT automation.
- Easy to start and use from day one, without the need for special coding skills.
- Simple deployment workflow without any extra agents.
- Includes sophisticated features for modularity and reusability, which become useful as users become more proficient.
- Extensive and comprehensive official documentation, complemented by a plethora of online resources produced by its community.

To sum up, Ansible is simple yet powerful, agentless, community-powered, predictable, and secure.

**Bibliography**:
- https://spacelift.io/blog/ansible-tutorial#what-is-ansible