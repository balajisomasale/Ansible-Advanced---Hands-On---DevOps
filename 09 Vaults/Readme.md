## Ansible Vault:

It is a feature within Ansible that allows you to encrypt and decrypt sensitive data, such as passwords or keys, so they can be stored in version control or shared securely without exposing the plain text values. This is particularly useful in scenarios where you need to manage sensitive information but want to avoid exposing it directly in your playbooks or inventory files.

### How Ansible Vault Works
Ansible Vault encrypts files using a password. When you want to use the encrypted data, you need to provide the same password to decrypt it. You can encrypt entire files or just variables within playbooks.

### Basic Commands

1. **Encrypting a file**:
   ```bash
   ansible-vault encrypt <filename>
   ```
   This command will prompt you to enter a password and will then encrypt the specified file.

2. **Decrypting a file**:
   ```bash
   ansible-vault decrypt <filename>
   ```
   This command will prompt you to enter the password used to encrypt the file and will then decrypt it.

3. **Editing an encrypted file**:
   ```bash
   ansible-vault edit <filename>
   ```
   This command allows you to edit the encrypted file. The file will be decrypted temporarily for editing and then re-encrypted after you save and exit.

4. **Viewing an encrypted file**:
   ```bash
   ansible-vault view <filename>
   ```
   This command allows you to view the contents of an encrypted file without decrypting it permanently.

5. **Encrypting variables within a playbook**:
   ```bash
   ansible-vault encrypt_string '<string>' --name '<variable_name>'
   ```
   This command encrypts a single string, which can then be included in your playbooks or variable files.

### Example

#### Step 1: Encrypting a File

Suppose you have a file called `secrets.yml` that contains sensitive information like this:

```yaml
# secrets.yml
db_password: mysecretpassword
api_key: myapikey
```

To encrypt this file, run:

```bash
ansible-vault encrypt secrets.yml
```

You will be prompted to enter a password. After encryption, the contents of `secrets.yml` will be replaced with an encrypted version.

#### Step 2: Using Encrypted File in Playbook

In your playbook, you can reference the encrypted variables like this:

```yaml
# playbook.yml
- hosts: localhost
  vars_files:
    - secrets.yml

  tasks:
    - name: Print the database password
      debug:
        msg: "The database password is {{ db_password }}"

    - name: Print the API key
      debug:
        msg: "The API key is {{ api_key }}"
```

#### Step 3: Running the Playbook

When you run the playbook, you need to provide the vault password so that Ansible can decrypt the variables:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

You will be prompted to enter the vault password. If the password is correct, Ansible will decrypt `secrets.yml` and use the variables in your playbook.

### Example with Encrypted Variables

You can also encrypt individual variables directly:

```bash
ansible-vault encrypt_string 'mysecretpassword' --name 'db_password'
```

This will output an encrypted string that you can include directly in your playbooks:

```yaml
# playbook.yml
- hosts: localhost
  vars:
    db_password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          62353538336233653032333433363561366266323638386137663631366161373362353132383535
          ...

  tasks:
    - name: Print the database password
      debug:
        msg: "The database password is {{ db_password }}"
```

When you run this playbook, you will need to provide the vault password as before:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

### Conclusion

Ansible Vault is a powerful tool for managing sensitive information in your automation scripts securely. By encrypting files and variables, you can safely store and share sensitive data without exposing it to unauthorized users.
