Web Application - 2
Introduction: In the given playbook the first task is incomplete. Only a name is given. 

Task: Update the task to use the "apt" module to install all required packages. The list of packages to be installed are given below. Remember to use loop (with_items) to install all packages in one task: 

        - python 
        - python-setuptools 
        - python-dev 
        - build-essential 
        - python-pip 
        - python-mysqldb 
Documentation: Refer to apt module - https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html

Not sure how to solve this? Check the answer in the solution.yml file.


--------------------

inventory.ini:
```
db_and_web_server ansible_connection=ssh ansible_ssh_pass=Passw0rd ansible_host=192.168.1.14
```
playbook.yml:

```-
  name: Deploy a web application
  hosts: db_and_web_server
  tasks:
    - name: Install dependencies
      apt: name='{{ item }}' state=present
      with_items:
       - python
       - python-setuptools
       - python-dev
       - build-essential
       - python-pip
       - python-mysqldb
```
