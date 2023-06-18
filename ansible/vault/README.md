#### playbook_without_vault.yml

```
---
- name: Playbook without Vault
  hosts: all
  vars:
    mypassword: mysupersecretpassword
  tasks:
    - name: print variable
      ansible.builtin.debug:
        var: mypassword
        
```

```
ansible-playbook playbook_without_vault.yml
```

#### Create an encrypted file to store the database credentials:

```
ansible-vault create mypassword.yml
```
Enter and confirm a password for the vault.

The encrypted file will open in the default text editor. Add the following content in YAML format:
```
mypassword: mysupersecretpassword

```
Save and close the file.

#### encrypted file using the vars_files directive: playbook_with_vault.yml 
```
---
- name: Playbook with Vault
  hosts: all
  tasks:
    - name: include vault
      ansible.builtin.include_vars:
        file: mypassword.yml

    - name: print variable
      ansible.builtin.debug:
        var: mypassword
      #no_log: true  

When running the playbook, provide the vault password using the --ask-vault-pass option:

```
ansible-playbook --ask-vault-password playbook_with_vault.yml
```

#### Ansible will automatically decrypt the file and make the variables available to your playbook.

```
ansible-vault decrypt encrypted_file.yml

```

