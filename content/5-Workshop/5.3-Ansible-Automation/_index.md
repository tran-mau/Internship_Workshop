---

title : "Ansible Automation"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.3 </b> "

---

### Overview

In the project, **Ansible Automation** is used to automate the management and configuration of the Managed Nodes. Instead of manually performing tasks on each server, Ansible allows configurations and administrative tasks to be centralized through Inventory, Playbooks, Roles, and Security Policies.

The main Ansible components used in the project include:

```text
Ansible Automation

│

├── Inventory

│   └── Defines the Managed Nodes

│

├── Playbooks

│   └── Defines automation tasks

│

├── Roles

│   └── Organizes configuration functions

│

├── Policies

│   └── Defines security requirements

│

└── ansible.cfg

    └── Ansible environment configuration
```

### List of Practical Lessons

+ [5.3.1 Ansible Architecture]({{< relref "5.3.1-Ansible-Structure">}})

+ [5.3.2 Ansible Inventory]({{< relref "5.3.2-Ansible-Inventory">}})

+ [5.3.3 Ansible Playbooks]({{< relref "5.3.3-Playbooks">}})

+ [5.3.4 Role Policies]({{< relref "5.3.4-Role-Policies">}})