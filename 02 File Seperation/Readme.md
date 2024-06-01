Solutions of above coding exercises: 
https://github.com/mmumshad/ansible-training-answer-keys-2/tree/master/Section_2_Web_Playbook

# File separation in Ansible:

refers to the practice of organizing your Ansible code into multiple files to improve readability, maintainability, and scalability. By separating your configuration into logical parts, you can manage and update your automation scripts more efficiently. Common strategies include splitting tasks, handlers, variables, and roles into separate files.

Here’s an example to illustrate file separation in Ansible:

### Example Directory Structure:

```plaintext
my_playbook/
├── playbook.yml
├── group_vars/
│   └── all.yml
├── host_vars/
│   └── hostname.yml
├── roles/
│   ├── webserver/
│   │   ├── tasks/
│   │   │   └── main.yml
│   │   ├── handlers/
│   │   │   └── main.yml
│   │   ├── templates/
│   │   │   └── httpd.conf.j2
│   │   └── vars/
│   │       └── main.yml
│   └── database/
│       ├── tasks/
│       │   └── main.yml
│       └── vars/
│           └── main.yml
└── inventory
```

### playbook.yml

```yaml
- name: Configure web and database servers
  hosts: all
  roles:
    - webserver
    - database
```

### group_vars/all.yml

```yaml
---
http_port: 80
db_port: 5432
```

### host_vars/hostname.yml

```yaml
---
db_name: my_database
db_user: admin
db_password: secret
```

### roles/webserver/tasks/main.yml

```yaml
---
- name: Install Apache
  ansible.builtin.yum:
    name: httpd
    state: present

- name: Deploy httpd.conf
  ansible.builtin.template:
    src: httpd.conf.j2
    dest: /etc/httpd/conf/httpd.conf
  notify:
    - restart apache
```

### roles/webserver/handlers/main.yml

```yaml
---
- name: restart apache
  ansible.builtin.service:
    name: httpd
    state: restarted
```

### roles/webserver/templates/httpd.conf.j2

```jinja
Listen {{ http_port }}
DocumentRoot "/var/www/html"
```

### roles/webserver/vars/main.yml

```yaml
---
server_admin: webmaster@localhost
```

### roles/database/tasks/main.yml

```yaml
---
- name: Install PostgreSQL
  ansible.builtin.yum:
    name: postgresql-server
    state: present

- name: Initialize PostgreSQL database
  ansible.builtin.command: /usr/bin/postgresql-setup initdb
  args:
    creates: /var/lib/pgsql/data

- name: Ensure PostgreSQL is running
  ansible.builtin.service:
    name: postgresql
    state: started
    enabled: yes
```

### roles/database/vars/main.yml

```yaml
---
pg_data: /var/lib/pgsql/data
pg_hba_conf: /var/lib/pgsql/data/pg_hba.conf
```

### inventory

```ini
[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
```

In this example, the playbook (`playbook.yml`) references roles for configuring web and database servers. Each role is separated into different files:

- `tasks/main.yml`: Defines the tasks to be executed.
- `handlers/main.yml`: Contains handlers that are notified by tasks.
- `vars/main.yml`: Holds variables specific to the role.
- `templates/`: Stores template files (e.g., configuration files).

Additionally, `group_vars` and `host_vars` directories are used to define variables for groups of hosts and individual hosts, respectively. This separation makes the playbook easier to read, manage, and scale as your infrastructure grows.
