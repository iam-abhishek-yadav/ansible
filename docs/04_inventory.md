### Ansible Inventory

The Ansible inventory file specifies remote hosts and their groups for management, supporting both static and dynamic formats.

- **Static Inventory**
  
  Static inventory files are manually created plain text files that define hosts and their groupings.

  - **INI Format**
    ```ini
    # inventory file: hosts

    [webservers]
    web1.example.com
    web2.example.com

    [dbservers]
    db1.example.com
    db2.example.com

    [all:vars]
    ansible_user=admin
    ansible_ssh_private_key_file=/path/to/key
    ```

    **Explanation**: 
    - `[webservers]`, `[dbservers]`: Groups of servers with their respective hostnames.
    - `[all:vars]`: Global variables applicable to all hosts, such as the Ansible user and SSH private key file path.

  - **YAML Format**
    ```yaml
    # inventory file: hosts.yaml

    all:
      vars:
        ansible_user: admin
        ansible_ssh_private_key_file: /path/to/key
      children:
        webservers:
          hosts:
            web1.example.com:
            web2.example.com:
        dbservers:
          hosts:
            db1.example.com:
            db2.example.com:
    ```

    **Explanation**:
    - `all`: Top-level group containing all hosts and their variables.
    - `vars`: Global variables for all hosts.
    - `children`: Groups of hosts categorized under `webservers` and `dbservers`.
    - `hosts`: Lists of specific hosts under each group.

- **Dynamic Inventory**
  
  Dynamic inventories are generated programmatically by scripts or plugins, ideal for environments with dynamically changing hosts.

  - **Example Script for AWS EC2 (Python)**
    ```python
    #!/usr/bin/env python

    import json
    import boto3

    def get_aws_ec2_inventory():
        ec2 = boto3.client('ec2')
        instances = ec2.describe_instances()
        inventory = {
            'all': {
                'hosts': [],
                'vars': {
                    'ansible_user': 'ec2-user',
                    'ansible_ssh_private_key_file': '/path/to/key'
                }
            },
            '_meta': {
                'hostvars': {}
            }
        }

        for reservation in instances['Reservations']:
            for instance in reservation['Instances']:
                if instance['State']['Name'] == 'running':
                    public_ip = instance['PublicIpAddress']
                    inventory['all']['hosts'].append(public_ip)
                    inventory['_meta']['hostvars'][public_ip] = {
                        'ansible_host': public_ip
                    }

        print(json.dumps(inventory, indent=2))

    if __name__ == '__main__':
        get_aws_ec2_inventory()
    ```

    **Explanation**:
    - This Python script utilizes the Boto3 library to fetch EC2 instances from AWS.
    - It constructs an inventory dictionary in JSON format containing `all` hosts with their respective variables (`ansible_user` and `ansible_ssh_private_key_file`).
    - The `_meta` section stores host-specific variables (`ansible_host` for each EC2 instance's public IP).

### Usage

To use the inventory file, execute Ansible commands as shown:

```sh
ansible-playbook -i inventory <adhoc command or playbook.yml>
```
