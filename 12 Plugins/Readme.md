# Plugins in Ansible:

There are pieces of code that augment the core functionality of Ansible, allowing you to customize and extend how Ansible operates. There are several types of plugins, each serving different purposes within Ansible's ecosystem. Here are some of the most commonly used types of plugins along with examples:

1. **Action Plugins**
2. **Callback Plugins**
3. **Lookup Plugins**
4. **Filter Plugins**
5. **Connection Plugins**
6. **Inventory Plugins**

### 1. Action Plugins
Action plugins define actions to be taken in a playbook, typically extending or overriding the behavior of existing modules.

**Example: Custom Action Plugin**
Create a custom action plugin to modify the behavior of the `command` module.

**File: `action_plugins/my_command.py`**

```python
from ansible.plugins.action import ActionBase

class ActionModule(ActionBase):
    def run(self, tmp=None, task_vars=None):
        result = super(ActionModule, self).run(tmp, task_vars)
        # Custom behavior here
        result.update({
            'changed': False,
            'stdout': 'Custom action executed',
        })
        return result
```

**Playbook: `test_action_plugin.yml`**

```yaml
- name: Test custom action plugin
  hosts: localhost
  tasks:
    - name: Run custom command
      my_command:
        cmd: echo "Hello World"
```

### 2. Callback Plugins
Callback plugins respond to events in the Ansible execution process, such as on task start, task completion, or playbook completion.

**Example: Custom Callback Plugin**
Create a custom callback plugin to print a message after each task.

**File: `callback_plugins/my_callback.py`**

```python
from ansible.plugins.callback import CallbackBase

class CallbackModule(CallbackBase):
    def v2_runner_on_ok(self, result):
        self._display.display("Task {} succeeded".format(result.task_name))
```

**Configuration: `ansible.cfg`**

```ini
[defaults]
callback_whitelist = my_callback
```

### 3. Lookup Plugins
Lookup plugins fetch data from external sources. They are used to get values from files, databases, or other systems.

**Example: Custom Lookup Plugin**
Create a custom lookup plugin to read a specific file.

**File: `lookup_plugins/my_lookup.py`**

```python
from ansible.plugins.lookup import LookupBase

class LookupModule(LookupBase):
    def run(self, terms, variables=None, **kwargs):
        with open(terms[0], 'r') as file:
            return [file.read()]
```

**Playbook: `test_lookup_plugin.yml`**

```yaml
- name: Test custom lookup plugin
  hosts: localhost
  tasks:
    - name: Read from file
      debug:
        msg: "{{ lookup('my_lookup', 'path/to/file.txt') }}"
```

### 4. Filter Plugins
Filter plugins are used to transform data inside templates.

**Example: Custom Filter Plugin**
Create a custom filter plugin to reverse a string.

**File: `filter_plugins/my_filters.py`**

```python
class FilterModule(object):
    def filters(self):
        return {
            'reverse_string': self.reverse_string,
        }

    def reverse_string(self, value):
        return value[::-1]
```

**Playbook: `test_filter_plugin.yml`**

```yaml
- name: Test custom filter plugin
  hosts: localhost
  tasks:
    - name: Reverse a string
      debug:
        msg: "{{ 'Hello World' | reverse_string }}"
```

### 5. Connection Plugins
Connection plugins handle communication between the control machine and the target hosts.

**Example: Custom Connection Plugin**
Create a custom connection plugin to print a message when connecting.

**File: `connection_plugins/my_connection.py`**

```python
from ansible.plugins.connection import ConnectionBase

class Connection(ConnectionBase):
    def __init__(self, *args, **kwargs):
        super(Connection, self).__init__(*args, **kwargs)
        self._connected = False

    def connect(self):
        super(Connection, self).connect()
        self._connected = True
        self._display.display("Connecting to host")

    def exec_command(self, cmd, in_data=None, sudoable=True):
        return super(Connection, self).exec_command(cmd, in_data, sudoable)
```

**Configuration: `ansible.cfg`**

```ini
[defaults]
connection_plugins = /path/to/your/connection_plugins
```

**Playbook: `test_connection_plugin.yml`**

```yaml
- name: Test custom connection plugin
  hosts: localhost
  tasks:
    - name: Test command
      command: echo "Hello World"
      delegate_to: localhost
      connection: my_connection
```

### 6. Inventory Plugins
Inventory plugins allow dynamic generation of inventory from various sources, such as cloud providers, databases, etc.

**Example: Custom Inventory Plugin**
Create a custom inventory plugin to generate inventory from a JSON file.

**File: `inventory_plugins/my_inventory.py`**

```python
from ansible.plugins.inventory import BaseInventoryPlugin

class InventoryModule(BaseInventoryPlugin):
    NAME = 'my_inventory'

    def verify_file(self, path):
        return path.endswith('.json')

    def parse(self, inventory, loader, path, cache=True):
        with open(path) as file:
            data = json.load(file)
            for host in data['hosts']:
                inventory.add_host(host)
```

**Configuration: `ansible.cfg`**

```ini
[defaults]
inventory_plugins = /path/to/your/inventory_plugins
```

**Inventory File: `inventory.json`**

```json
{
  "hosts": ["host1", "host2"]
}
```

**Playbook: `test_inventory_plugin.yml`**

```yaml
- name: Test custom inventory plugin
  hosts: all
  tasks:
    - name: Test
      debug:
        msg: "This is a custom inventory plugin test."
```

### Conclusion

Plugins in Ansible provide a powerful way to extend its functionality. By writing custom plugins, you can tailor Ansible to meet specific needs that go beyond the capabilities of built-in modules and plugins. Each type of plugin serves a different purpose, and understanding these can help you leverage Ansible more effectively in your automation tasks.
