# Asynchronous functions

Asynchronous functions in Ansible allow you to execute tasks in the background, enabling other tasks to continue running without waiting for the asynchronous task to complete. This is particularly useful when dealing with tasks that can take a long time to finish, such as lengthy installations or large data transfers.

### How Asynchronous Tasks Work

1. **Launch the Task Asynchronously**: You specify a timeout and a polling interval for the task.
2. **Check Task Status**: Optionally, you can wait for the task to complete or check its status later.

### Key Parameters

- `async`: Specifies the maximum amount of time (in seconds) to wait for the task to complete.
- `poll`: Specifies how often (in seconds) to check the status of the task. A value of `0` means not to wait.

### Example

Here’s an example demonstrating the use of asynchronous tasks in Ansible:

#### Directory Structure:

```plaintext
my_playbook/
├── playbook.yml
└── inventory
```

#### inventory

```ini
[webservers]
web1.example.com
web2.example.com
```

#### playbook.yml

```yaml
- name: Run asynchronous tasks
  hosts: webservers
  tasks:
    - name: Start a long-running job
      command: /usr/bin/some_long_running_command
      async: 3600
      poll: 0
      register: long_running_job

    - name: Check if the long-running job has finished
      async_status:
        jid: "{{ long_running_job.ansible_job_id }}"
      register: job_result
      until: job_result.finished
      retries: 30
      delay: 60

    - name: Output the result
      debug:
        msg: "The job has completed with result: {{ job_result }}"
```

### Explanation:

1. **Starting the Asynchronous Task**:
    ```yaml
    - name: Start a long-running job
      command: /usr/bin/some_long_running_command
      async: 3600
      poll: 0
      register: long_running_job
    ```
    - `command`: Executes the specified command.
    - `async: 3600`: Allows up to 3600 seconds (1 hour) for the command to complete.
    - `poll: 0`: Tells Ansible not to wait for the command to finish immediately.
    - `register: long_running_job`: Captures the job details, including the job ID.

2. **Checking the Task Status**:
    ```yaml
    - name: Check if the long-running job has finished
      async_status:
        jid: "{{ long_running_job.ansible_job_id }}"
      register: job_result
      until: job_result.finished
      retries: 30
      delay: 60
    ```
    - `async_status`: Checks the status of the asynchronous job using the job ID.
    - `register: job_result`: Captures the result of the status check.
    - `until: job_result.finished`: Continues checking until the job is finished.
    - `retries: 30`: Retries the status check up to 30 times.
    - `delay: 60`: Waits 60 seconds between retries.

3. **Outputting the Result**:
    ```yaml
    - name: Output the result
      debug:
        msg: "The job has completed with result: {{ job_result }}"
    ```
    - `debug`: Outputs the final result of the job.

### Benefits of Asynchronous Tasks:

- **Efficiency**: Other tasks can proceed while the asynchronous task runs in the background.
- **Scalability**: Particularly useful in large-scale environments where multiple long-running tasks can be executed concurrently.
- **Resource Management**: Prevents blocking of playbook execution due to long-running tasks.

Using asynchronous tasks in Ansible is a powerful way to manage long-running operations, ensuring that your automation processes remain efficient and responsive.
