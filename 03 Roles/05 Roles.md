Roles - 5
Introduction: We are now tasked to re-use our work to split the Architecture of our application
from a monolithic (all-in-one) to distributed. 

Note that the inventory file is now updated with two separate servers - db_server and web_server.
Also separate host_vars file have been created for each of them. 

Task: Update the current play to target "db_server" host and apply roles "python" and "mysql_db" to it. 

Note: We need python dependencies on the sql server as well.

--------------------


```
-
  name: Deploy a mysql DB
  hosts: db_server
  roles:
    - python
    - mysql_db
```
