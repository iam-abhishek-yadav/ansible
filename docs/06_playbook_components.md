## Playbook

A **Playbook** in Ansible is a YAML file that defines a series of actions to be executed on managed nodes. It organizes these actions into plays, which map groups of hosts to specific roles and tasks.

#### Example Playbook

```yaml
---
- name: Update web servers
  hosts: webservers
  remote_user: root

  tasks:
    - name: Ensure Apache is at the latest version
      yum:
        name: httpd
        state: latest

    - name: Write the Apache config file
      template:
        src: /srv/httpd.j2
        dest: /etc/httpd.conf

- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
    - name: Ensure PostgreSQL is at the latest version
      yum:
        name: postgresql
        state: latest

    - name: Ensure that PostgreSQL is started
      service:
        name: postgresql
        state: started
```

## Play

A **Play** in Ansible is a unit of configuration and execution. It specifies a set of tasks to be applied to one or more hosts defined in the playbook. Each play defines which hosts to target and what roles and tasks to execute on those hosts.

#### Example Play

```yaml
- name: Install and configure Nginx
  hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```

## Modules

**Modules** are reusable, standalone scripts executed by Ansible on remote hosts. They perform specific tasks such as installing packages, managing files, and interacting with services. Ansible includes a wide range of built-in modules and also supports custom modules.

#### Example Module Usage

```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present
```

## Tasks

**Tasks** are the individual steps within a play that leverage modules to perform actions on managed nodes. Tasks execute in sequential order and can include conditions, loops, and error handling.

#### Example Tasks

```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present

- name: Start Nginx service
  service:
    name: nginx
    state: started
```

## Collections

**Collections** in Ansible bundle and distribute roles, modules, plugins, and other content. They facilitate sharing and reusing Ansible components across different environments.

#### Example Collection Structure

```
my_collection/
├── roles/
│   └── my_role/
│       └── tasks/
│           └── main.yml
├── plugins/
│   └── modules/
│       └── my_module.py
└── README.md
```

#### Using a Collection

```yaml
- name: Use a custom module from a collection
  community.general.my_module:
    option: value
```
