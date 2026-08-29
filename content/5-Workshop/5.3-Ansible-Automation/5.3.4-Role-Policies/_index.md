---

title : "Ansible Roles and Policies"

date : "`r Sys.Date()`"

weight : 4

chapter : false

pre : " <b> 5.3.4 </b> "

---

### Overview

In this project, **Ansible Roles** are used to organize automation components according to their respective functions. In addition to Roles, the `policies/` directory contains the security policies used by the system.

The structure is as follows:

~~~text
ansible/

├── policies/
│   └── security_policy.yml
│
└── roles/
    ├── common/
    │   ├── defaults/
    │   │   └── main.yml
    │   ├── handlers/
    │   │   └── main.yml
    │   └── tasks/
    │       └── main.yml
    │
    ├── firewall/
    │   ├── defaults/
    │   │   └── main.yml
    │   └── tasks/
    │       └── main.yml
    │
    └── ssh_hardening/
        ├── defaults/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        └── tasks/
            └── main.yml
~~~

![ASAU](/images/01/image_215.png)

### 1. What is an Ansible Role?

A Role is a way for Ansible to organize tasks, variables, and handlers into a structured and reusable component.

Instead of placing all tasks in a single large Playbook, the project divides automation into separate Roles based on their functions.

~~~text
Playbook

   |

   +── common

   |

   +── firewall

   |

   └── ssh_hardening
~~~

This organization makes the code easier to read, maintain, and reuse.

### 2. `common` Role

The Role structure is:

~~~text
roles/common/

├── defaults/
│   └── main.yml
│
├── handlers/
│   └── main.yml
│
└── tasks/
    └── main.yml
~~~

The `common` Role contains shared configuration components.

The main components are:

- `tasks/main.yml`: Contains the main tasks of the Role.
- `defaults/main.yml`: Contains the default values of the Role.
- `handlers/main.yml`: Contains Handlers that are triggered when notified by a task.

![ASAU](/images/01/image_216.png)

![ASAU](/images/01/image_217.png)

### 3. `firewall` Role

The Role structure is:

~~~text
roles/firewall/

├── defaults/
│   └── main.yml
│
└── tasks/
    └── main.yml
~~~

The `firewall` Role focuses on tasks related to Firewall configuration.

Configurable values are organized in:

~~~text
defaults/main.yml
~~~

The tasks that perform the actual configuration are located in:

~~~text
tasks/main.yml
~~~

![ASAU](/images/01/image_218.png)

### 4. `ssh_hardening` Role

The Role structure is:

~~~text
roles/ssh_hardening/

├── defaults/
│   └── main.yml
│
├── handlers/
│   └── main.yml
│
└── tasks/
    └── main.yml
~~~

The `ssh_hardening` Role focuses on SSH security configuration.

The main components are:

- `tasks/main.yml`: Contains tasks for SSH Hardening.
- `defaults/main.yml`: Contains the default configuration values.
- `handlers/main.yml`: Contains Handlers used to apply changes when required.

![ASAU](/images/01/image_219.png)

### 5. Defaults

Roles can use:

~~~text
defaults/main.yml
~~~

to define default values.

The basic flow is:

~~~text
defaults/main.yml

        |

        ↓

      Role

        |

        ↓

  tasks/main.yml
~~~

Separating configurable values from the tasks makes the Role more flexible when used in different environments or scenarios.

### 6. Tasks

The file:

~~~text
tasks/main.yml
~~~

is the main component that contains the tasks of a Role.

When a Role is invoked, Ansible executes the tasks defined in this file in sequence.

### 7. Handlers

Some Roles contain:

~~~text
handlers/main.yml
~~~

Handlers are used for tasks that only need to be executed when a previous task makes a change and sends a notification using `notify`.

The basic flow is:

~~~text
Task

  |

  | changed

  ↓

notify

  |

  ↓

Handler
~~~

In this project, the `common` and `ssh_hardening` Roles contain `handlers` directories.

![ASAU](/images/01/image_221.png)

### 8. Security Policy

In addition to Roles, the project contains:

~~~text
ansible/policies/security_policy.yml
~~~

This file belongs to the **Policies** component and is used to store security-related criteria or configuration for the system.

Separating the Security Policy into its own file prevents policy definitions from being directly mixed with task implementation.

![ASAU](/images/01/image_222.png)

### 9. Relationship Between Roles, Playbooks, and Policies

The components work together according to the following model:

~~~text
                Security Policy

                       |

                       ↓

                security_policy.yml

                       |

                       |

Inventory → Playbook → Role

                       |

              +--------+--------+
              |        |        |
              ↓        ↓        ↓
           common   firewall  ssh_hardening
              |        |        |
              +--------+--------+
                       |
                       ↓
                 Managed Nodes
~~~

The Playbook defines the automation workflow, Roles organize tasks by function, and Policies provide the security criteria or configuration used by the system.

### 10. Result

After organizing Roles and Policies, the Ansible section of the project has the following structure:

~~~text
ansible/

│

├── policies/
│   └── security_policy.yml
│
└── roles/
    ├── common/
    ├── firewall/
    └── ssh_hardening/
~~~

This organization clearly separates the responsibilities:

~~~text
Playbooks → Orchestrate automation

Roles     → Organize tasks by function

Policies  → Manage security criteria
~~~

This structure provides the foundation for implementing **Security Hardening, Security Audit, and Automated Remediation** in the following sections.