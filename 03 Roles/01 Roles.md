Roles - 1
Introduction: In the previous Exercises we moved tasks to a separate tasks file and used include statements to include tasks. Now we will start using Roles to organize and reuse our work. We have created a new role using the following command 'ansible-galaxy init mysql_db'. This has created a folder structure for us.  See the folder structure in the attached image. 

Task: First, move (simply cut and paste) the below tasks into roles/mysql_db/tasks/main.yml file. 

- Install MySQL database 
- Start Mysql Service 
- Create Application Database 
- Create Application DB User

  
Note: We will leave 'Install Dependencies' there, since it is not specific to database or web. 
We will add roles statement in a later Exercise.

---------------------

paste the code into roles/main.yml file 
