Web Application - 7
Introduction: Now let us install python dependencies for the Flask Application.

Task: Create a new task and use "pip" module to install python dependencies. 

Remember to use loop with with_items to install below dependencies:-

- flask 
- flask-mysql
Documentation: Refer to pip module - https://docs.ansible.com/ansible/2.9/modules/pip_module.html
--------------------------------------------------------

inv:
```
db_and_web_server ansible_connection=ssh ansible_ssh_pass=Passw0rd ansible_host=192.168.1.14
```
playbook.yaml:
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

    - name: Create Application Database
      mysql_db: name='employee_db' state=present

    - name: Create Application DB User
      mysql_user: name='db_user' password='Passw0rd' priv='*.*:ALL' host='%' state='present'

    - name: Install Python Flask dependencies
      pip:
        name: '{{ item }}'
        state: present
      with_items:
       - flask
       - flask-mysql

```
