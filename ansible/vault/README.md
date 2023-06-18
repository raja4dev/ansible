#### Create an encrypted file to store the database credentials:

```
ansible-vault create database_credentials.yml

```
Enter and confirm a password for the vault.

The encrypted file will open in the default text editor. Add the following content in YAML format:
```
database_host: localhost
database_port: 3306
database_name: mydb
database_user: myuser
database_password: mysecretpassword
```
Save and close the file.

#### encrypted file using the vars_files directive:
```
- hosts: web
  vars_files:
    - path/to/database_credentials.yml

  tasks:
    - name: Configure database
      mysql_db:
        name: "{{ database_name }}"
        state: present
```

When running the playbook, provide the vault password using the --ask-vault-pass option:

```
ansible-playbook myplaybook.yml --ask-vault-pass

```
Ansible will automatically decrypt the file and make the variables available to your playbook.
