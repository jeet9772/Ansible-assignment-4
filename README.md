# Ansible System Manager Role

## Objective

Create an Ansible `system_manager` role to manage common system-level configurations on a Linux server.

The role can be used to manage:

* Software packages
* System users
* Git repositories
* Required folder structures
* Other basic system settings

## Author

Jeetendra Singh

## Project Structure

```text
.
├── ansible.cfg
├── inventory
├── jeet11.pem
├── system-manager.yml
└── system_manager
    ├── README.md
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml
    ├── templates
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml
```

## How the role is organized

The `system_manager` role follows the standard Ansible role structure.

The main tasks are defined in `tasks/main.yml`, while configurable values are maintained in `defaults/main.yml`.

| Feature              | Responsibility                    |
| -------------------- | --------------------------------- |
| Software Management  | Install required packages         |
| User Management      | Create/manage system users        |
| Git Management       | Clone/manage Git repositories     |
| Directory Management | Create required folder structures |

## Role Variables

All configurable data is defined in:

```text
system_manager/defaults/main.yml
```

Example:

```yaml
system_manager_packages:
  - git
  - curl
  - vim
  - wget

system_manager_users:
  - devuser
  - testuser

system_manager_git_repositories:
  - repo: https://github.com/opstree/spring3hibernate.git
    dest: /opt/spring3hibernate

system_manager_directories:
  - /opt/app
  - /opt/app/logs
  - /opt/app/config
  - /opt/app/data
```

## Example Playbook (`system-manager.yml`)

```yaml
---
- name: Configure System Manager
  hosts: workers
  become: true

  roles:
    - system_manager
```

## How to run

```bash
# Test connectivity
ansible workers -m ping

# Syntax check
ansible-playbook system-manager.yml --syntax-check

# Apply configuration
ansible-playbook system-manager.yml
```

## Verify Result

```bash
# Verify packages
rpm -q git curl vim wget

# Verify users
id devuser
id testuser

# Verify Git repository
ls -ld /opt/spring3hibernate

# Verify directories
ls -ld /opt/app
ls -ld /opt/app/logs
ls -ld /opt/app/config
ls -ld /opt/app/data
```

## Additional System-Specific Settings

The role can be extended to manage:

* Services
* Firewall rules
* Hostname
* Timezone
* Cron jobs
* SSH configuration
* File permissions

## Conclusion

The `system_manager` role automates common Linux system administration tasks such as software installation, user management, Git repository management, and directory creation.

**Assignment:** Ansible Assignment 4 – System Manager Role

**Prepared By:** Jeetendra Singh
