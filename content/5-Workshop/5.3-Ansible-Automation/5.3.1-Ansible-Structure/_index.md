---

title : "Ansible Structure"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.3.1 </b> "

---

### Overview

In the project, **Ansible** is responsible for managing and automating configuration on the Managed Nodes.

All Ansible components are organized in the following directory:

```text
ansible/
```

The main structure consists of **Inventory, Playbooks, Policies, Roles, and the `ansible.cfg` configuration file**.

### 1. Directory Structure

```text
ansible/

├── inventory/

│   ├── group_vars/

│   │   └── managed_nodes.yml

│   ├── host_vars/

│   │   ├── managed-01.yml

│   │   └── managed-02.yml

│   ├── hosts.example.ini

│   └── hosts.ini

│

├── playbooks/

│   ├── common.yml

│   ├── facts.yml

│   ├── firewall.yml

│   ├── security_audit.yml

│   ├── security_baseline.yml

│   ├── security_collect.yml

│   ├── ssh_hardening.yml

│   ├── system_info.yml

│   └── variables_demo.yml

│

├── policies/

│   └── security_policy.yml

│

├── roles/

│   ├── common/

│   ├── firewall/

│   └── ssh_hardening/

│

└── ansible.cfg
```

![ASAU](/images/01/image_197.png)

### 2. Inventory

The `inventory/` directory contains information about the Managed Nodes managed by Ansible.

```text
inventory/

├── group_vars/

│   └── managed_nodes.yml

├── host_vars/

│   ├── managed-01.yml

│   └── managed-02.yml

├── hosts.example.ini

└── hosts.ini
```

Where:

- `hosts.ini` contains the list of Managed Nodes.
- `group_vars/` contains variables applied to a group of hosts.
- `host_vars/` contains variables specific to individual hosts.
- `hosts.example.ini` is an example file.

The Inventory allows Ansible to determine **which servers need to be managed** and their corresponding variables.

### 3. Playbooks

The `playbooks/` directory contains Playbooks that perform different automation tasks.

```text
playbooks/

├── common.yml

├── facts.yml

├── firewall.yml

├── security_audit.yml

├── security_baseline.yml

├── security_collect.yml

├── ssh_hardening.yml

├── system_info.yml

└── variables_demo.yml
```

The Playbooks are organized by functions such as system information collection, firewall configuration, security audit, security baseline, security collection, SSH hardening, and variables.

A Playbook is where **the tasks that Ansible will perform on the Managed Nodes are defined**.

### 4. Policies

The `policies/` directory contains:

```text
policies/

└── security_policy.yml
```

The `security_policy.yml` file stores criteria and configurations related to the security policy of the project.

### 5. Roles

The `roles/` directory organizes reusable automation components:

```text
roles/

├── common/

├── firewall/

└── ssh_hardening/
```

The main Roles are:

- `common`: Common configurations.
- `firewall`: Firewall configuration.
- `ssh_hardening`: SSH Hardening configuration.

Roles help divide automation into clearly structured and manageable components.

### 6. Ansible Configuration

The file:

```text
ansible.cfg
```

is the main configuration file for Ansible.

This file defines settings used when Ansible executes, such as the Inventory and options related to the execution process.

![ASAU](/images/01/image_200.png)

### 7. Overall Workflow

```text
                 ansible.cfg

                      |

                      ↓

                  Inventory

                      |

          +-----------+-----------+

          |                       |

      group_vars               host_vars

          |                       |

          +-----------+-----------+

                      |

                      ↓

                   Playbook

                      |

                      ↓

                     Role

                      |

                      ↓

                Managed Nodes
```

When a Playbook is executed, Ansible uses the configuration in `ansible.cfg`, retrieves the host list from the Inventory, combines the variables, and executes the tasks on the Managed Nodes.

### Result

```text
Ansible

│

├── Inventory   → Defines Managed Nodes

├── Variables   → Provides configuration

├── Playbooks   → Defines automation tasks

├── Policies    → Defines security policies

├── Roles       → Organizes automation components

└── ansible.cfg → Ansible configuration
```

This structure provides the foundation for the following sections, where we will explore the **Inventory, Variables, Playbooks, and Roles** of the project in greater detail.