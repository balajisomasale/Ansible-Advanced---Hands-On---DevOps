File Separation - 3
Introduction: We will now separate the tasks into different files. We have now created a folder called "tasks" and created two files under it called "deploy_db.yml" and "deploy_web.yml". We will now move the tasks from the main playbook into respective tasks files - deploy_db.yml and deploy_web.yml 

Task: First, move (simply cut and paste) the below tasks into deploy_db.yml file 

- Install MySQL database 
- Start Mysql Service 
- Create Application Database 
- Create Application DB User 
Note: We will leave Install Dependencies there, since it is not specific to database or web. We will add the include statement in the next exercise.

-----------------------------------------

copy paste as instructed above into `deploy_db.yml file `
