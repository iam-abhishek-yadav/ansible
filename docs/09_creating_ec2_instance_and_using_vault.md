**Setup EC2 Collection and Authentication**

- **Install boto3**

  ```bash
  pip install boto3
  ```

- **Install AWS Collection**

  ```bash
  ansible-galaxy collection install amazon.aws
  ```

- **Setup Vault for AWS Credentials**

  - `Create a Password for Vault` : Generate a strong password to use with Ansible Vault. This password will be needed to encrypt and decrypt sensitive data (like AWS credentials):

    ```bash
    openssl rand -base64 2048 > vault.pass
    ```

  - `Add AWS Credentials to Vault` : Create a vault file (`pass.yml`) and add your AWS credentials securely:

    ```bash
    ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
    ```

    ```yaml
    aws_access_key: YOUR_ACCESS_KEY_HERE
    aws_secret_key: YOUR_SECRET_KEY_HERE
    ```

  Save and close the vault file (`pass.yml`). Remember to keep `vault.pass` (the password file) secure and accessible only to authorized users or processes.

- **Create a Blank `inventory.ini` File**

  ```bash
  touch inventory.ini
  ```

- **Run Ansible Playbook with Vault**

  Example `playbook.yml`:

  ```yaml
  ---
  - hosts: localhost
    connection: local
    tasks:
      - name: start an instance with a public IP address
        amazon.aws.ec2_instance:
          name: 'ansible-instance'
          instance_type: t2.micro
          security_group: default
          region: us-east-1
          aws_access_key: '{{ aws_access_key }}'
          aws_secret_key: '{{ aws_secret_key }}'
          network:
            assign_public_ip: true
          image_id: ami-04b70fa74e45c3917
  ```

- **Execute the Playbook**

  ```bash
  ansible-playbook playbook.yml --inventory inventory.ini --vault-password-file vault.pass
  ```
