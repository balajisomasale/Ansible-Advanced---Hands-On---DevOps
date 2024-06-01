
Asynchronous Actions - 1

Introduction: We have added a new play at the end of our playbook to monitor the web application 
for 6 minutes to ensure its running OK.
However, we don't want to hold the SSH Connection for the duration of this execution. 

Task: Make the monitoring task Asynchronous by adding async option to the task to wait for 6 minutes.

---------------------------------

```
-
  name: Monitor Web Application for 6 Minutes
  hosts: web_server
  command: /opt/monitor_webapp.py
  async: 360
```
