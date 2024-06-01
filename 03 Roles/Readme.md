Solutions for coding exercises: 

https://github.com/mmumshad/ansible-training-answer-keys-2


# Ansible roles:

provide a structured way to group and organize tasks, handlers, variables, files, templates, and modules into reusable and shareable units. Roles help in maintaining a clean, modular, and reusable codebase.

### Structure of a Role

Roles have a specific directory structure:

```plaintext
roles/
  └── role_name/
      ├── tasks/
      │   └── main.yml
      ├── handlers/
      │   └── main.yml
      ├── files/
      ├── templates/
      ├── vars/
      │   └── main.yml
      ├── defaults/
      │   └── main.yml
      ├── meta/
      │   └── main.yml
      └── README.md
```

### Example of Using Roles

#### Directory Structure:

```plaintext
my_playbook/
├── playbook.yml
├── roles/
│   └── webserver/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       ├── templates/
│       │   └── httpd.conf.j2
│       ├── vars/
│       │   └── main.yml
│       └── defaults/
│           └── main.yml
└── inventory
```

#### playbook.yml

```yaml
- name: Apply webserver role
  hosts: webservers
  roles:
    - webserver
```

#### roles/webserver/tasks/main.yml

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

#### roles/webserver/handlers/main.yml

```yaml
---
- name: restart apache
  ansible.builtin.service:
    name: httpd
    state: restarted
```

#### roles/webserver/templates/httpd.conf.j2

```jinja
Listen {{ http_port }}
DocumentRoot "/var/www/html"
```

#### roles/webserver/vars/main.yml

```yaml
---
server_admin: webmaster@localhost
```

#### roles/webserver/defaults/main.yml

```yaml
---
http_port: 80
```

### inventory

```ini
[webservers]
web1.example.com
web2.example.com
```

### Explanation:

1. **playbook.yml**: This playbook applies the `webserver` role to all hosts in the `webservers` group.
2. **roles/webserver/tasks/main.yml**: This file contains tasks to install Apache and deploy the `httpd.conf` file from a template.
3. **roles/webserver/handlers/main.yml**: This file defines a handler to restart Apache whenever it is notified by a task.
4. **roles/webserver/templates/httpd.conf.j2**: This Jinja2 template defines the content of the `httpd.conf` file, using the variable `http_port`.
5. **roles/webserver/vars/main.yml**: This file contains role-specific variables. Here, it defines the `server_admin` variable.
6. **roles/webserver/defaults/main.yml**: This file contains default values for variables used in the role. It sets `http_port` to 80.
7. **inventory**: This file lists the hosts that belong to the `webservers` group.

### Benefits of Using Roles:

- **Reusability**: Roles can be reused across multiple playbooks and projects.
- **Organization**: Roles provide a clear structure, making it easier to manage and navigate Ansible code.
- **Modularity**: Roles allow you to break down complex configurations into manageable, self-contained units.
- **Maintainability**: With a well-structured role, updating and maintaining the codebase becomes easier, especially in larger projects.

Roles are an essential feature in Ansible that promote good practices in managing infrastructure as code.
