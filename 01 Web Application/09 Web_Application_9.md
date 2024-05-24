Web Application - 9
Introduction: Let us now start the web application using the below command:-

   FLASK_APP=/opt/app.py nohup flask run --host=0.0.0.0 &  

Task: Use the "shell" module to execute the above command on the target host.

Documentation: Refer to shell module - https://docs.ansible.com/ansible/2.9/modules/shell_module.html

Not sure how to solve this? Check the answer in the solution.yml file.
-------------------------------------------
inv:
```
db_and_web_server ansible_connection=ssh ansible_ssh_pass=Passw0rd ansible_host=192.168.1.14
```
playbook.yml:
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

    - name: Start web-application
      shell: FLASK_APP=/opt/app.py nohup flask run --host=0.0.0.0 &

```

