- **[Generate Vault Password](../docs/09_creating_ec2_instance_and_using_vault.md)**
- **Run Playbook to Create Instances:**

  ```yaml
  ansible-playbook create.yml -i inventory.ini --vault-password-file vault.pass
  ```

- **Retrieve Instance IPs and Configure Inventory:**

  - Obtain the IP addresses of the newly created instances from your AWS Management Console or via Ansible dynamic inventory scripts.

- **[Set Up Passwordless Authentication](../docs/03_passwordless_authentication.md)**

- **Shutdown Instances:**
  ```yaml
  ansible-playbook shutdown.yml -i inventory.ini --vault-password-file vault.pass
  ```
