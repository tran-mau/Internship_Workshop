---

title : "Ansible Playbooks"

date : "`r Sys.Date()`"

weight : 3

chapter : false

pre : " <b> 5.3.3 </b> "

---

### Overview

**Ansible Playbook** is the component that describes the tasks Ansible will perform on the Managed Nodes.

In the project, Playbooks are organized in the following directory:

```text
ansible/playbooks/
```

The current structure includes:

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

Each Playbook is responsible for a specific group of functions in the management and security process of the Managed Nodes.

![ASAU](/images/01/image_205.png)

### 1. common.yml

`common.yml` contains common configuration tasks for the Managed Nodes.

This Playbook is used when performing basic configurations or settings that are shared across multiple servers.

![ASAU](/images/01/image_206.png)

### 2. facts.yml

`facts.yml` is used to collect **Ansible Facts** from the Managed Nodes.

Facts provide information about the servers, such as the operating system, hostname, network addresses, memory, and other system information.

![ASAU](/images/01/image_207.png)

### 3. system_info.yml

`system_info.yml` is used to collect or display system information from the Managed Nodes.

This Playbook helps check the basic status of the servers before or during the automation process.

![ASAU](/images/01/image_208.png)

### 4. firewall.yml

`firewall.yml` is related to configuring the **Firewall** on the Managed Nodes.

This Playbook works together with the `firewall` Role to apply firewall configurations according to the project's design.

![ASAU](/images/01/image_209.png)

### 5. ssh_hardening.yml

`ssh_hardening.yml` performs tasks related to **SSH Hardening**.

This Playbook works together with the `ssh_hardening` Role to apply security configurations to the SSH service on the Managed Nodes.

![ASAU](/images/01/image_210.png)

### 6. security_audit.yml

`security_audit.yml` is used to perform a **Security Audit** on the Managed Nodes.

Its purpose is to check the security configuration status and identify settings that do not meet the project's requirements.

![ASAU](/images/01/image_211.png)

### 7. security_baseline.yml

`security_baseline.yml` is related to establishing or checking the **Security Baseline**.

The Security Baseline provides a basic security configuration state that the Managed Nodes should meet.

![ASAU](/images/01/image_212.png)

### 8. security_collect.yml

`security_collect.yml` is used to collect security status information from the Managed Nodes.

The collected data can be used by the Security Engine components in the Python section.

![ASAU](/images/01/image_213.png)

### 9. variables_demo.yml

`variables_demo.yml` is used to demonstrate or test how Ansible uses **Variables** in a Playbook.

This Playbook is directly related to the mechanism for retrieving values from the Inventory, `group_vars`, and `host_vars`.

![ASAU](/images/01/image_214.png)

### 10. Relationship Between Playbooks and Ansible Components

A Playbook does not operate independently but uses other Ansible components:

```text
                 ansible.cfg

                      |

                      ↓

                  Inventory

             +--------+--------+

             |                 |

         group_vars        host_vars

             |                 |

             +--------+--------+

                      |

                      ↓

                   Playbook

             +-------+-------+

             |       |       |

             ↓       ↓       ↓

          common  firewall  ssh_hardening

             |       |       |

             +-------+-------+

                      |

                      ↓

                Managed Nodes
```

When a Playbook is executed, Ansible identifies the target hosts from the Inventory, retrieves the corresponding variables, and executes the tasks described in the Playbook or Role.

### 11. Executing a Playbook

A Playbook can be executed using the following command:

```bash
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/<playbook>.yml
```

Where:

- `ansible-playbook` is used to execute the Playbook.
- `-i` specifies the Inventory.
- `hosts.ini` identifies the Managed Nodes.
- `<playbook>.yml` is the Playbook to be executed.

For example, when running a security checking or configuration task, the command points to the corresponding Playbook in the `ansible/playbooks/` directory.

### 12. Workflow

The general workflow is:

```text
Ansible Control Node

        |

        ↓

    ansible.cfg

        |

        ↓

    Inventory

        |

        ↓

    Playbook

        |

        ↓

   Tasks / Roles

        |

        ↓

 Managed Nodes
```

The Playbook plays the central role in describing **what Ansible needs to do**, while the Inventory determines **which machines the tasks are performed on**, and Variables provide **the required configuration values**.

### Result

After building the Playbooks, the project can organize automation tasks by function:

```text
Ansible Playbooks

│

├── System Management

│   ├── common.yml

│   ├── facts.yml

│   └── system_info.yml

│

├── Security

│   ├── firewall.yml

│   ├── ssh_hardening.yml

│   ├── security_audit.yml

│   ├── security_baseline.yml

│   └── security_collect.yml

│

└── Variables

    └── variables_demo.yml
```

This organization helps separate automation tasks by function and provides a foundation for using **Ansible Roles** in the next section.