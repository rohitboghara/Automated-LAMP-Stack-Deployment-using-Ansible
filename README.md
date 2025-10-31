Automated LAMP Stack Deployment using Ansible
=============================================

A quick and repeatable way to deploy a full LAMP (Linux, Apache, MySQL, PHP)
stack using Ansible playbooks.

------------------------------------------------------------
TABLE OF CONTENTS
------------------------------------------------------------
1. Introduction
2. Features
3. Prerequisites
4. Architecture
5. Usage
   - nodes.ini (Inventory file)
   - site.yml (Playbook)
6. Roles & Directory Structure
7. Customisation
8. Testing & Troubleshooting
9. Licence
10. Contributing

------------------------------------------------------------
1. INTRODUCTION
------------------------------------------------------------
This project automates the deployment of a full LAMP stack on
servers using Ansible.

What it installs:
- Linux environment (target server)
- Apache Web Server
- MySQL / MariaDB Database Server
- PHP and required extensions

It supports multiple servers and ensures consistent and automated deployment.

------------------------------------------------------------
2. FEATURES
------------------------------------------------------------
- Fully automated using Ansible playbook
- Dedicated roles for Apache, MySQL, PHP
- nodes.ini file to control all servers
- Idempotent (run multiple times safely)
- Modular & extendable

------------------------------------------------------------
3. PREREQUISITES
------------------------------------------------------------
Control machine must have:
- Ansible installed
- SSH access to target machines
- Python installed on target hosts
- sudo/root permissions

------------------------------------------------------------
4. ARCHITECTURE
------------------------------------------------------------
Control Machine (Ansible)
      |
      v
--------------------------------
| Target Server 1 (Linux)     |
| Apache + MySQL + PHP        |
--------------------------------
         ...
--------------------------------
| Target Server N (Linux)     |
| Apache + MySQL + PHP        |
--------------------------------

Order of playbook execution:
1. MySQL Role
2. Apache Role
3. PHP Role

------------------------------------------------------------
5. USAGE
------------------------------------------------------------

----- nodes.ini -----
Example inventory file:
[webservers]
server1.example.com
server2.example.com

[dbservers]
db1.example.com

----- Run Playbook -----
To deploy:
ansible-playbook -i nodes.ini site.yml

If sudo password needed:
ansible-playbook -i nodes.ini site.yml --ask-become-pass

------------------------------------------------------------
6. ROLES & DIRECTORY STRUCTURE
------------------------------------------------------------
Directory structure:
.
├─ apache/
│  ├─ tasks/
│  ├─ handlers/
│  └─ templates/
├─ mysql/
│  ├─ tasks/
│  ├─ handlers/
│  └─ templates/
├─ php/
│  ├─ tasks/
│  ├─ handlers/
│  └─ templates/
├─ nodes.ini
└─ site.yml

Each role contains:
- tasks → installation and config steps
- handlers → restart services
- templates → config templates

------------------------------------------------------------
7. CUSTOMISATION
------------------------------------------------------------
- Change MySQL root password in mysql/vars
- Add Apache Virtual Hosts in apache/templates
- Add extra PHP modules in php/tasks
- Add more roles (SSL, firewall, backup etc.)

------------------------------------------------------------
8. TESTING & TROUBLESHOOTING
------------------------------------------------------------
Dry-run (check mode):
ansible-playbook -i nodes.ini site.yml --check

Show file differences:
ansible-playbook -i nodes.ini site.yml --diff

Common checks:
- Ping hosts: ansible -i nodes.ini -m ping all
- Check SSH connection
- Check /var/log/apache2/ or /var/log/mysql logs

------------------------------------------------------------
9. LICENCE
------------------------------------------------------------
Licensed under MIT License.

------------------------------------------------------------
10. CONTRIBUTING
------------------------------------------------------------
How to contribute:
1. Fork project
2. Create a branch
3. Commit changes
4. Push branch
5. Open Pull Request

------------------------------------------------------------
QUOTE
------------------------------------------------------------
"Automate everything, and then sleep easy."
