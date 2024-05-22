Web Application - 3
Introduction: Now let us add a new task to the play to install MySQL database. 

Task: Create a new task similar to the first one and use "apt" to install two more packages: 

        - mysql-server 
        - mysql-client 
Documentation: Refer to apt module - https://docs.ansible.com/ansible/2.9/modules/apt_module.html



Not sure how to solve this? Check the answer in the solution.yml file.
----------------------------------------------------------------------------

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
      apt: name='{{ item }}' state=present
      with_items:
       - mysql-server
       - mysql-client

```
