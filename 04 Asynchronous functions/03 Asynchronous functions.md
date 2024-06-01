Asynchronous Actions - 3

Introduction: We have now added a new monitoring play to monitor the database. 
However, our playbook spends 6 minutes monitoring web application and 
once that completes monitors database for 6 minutes. We would like to make this parallel. 

Task: Update poll value for both tasks to 0 to "fire and forget" the monitoring tasks. 

--------------------------

```
-
  name: Monitor Web Application for 6 Minutes
  hosts: web_server
  command: /opt/monitor_webapp.py
  async: 360
  poll: 0
```

```
-
  name: Monitor Database for 6 Minutes
  hosts: db_server
  command: /opt/monitor_database.py
  async: 360
  poll: 0

```
