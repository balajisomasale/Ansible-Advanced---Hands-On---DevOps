File Separation - 5
Introduction: Do the same for all the tasks under web application deployment. A new file is created under tasks folder named - deploy_web.yml. 

Task: Move the below tasks to the new file and add include statement in the main playbook to include the file "tasks/deploy_web.yml"

- name: Install Python Flask dependencies
- name: Copy web-server code
- name: Start web-application

------------------------------------------------------------

cut the exisitng code to ``` tasks/deploy_web.yml```
then add ``` - include tasks/deploy_web.yaml```

