---

title : "Ansible Inventory"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.3.2 </b> "

---

### Overview

**Ansible Inventory** is the component used to define the servers that Ansible will manage.

In the project, the Inventory is organized as follows:

```text
ansible/inventory/

├── group_vars/

│   └── managed_nodes.yml

├── host_vars/

│   ├── managed-01.yml

│   └── managed-02.yml

├── hosts.example.ini

└── hosts.ini
```

`hosts.ini` is the main Inventory file of the project, while `group_vars` and `host_vars` provide variables for groups or individual hosts.

![ASAU](/images/01/image_202.png)

### 1. hosts.ini File

The file:

```text
ansible/inventory/hosts.ini
```

is used to define the Managed Nodes.

The two Managed Nodes in the project are:

```text
managed-01

managed-02
```

Through the Inventory, Ansible knows which servers are within its management scope.

![ASAU](/images/01/image_203.png)

> **Note:** The `hosts.ini` content in the report should use the FINAL version of the project file. Do not reuse IP addresses or configurations from older versions if the project has been changed.

### 2. group_vars

The directory:

```text
inventory/group_vars/
```

contains variables that are applied to a group.

The project contains:

```text
managed_nodes.yml
```

The variables in this file can be shared among the Managed Nodes belonging to the same group.

![ASAU](/images/01/image_204.png)

### 3. host_vars

The directory:

```text
inventory/host_vars/
```

contains variables specific to individual hosts.

The project contains:

```text
host_vars/

├── managed-01.yml

└── managed-02.yml
```

This organization allows the project to separate shared variables from variables specific to each Managed Node.

### 4. hosts.example.ini

The project also contains:

```text
hosts.example.ini
```

This is an example file used as a reference for the Inventory structure.

Meanwhile:

```text
hosts.ini
```

is the Inventory file used for the actual environment.

### 5. How Ansible Uses the Inventory

The basic workflow is:

```text
                 Ansible

                    |

                    ↓

               ansible.cfg

                    |

                    ↓

                hosts.ini

                    |

          +---------+---------+

          |                   |

          ↓                   ↓

      managed-01          managed-02

          |                   |

          +---------+---------+

                    |

                    ↓

              Playbook / Task
```

When a Playbook specifies a group, Ansible executes the tasks on the hosts belonging to that group. Variables in `group_vars` and `host_vars` are used during the process.

### 6. Check the Inventory

The Inventory can be checked using:

```bash
ansible-inventory --list
```

Or the group and host structure can be displayed using:

```bash
ansible-inventory --graph
```

### Result

After completing the configuration, the project's Inventory structure is:

```text
Inventory

│

├── hosts.ini

│   ├── managed-01

│   └── managed-02

│

├── group_vars/

│   └── managed_nodes.yml

│

└── host_vars/

    ├── managed-01.yml

    └── managed-02.yml
```

The Inventory serves as the connection between the **Ansible Control Node** and the **Managed Nodes**, providing the host list and the variables required for the automation process.

The next section will explore **Ansible Playbooks** and how Playbooks use the Inventory to execute tasks on the Managed Nodes.