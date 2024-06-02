# Jinja2 Templating:

is a templating engine used in Ansible to generate dynamic content. It allows you to use variables, control structures (like loops and conditionals), and filters to create templates for configuration files, scripts, or other text files. 

### Example of Jinja2 Templating in Ansible

#### Directory Structure:
```plaintext
my_playbook/
├── playbook.yml
├── templates/
│   └── config.j2
└── inventory
```

#### inventory
```ini
[webservers]
web1.example.com
web2.example.com
```

#### playbook.yml

```yaml
- name: Configure web servers
  hosts: webservers
  vars:
    server_name: "{{ inventory_hostname }}"
    document_root: "/var/www/html"
  tasks:
    - name: Deploy configuration file
      ansible.builtin.template:
        src: config.j2
        dest: /etc/myapp/config.conf
      notify: restart myapp

  handlers:
    - name: restart myapp
      ansible.builtin.service:
        name: myapp
        state: restarted
```

#### templates/config.j2

```jinja
# Configuration file for myapp

server {
    listen 80;
    server_name {{ server_name }};
    
    location / {
        root {{ document_root }};
        index index.html index.htm;
    }
}
```

### Explanation:

1. **Template File (config.j2)**:
   - The `config.j2` file is a Jinja2 template that generates a configuration file. It uses variables `{{ server_name }}` and `{{ document_root }}` to insert dynamic values into the template.

2. **Playbook (playbook.yml)**:
   - The playbook applies to all hosts in the `webservers` group.
   - It defines two variables: `server_name` and `document_root`. The `server_name` variable uses the `inventory_hostname` to dynamically set the name of the server.
   - The `template` module is used to deploy the `config.j2` template to `/etc/myapp/config.conf` on each web server.
   - A handler named `restart myapp` is notified to restart the service whenever the configuration file is deployed.

3. **Inventory (inventory)**:
   - Lists the web servers where the playbook will be executed.

### Running the Playbook

To execute the playbook, use the following command:

```sh
ansible-playbook -i inventory playbook.yml
```

### Key Features of Jinja2 Templating:

1. **Variables**: Insert dynamic data into templates using `{{ variable_name }}`.
2. **Control Structures**: Use loops and conditionals to generate dynamic content.
   - **Loop Example**:
     ```jinja
     {% for user in users %}
     User: {{ user.name }}
     {% endfor %}
     ```
   - **Conditional Example**:
     ```jinja
     {% if server_role == "web" %}
     Server is a web server.
     {% else %}
     Server is not a web server.
     {% endif %}
     ```
3. **Filters**: Modify variables using filters.
   - **Example**:
     ```jinja
     {{ my_variable | upper }}
     ```
   - This converts the content of `my_variable` to uppercase.

4. **Whitespace Control**: Manage whitespace using control statements `{%-` and `-%}`.

### Benefits:

- **Dynamic Configuration**: Generate configuration files tailored to specific environments or hosts.
- **Reuse and Modularity**: Use templates to manage configurations across multiple hosts and environments.
- **Readability**: Keep playbooks clean by separating static content from dynamic content.

Using Jinja2 templating in Ansible is a powerful way to manage dynamic content, making your automation more flexible and adaptable to different environments and configurations.
