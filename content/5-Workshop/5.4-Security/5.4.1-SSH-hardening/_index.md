---

title : "SSH Hardening"

date : "`r Sys.Date()`"

weight : 1

chapter : false

pre : " <b> 5.4.1 </b> "

---

### Overview

After completing the Ansible Automation section and establishing SSH connectivity, the project moves to the **Security** section.

SSH Hardening is one of the security functions implemented using Ansible. The objective of this section is to apply security configurations to the SSH service on the Managed Nodes.

In this project, SSH Hardening is organized through:

~~~text
ansible/

├── playbooks/
│   └── ssh_hardening.yml
│
└── roles/
    └── ssh_hardening/
        ├── defaults/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        └── tasks/
            └── main.yml
~~~

### 1. `ssh_hardening.yml` Playbook

File:

~~~text
ansible/playbooks/ssh_hardening.yml
~~~

acts as the orchestrator for the SSH Hardening process.

The Playbook identifies the Managed Nodes as the target hosts and calls the `ssh_hardening` Role.

Processing flow:

~~~text
ssh_hardening.yml

        |

        ↓

ssh_hardening Role

        |

        ↓

SSH configuration

        |

        ↓

Managed Nodes
~~~

![ASAU](/images/01/image_223.png)

### 2. `ssh_hardening` Role

Role:

~~~text
ansible/roles/ssh_hardening/
~~~

is used to organize tasks related to SSH Hardening.

The Role is divided into the following components:

~~~text
ssh_hardening/

├── defaults/
│   └── main.yml
│
├── handlers/
│   └── main.yml
│
└── tasks/
    └── main.yml
~~~

This organization separates default configuration, execution tasks, and handlers into different components.

### 3. Tasks

File:

~~~text
roles/ssh_hardening/tasks/main.yml
~~~

contains the tasks that perform SSH Hardening.

When the Role is called from the Playbook, Ansible executes the tasks in this file on the Managed Nodes.

![ASAU](/images/01/image_224.png)

**How it works:**

~~~text
Playbook

   ↓

ssh_hardening Role

   ↓

tasks/main.yml

   ↓

Managed Node

   ↓

SSH configuration changed
~~~

### 4. Defaults

File:

~~~text
roles/ssh_hardening/defaults/main.yml
~~~

contains the default values used by the Role.

Placing configurable values in `defaults` separates configuration parameters from the task implementation.

![ASAU](/images/01/image_225.png)

### 5. Handlers

File:

~~~text
roles/ssh_hardening/handlers/main.yml
~~~

contains Handlers that are used when a change to the SSH configuration requires an additional action.

Basic flow:

~~~text
Task

  |

  | configuration changed

  ↓

notify

  |

  ↓

Handler
~~~

![ASAU](/images/01/image_226.png)

### 6. Overall Workflow

SSH Hardening is implemented according to the following model:

~~~text
                Automation Server

                        |

                      Ansible

                        |

               ssh_hardening.yml

                        |

                ssh_hardening

                     Role

                        |

              +---------+---------+
              |                   |
              ↓                   ↓

       Managed-Node-01     Managed-Node-02

              |                   |
              ↓                   ↓

        SSH Hardening       SSH Hardening
~~~

Ansible obtains the target hosts from the Inventory, calls the `ssh_hardening.yml` Playbook, and then the `ssh_hardening` Role performs the required tasks on the Managed Nodes.

### 7. Verification

After applying SSH Hardening, the configuration should be checked on the Managed Nodes to confirm that the required security settings have been successfully applied.

![ASAU](/images/01/image_227.png)

### Result

After completing the implementation, SSH Hardening is organized as follows:

~~~text
ssh_hardening.yml

        ↓

ssh_hardening Role

        ↓

tasks / defaults / handlers

        ↓

Managed Nodes
~~~

This organization separates Playbook orchestration from SSH Hardening implementation, while providing a clear structure that is easier to maintain and extend.