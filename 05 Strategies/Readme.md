# Strategies:

control the execution flow of your playbooks. They determine how tasks are executed across multiple hosts, influencing the concurrency, order, and speed of task execution. There are three main strategies in Ansible:

1. **Linear (default)**
2. **Free**
3. **Debug**

### 1. Linear Strategy (default)
The `linear` strategy executes tasks in the order they are defined, across all hosts in the batch. This means that a task will be run on all hosts before moving on to the next task.

### 2. Free Strategy
The `free` strategy allows each host to run tasks as quickly as possible, without waiting for other hosts. This can speed up the playbook execution but might cause out-of-order task execution.

### 3. Debug Strategy
The `debug` strategy is useful for debugging playbooks. It allows you to step through each task interactively.

### Example Playbook with Different Strategies

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
---
- name: Demonstrate Ansible Strategies
  hosts: webservers
  strategy: linear  # You can change this to 'free' or 'debug'
  tasks:
    - name: Task 1 - Print hostname
      ansible.builtin.shell: echo "Task 1 running on $(hostname)"
      register: result1
      changed_when: false

    - name: Task 2 - Sleep for 5 seconds
      ansible.builtin.shell: sleep 5
      register: result2
      changed_when: false

    - name: Task 3 - Print completion message
      ansible.builtin.shell: echo "Task 3 completed on $(hostname)"
      register: result3
      changed_when: false

    - name: Show results of Task 1
      ansible.builtin.debug:
        msg: "Task 1 result: {{ result1.stdout }}"

    - name: Show results of Task 2
      ansible.builtin.debug:
        msg: "Task 2 result: {{ result2.stdout }}"

    - name: Show results of Task 3
      ansible.builtin.debug:
        msg: "Task 3 result: {{ result3.stdout }}"
```

### Explanation:

1. **Linear Strategy (default)**:
   - With the `linear` strategy, Task 1 will run on `web1` and `web2` before moving on to Task 2. Once Task 2 completes on both hosts, it will proceed to Task 3.

2. **Free Strategy**:
   - Change `strategy: linear` to `strategy: free`.
   - With the `free` strategy, each host will run through all the tasks as fast as possible. Task 2 on `web1` might finish while Task 1 is still running on `web2`.

3. **Debug Strategy**:
   - Change `strategy: linear` to `strategy: debug`.
   - With the `debug` strategy, after each task, Ansible will prompt you to continue, allowing you to debug and inspect the state between tasks.

### How to Run the Playbook:

To execute the playbook, use the following command:

```sh
ansible-playbook -i inventory playbook.yml
```

### Benefits of Each Strategy:

- **Linear Strategy**: Ensures a consistent order of execution across all hosts, making it easier to predict and manage dependencies between tasks.
- **Free Strategy**: Increases speed by allowing hosts to execute tasks independently. Useful when tasks on different hosts do not depend on each other.
- **Debug Strategy**: Ideal for troubleshooting and debugging playbooks interactively.

Choosing the right strategy depends on the specific requirements of your automation tasks and the level of control or speed you need.
