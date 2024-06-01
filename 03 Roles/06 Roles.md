
Role - 6
Introduction: We only have db server right now.
Let us create a new play to install and configure web application on the web server. 

Task: Create a new play called "Deploy a web server" and target host "web_server". 
Apply the roles "python" and "flask_web" to it

--------------------------

```
-
  name: Deploy a mysql DB
  hosts: db_server
  roles:
    - python
    - mysql_db
    
- name: Deploy a web server 
  hosts: web_server
  roles:
    - python
    - flask_web


```
