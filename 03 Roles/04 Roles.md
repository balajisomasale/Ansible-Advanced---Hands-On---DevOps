
Roles - 4
Task: To tie it all together, add roles directive to the playbook and add the roles in the following order:- 

- python 
- mysql_db 
- flask_web

-------------------------------

```
-
  name: Deploy a web application
  hosts: db_and_web_server
  roles:
    - python
    - mysql_db 
    - flask_web
```
