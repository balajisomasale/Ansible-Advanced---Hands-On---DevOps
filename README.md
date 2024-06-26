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

## Ansible Lookups:
- It will allow you to retrieve data from external sources and use that data in your playbooks, roles, and templates. Lookups can be used to access files, generate lists, read environment variables, and more. They are evaluated on the Ansible controller side before the task is executed on the remote host
- More details: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/42c3ebd8603226d20716cf2c04fbc8bcbfbfe28d/08%20Lookups

## Ansible Vaults:

- More details: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/521bd246d7a8391ba803ad667b187301cfbe116c/09%20Vaults

## Dynamic Inventory:

- MOre details : https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/9e5632a5d063ba4f103fa42b598aa6b23e223c4a/10%20Dynamic%20Inventory

## Custom Modules:
- More details: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/e88c3ba85274125441c0089a8667acb9a923114e/11%20Custom%20Modules

## Plugins:
- More details: https://github.com/balajisomasale/Ansible-Advanced---Hands-On---DevOps/tree/9b88c218c0099e786ff1ba772de98836f8c0b653/12%20Plugins
