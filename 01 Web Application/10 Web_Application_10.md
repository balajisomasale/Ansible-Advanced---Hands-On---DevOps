Web Application - 10
Introduction: Let us now improvise a little bit. Let us move some of the variable details out to a vars section at the top. 

Task: Add a vars section under the playbook and define db_name, db_user and db_password. Then replace the static definitions to use variable name.

Documentation: Refer to vars in ansible - variables

Not sure how to solve this? Check the answer in the solution.yml file.
--------------------------------------------------------
inv:
```
db_and_web_server ansible_connection=ssh ansible_ssh_pass=Passw0rd ansible_host=192.168.1.14
```

playbook.yml:
```
-
  name: Deploy a web application
  hosts: db_and_web_server
  vars:
    db_name: employee_db
    db_user: db_user
    db_password: Passw0rd
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
      mysql_db: name={{ db_name }} state=present

    - name: Create Application DB User
      mysql_user: name={{ db_user }} password={{ db_password }} priv='*.*:ALL' host='%' state='present'

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


