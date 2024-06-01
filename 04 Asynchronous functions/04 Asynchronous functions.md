Asynchronous Actions - 4
Introduction: We do not want to just "fire and forget", we would like to "check on it later" too. 

Task: Register the results of the monitoring tasks into variables "webapp_result" and "database_result".

----------------------------------------

```
-
  name: Monitor Web Application for 6 Minutes
  hosts: web_server
  command: /opt/monitor_webapp.py
  async: 360
  poll: 0
  register: webapp_result

```
```

-
  name: Monitor Database for 6 Minutes
  hosts: db_server
  command: /opt/monitor_database.py
  async: 360
  poll: 0
  register: database_result

```
