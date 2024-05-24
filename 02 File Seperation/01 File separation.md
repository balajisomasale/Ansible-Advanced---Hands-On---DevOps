File Separation - 1
Introduction: Let us improvise our playbook a little bit more. We have created a folder called host_vars and created a file under it called "db_and_web_server.yml". 

Task: Move the connection information such as the IP and password to the new file and remove it from the inventory file.

---------
db_and_web_server.yml
```
ansible_ssh_pass: Passw0rd
ansible_host: 192.168.1.14
```
