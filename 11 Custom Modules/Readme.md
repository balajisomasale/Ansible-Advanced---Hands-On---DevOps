## Custom modules in Ansible:

are user-defined modules that extend Ansible's functionality beyond the built-in modules. Custom modules allow you to create your own logic and operations that can be used just like any other Ansible module in your playbooks. This can be particularly useful when you need to automate tasks that are not covered by Ansible’s standard modules.

### Structure of a Custom Ansible Module

A custom Ansible module is typically written in Python, but you can use any language that can return JSON output. The module should:

1. Accept input parameters.
2. Perform the desired operations.
3. Return results in JSON format.

### Basic Example: A Custom Module in Python

Here's a step-by-step guide to creating a simple custom Ansible module in Python.

#### Step 1: Create the Module File

Create a file named `my_module.py`. This script will serve as your custom module.

```python
#!/usr/bin/python

from ansible.module_utils.basic import AnsibleModule

def main():
    # Define the module's argument/spec
    module_args = dict(
        name=dict(type='str', required=True)
    )

    # Create the Ansible module instance
    module = AnsibleModule(
        argument_spec=module_args,
        supports_check_mode=True
    )

    # Retrieve the parameters
    name = module.params['name']

    # Perform the operation (in this case, just create a simple message)
    message = f"Hello, {name}!"

    # Exit the module with the result
    module.exit_json(changed=False, message=message)

if __name__ == '__main__':
    main()
```

This custom module accepts a single parameter `name` and returns a greeting message.

#### Step 2: Create a Playbook to Use the Custom Module

Create a playbook named `test_custom_module.yml` to test the custom module.

```yaml
---
- name: Test custom module
  hosts: localhost
  tasks:
    - name: Use custom module
      my_module:
        name: "Ansible User"
      register: result

    - name: Print result
      debug:
        msg: "{{ result.message }}"
```

#### Step 3: Configure the Module Library Path

Ansible needs to know where to find your custom module. You can specify the path in your playbook or configuration file. Here, we'll specify it in the playbook.

```yaml
---
- name: Test custom module
  hosts: localhost
  tasks:
    - name: Use custom module
      my_module:
        name: "Ansible User"
      register: result
      module_defaults:
        my_module:
          library: ./library

    - name: Print result
      debug:
        msg: "{{ result.message }}"
```

Ensure that your `my_module.py` is placed in the `./library` directory.

#### Step 4: Run the Playbook

Run the playbook to see your custom module in action.

```bash
ansible-playbook test_custom_module.yml
```

### Output

The output should look something like this:

```plaintext
PLAY [Test custom module] ******************************************************************

TASK [Gathering Facts] *********************************************************************
ok: [localhost]

TASK [Use custom module] *******************************************************************
ok: [localhost]

TASK [Print result] ************************************************************************
ok: [localhost] => {
    "msg": "Hello, Ansible User!"
}

PLAY RECAP *********************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### Conclusion

Creating custom modules in Ansible allows you to extend its functionality to cover specific needs that are not addressed by the built-in modules. By following the structure of accepting parameters, performing operations, and returning results in JSON format, you can integrate your custom logic seamlessly into your Ansible workflows.
