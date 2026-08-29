---

title : "Firewall"

date : "`r Sys.Date()`"

weight : 2

chapter : false

pre : " <b> 5.4.2 </b> "

---

### Overview

In addition to SSH Hardening, the project uses **Firewall** as an additional security layer on the Managed Nodes.

In the Ansible section, the Firewall functionality is organized through a Playbook and Role:

~~~text
ansible/

├── playbooks/
│   └── firewall.yml
│
└── roles/
    └── firewall/
        ├── defaults/
        │   └── main.yml
        └── tasks/
            └── main.yml
~~~

### 1. `firewall.yml` Playbook

File:

~~~text
ansible/playbooks/firewall.yml
~~~

acts as the orchestrator for the Firewall configuration process.

The Playbook identifies the target hosts and calls the `firewall` Role to perform the Firewall-related tasks.

Processing flow:

~~~text
firewall.yml

      |

      ↓

firewall Role

      |

      ↓

Firewall Tasks

      |

      ↓

Managed Nodes
~~~

![ASAU](/images/01/image_228.png)

### 2. `firewall` Role

Role:

~~~text
ansible/roles/firewall/
~~~

is used to organize Firewall configuration tasks.

The Role contains:

~~~text
firewall/

├── defaults/
│   └── main.yml
│
└── tasks/
    └── main.yml
~~~

The main components are:

- `tasks/main.yml`: Contains the tasks that configure the Firewall.
- `defaults/main.yml`: Contains the default values used by the Role.

### 3. Firewall Tasks

File:

~~~text
roles/firewall/tasks/main.yml
~~~

is the component that directly performs Firewall-related changes on the Managed Nodes.

When `firewall.yml` calls the `firewall` Role, Ansible executes the tasks defined in this file.

~~~text
Playbook

   ↓

firewall Role

   ↓

tasks/main.yml

   ↓

Managed Node

   ↓

Firewall configuration
~~~

![ASAU](/images/01/image_229.png)

### 4. Defaults

File:

~~~text
roles/firewall/defaults/main.yml
~~~

contains the default values for the Firewall Role.

Separating configuration values from `tasks/main.yml` makes the Role easier to modify and manage.

### 5. Firewall Deployment Workflow

The Firewall deployment flow is:

~~~text
                Automation Server

                        |

                      Ansible

                        |

                   firewall.yml

                        |

                   firewall Role

                        |

              +---------+---------+
              |                   |
              ↓                   ↓

       Managed-Node-01     Managed-Node-02

              |                   |
              ↓                   ↓

           Firewall            Firewall
~~~

The Automation Server executes the Playbook, the Playbook calls the Role, and the Role performs the required tasks on the Managed Nodes.

### 6. Verification

After executing the Playbook, the results should be checked on the Managed Nodes to confirm that the Firewall has been configured successfully.

The verification should use commands or dedicated Playbooks that correspond to the actual Firewall configuration used in the project.

![ASAU](/images/01/image_230.png)

### Result

After completion, the Firewall functionality is organized as follows:

~~~text
firewall.yml

      ↓

firewall Role

      ↓

tasks/main.yml

      ↓

Managed Nodes
~~~

The Firewall provides an additional layer of network traffic control on the Managed Nodes while being centrally deployed and managed through Ansible.