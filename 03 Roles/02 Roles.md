Roles - 2
Introduction: We have now created a new role using the following command 'ansible-galaxy init flask_web'. 
This has created a folder structure for us. 

Task: Move the web related tasks to roles/flask_web/tasks/main.yml file. 

- Install Python Flask dependencies 
- Copy web-server code 
- Start web-application
  
Note: We will leave Install Dependencies there, since it is not specific to database or web. We will add roles statement in a later exercise.

-------------------------------


 Move the web related tasks to roles/flask_web/tasks/main.yml 

