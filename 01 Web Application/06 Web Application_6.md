Web Application - 6
Introduction: Now let us create application database user on the sql server. 

Task: Create a new task and use "mysql_user" module to create a new user. Use the details below:-

user name: db_user 
user password: Passw0rd 
user privilege: *.*:ALL 
host: '%' 
Documentation: Refer to mysql_user module - https://docs.ansible.com/ansible/2.9/modules/mysql_user_module.html

Not sure how to solve this? Check the answer in the solution.yml file.
------------------------------------------------------------

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
```
