Web Application - 8
Introduction: Now we copy our application code. As you can see our application code is located right next to our playbook. Feel free to explore it, but do not modify it. 

Task: Use the "copy" module to copy the application code file (app.py) to the location - /opt/app.py on the target server.

Documentation: Refer to copy module - https://docs.ansible.com/ansible/2.9/modules/copy_module.html

Not sure how to solve this? Check the answer in the solution.yml file.
--------------------
app.py is given in side as well so its available 

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

    - name: Copy web-server code
      copy: src=app.py dest=/opt/app.py


```
