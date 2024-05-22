Web Application - 5
Introduction: Now let us create application database on the sql server. 

Task: Create a new task and use "mysql_db" module to create a new database by the name "employee_db". 

Documentation: Refer to mysql_db module - https://docs.ansible.com/ansible/2.9/modules/mysql_db_module.html

Not sure how to solve this? Check the answer in the solution.yml file.
--------------------------------------------------------------------

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
        
    - name: Create a New database
      mysql_db:
        name: employee_db
        state: present
        
```
