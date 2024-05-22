Task: Update the host on the playbook to work with our target server "db_and_web_server"


inventory.ini

`
db_and_web_server ansible_connection=ssh ansible_ssh_pass=Passw0rd ansible_host=192.168.1.14

`
Task is 

playbook.yml:

`
-
  name: Deploy a web application
  hosts: db_and_web_server
  tasks:
    - name: Install dependencies
`
