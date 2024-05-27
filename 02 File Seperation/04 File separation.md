File Separation - 4
Introduction: Let us now add an include statement in the playbook to include the tasks into this playbook. 

Task: After the first task - "Install dependencies" and before the current second task  "Install Python Flask dependencies", add include statement to include the file "tasks/deploy_db.yml"

--------------------------------------------------------------------------

Add below line in tasks of playbook.yaml file
```
    - include: ./tasks/deploy_db.yml
```
