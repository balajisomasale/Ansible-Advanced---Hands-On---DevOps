Error handling in Ansible is crucial for managing and responding to failures in your playbooks. Ansible provides several mechanisms for error handling, including `ignore_errors`, `failed_when`, `changed_when`, and `rescue`/`always` blocks.

### Common Error Handling Methods:

1. **ignore_errors**
2. **failed_when**
3. **changed_when**
4. **rescue/always blocks**

### Examples:

#### 1. ignore_errors

This allows a task to continue even if it fails.

```yaml
- name: Attempt to install a package
  ansible.builtin.yum:
    name: non_existent_package
    state: present
  ignore_errors: yes

- name: This task will still run
  ansible.builtin.debug:
    msg: "The previous task was ignored."
```

#### 2. failed_when

This allows you to specify conditions under which a task should be considered failed.

```yaml
- name: Check for a specific string in a file
  ansible.builtin.shell: cat /path/to/file
  register: result

- name: Fail if the file does not contain the string
  ansible.builtin.debug:
    msg: "File contains the string"
  failed_when: "'specific_string' not in result.stdout"
```

#### 3. changed_when

This allows you to specify conditions under which a task should be considered changed.

```yaml
- name: Check if a file exists
  ansible.builtin.stat:
    path: /path/to/file
  register: file_stat

- name: Create the file if it does not exist
  ansible.builtin.file:
    path: /path/to/file
    state: touch
  changed_when: not file_stat.stat.exists
```

#### 4. rescue/always blocks

These blocks allow you to handle errors and run cleanup tasks.

```yaml
- name: Example of rescue and always blocks
  hosts: localhost
  tasks:
    - name: Task that might fail
      ansible.builtin.command: /bin/false
      register: result
      ignore_errors: yes

    - name: Print success message
      ansible.builtin.debug:
        msg: "Task succeeded"
      when: result.rc == 0

    - name: Handle the failure
      block:
        - name: Task that will fail
          ansible.builtin.command: /bin/false
      rescue:
        - name: Print a failure message
          ansible.builtin.debug:
            msg: "Task failed, but we are handling it"
      always:
        - name: Always run this task
          ansible.builtin.debug:
            msg: "This task runs regardless of failure"
```

### Explanation:

1. **ignore_errors**: The playbook will continue executing even if the task fails.
2. **failed_when**: Specifies custom conditions to mark a task as failed based on the task's result.
3. **changed_when**: Specifies custom conditions to mark a task as changed based on the task's result.
4. **rescue/always blocks**: Allows you to define a block of tasks that will be run if an error occurs and tasks that will always run regardless of the outcome.

These error-handling mechanisms help ensure that your playbooks are robust, can handle failures gracefully, and perform necessary cleanup or recovery actions.
