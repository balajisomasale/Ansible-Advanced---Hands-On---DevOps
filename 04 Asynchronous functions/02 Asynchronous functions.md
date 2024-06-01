Asynchronous Actions - 2
Introduction: The default polling interval is 10 seconds. We think that is too often. 

Task: Change it to poll every 30 seconds. 

-------------------

```
-
  name: Monitor Web Application for 6 Minutes
  hosts: web_server
  command: /opt/monitor_webapp.py
  async: 360
  poll: 30

```
