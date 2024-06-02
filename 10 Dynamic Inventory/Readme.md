## Dynamic inventory:

- in Ansible refers to the capability of sourcing inventory from external scripts or programs, which allows for more flexible and scalable management of hosts and groups. Unlike static inventory files, which list hosts and groups in a fixed format, dynamic inventories can be generated on-the-fly, reflecting changes in the environment, such as cloud infrastructure.

### How Dynamic Inventory Works
Ansible uses executable scripts or programs to generate inventory data. These scripts output JSON-formatted data that Ansible can interpret. Dynamic inventory scripts can pull data from various sources, including cloud providers (AWS, Azure, GCP), CMDBs, databases, or any other system that can produce the required information.

### Basic Structure of a Dynamic Inventory Script

A dynamic inventory script must produce JSON output in a specific format. Here’s a simple example of the required JSON structure:

```json
{
  "all": {
    "hosts": ["host1", "host2"],
    "vars": {
      "var1": "value1"
    }
  },
  "_meta": {
    "hostvars": {
      "host1": {
        "ansible_host": "192.168.1.10"
      },
      "host2": {
        "ansible_host": "192.168.1.11"
      }
    }
  }
}
```

### Example: Dynamic Inventory Script with AWS EC2

Below is an example of how you might set up a dynamic inventory script to source hosts from AWS EC2. Ansible provides an AWS EC2 dynamic inventory script that you can use as a starting point.

1. **Install Required Packages**
   First, you need to install `boto3` and `botocore`, which are Python packages used to interact with AWS:

   ```bash
   pip install boto3 botocore
   ```

2. **Download AWS EC2 Inventory Script**
   Ansible provides an example EC2 inventory script in their GitHub repository. Download it:

   ```bash
   wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py
   chmod +x ec2.py
   ```

3. **Configure AWS Credentials**
   Ensure your AWS credentials are set up properly. You can do this via the AWS CLI or by setting environment variables:

   ```bash
   export AWS_ACCESS_KEY_ID='your_access_key'
   export AWS_SECRET_ACCESS_KEY='your_secret_key'
   export AWS_REGION='your_region'
   ```

4. **Configure Ansible to Use the Script**
   Create a file named `ansible.cfg` in your project directory to configure Ansible to use the dynamic inventory script:

   ```ini
   [defaults]
   inventory = ./ec2.py
   ```

5. **Run Ansible Commands**
   Now you can run Ansible commands, and it will use the dynamic inventory script to fetch the current inventory from AWS EC2.

   ```bash
   ansible all -m ping
   ```

### Custom Dynamic Inventory Script Example

Here's a simple example of a custom dynamic inventory script written in Python:

```python
#!/usr/bin/env python3

import json

def main():
    inventory = {
        "all": {
            "hosts": ["host1.example.com", "host2.example.com"],
            "vars": {
                "example_variable": "value"
            }
        },
        "_meta": {
            "hostvars": {
                "host1.example.com": {
                    "ansible_host": "192.168.1.10"
                },
                "host2.example.com": {
                    "ansible_host": "192.168.1.11"
                }
            }
        }
    }

    print(json.dumps(inventory))

if __name__ == "__main__":
    main()
```

Make the script executable:

```bash
chmod +x my_dynamic_inventory.py
```

Configure Ansible to use the custom script:

```ini
# ansible.cfg
[defaults]
inventory = ./my_dynamic_inventory.py
```

Now, you can run Ansible commands, and it will use your custom script for inventory:

```bash
ansible all -m ping
```

### Conclusion

Dynamic inventory in Ansible allows you to generate your inventory dynamically from various sources, making it more flexible and suitable for environments that change frequently, such as cloud infrastructure. By using dynamic inventory scripts, you can automate the process of keeping your inventory up-to-date, ensuring that your playbooks always target the correct hosts.
