Web Application - 4
Introduction: Now let us add a new task to start the mysql service.

Task: Create a new task and use "service" module to start the "mysql" service. Ensure you set enabled to true so that the service starts automatically every time the server restarts.

Documentation: Refer to service module - https://docs.ansible.com/ansible/2.9/modules/service_module.html

Not sure how to solve this? Check the answer in the solution.yml file.
--------------------------------------------------------------
inv:
```
db_and_web_server ansible_connection=ssh ansible_ssh_pass=Passw0rd ansible_host=192.168.1.14
```

playbook.yaml
```
-
  name: Deploy a web application
  hosts: db_and_web_server
  tasks:
    - name: Install dependencies
      apt: name={{ item }} state=present
      with_items:
       - python
       - python-setuptools
       - python-dev
       - build-essential
       - python-pip
       - python-mysqldb

    - name: Install MySQL database
      apt:
        name: "{{ item }}"
        state:  present
      with_items:
       - mysql-server
       - mysql-client

    - name: Start Mysql Service
      service:
        name: mysql
        state: started
        enabled: yes
```
