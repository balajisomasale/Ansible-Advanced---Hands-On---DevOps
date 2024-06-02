# Ansible-Advanced---Hands-On---DevOps :: KodeKloud Udemy

## File Separation:
- File separation can be used by invoking `include` command in a playbook. Its purpose is to use any playbook file into the main playbook.
- For quick walkthrough of how file separation works, visit: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/blob/000b546735f14c937bf68f8fb25d6517d4341bd3/02%20File%20Seperation/Readme.md

## Ansible Roles:
- Roles were introduced to replace `include` commands of many `separation` among files and can be invoked anytime
- For quick walkthrough of how Ansible roles works, visit: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/blob/b535f1cefbe5ff4fb5b00a380c36223d65ce01ee/03%20Roles/Readme.md
  
## Asynchronous functions:
- Asynchronous functions `async` to wait and `poll` frequency for tasks to finish. It also has `aync_status` with its parameters that can be used to check the status for any registered custom variable in a given play.
- For quick walkthrough of how it works, visit: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/f786769d74622642aef1522301079ecc8f01ee3a/04%20Asynchronous%20functions

## Strategies:
- strategies control the execution flow of tasks across hosts, with options like linear for sequential execution, free for concurrent execution, and debug for interactive debugging.
For detailed info: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/blob/c82c9765f5f347547b707c179d4901a6fd34ac20/05%20Strategies/Readme.md1

## Error Handling:
- Error handling in Ansible is crucial for managing and responding to failures in your playbooks. Ansible provides several mechanisms for error handling, including ignore_errors, failed_when, changed_when, and rescue/always blocks.
- More details: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/blob/54146cbe652f197276b5e1e12072bd60f56b9d8c/06%20Error%20Handling/Readme.md

## Jinja2 Templating:
- It is a templating engine used in Ansible to generate dynamic content. It allows you to use variables, control structures (like loops and conditionals), and filters to create templates for configuration files, scripts, or other text files.
- More details: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/701f6155a80979dee262cf9203d05e38c09a6f5b/07%20Jinja2%20Templating






