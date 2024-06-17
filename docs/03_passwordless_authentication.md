
### How to Set Up Passwordless Authentication

#### Using Public Key

To set up passwordless authentication on EC2 instances using a public key, follow these steps:

- **Copy Your Public Key to the Remote Machine**: 
  Use the `ssh-copy-id` command to copy your public key to the remote EC2 instance.

  ```sh
  ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
  ```

  - **ssh-copy-id**: Command used to copy your public key to a remote machine.
  - **-f**: Forces the copying of keys, useful if you need to overwrite existing keys.
  - **"-o IdentityFile <PATH TO PEM FILE>"**: Specifies the identity file (private key) for the connection. The `-o` flag passes this option to the underlying `ssh` command.
  - **ubuntu@<INSTANCE-IP>**: Represents the username (e.g., `ubuntu`) and the public IP address of the remote EC2 instance.

  **Common Issue**:
  If you encounter the error `/usr/bin/ssh-copy-id: ERROR: No identities found`, it means that no public key is available to copy. Here's how to resolve it:

  - **Check for .ssh Directory**: 
    If the `.ssh` directory does not exist, create it using the `ssh-keygen` command.

    ```sh
    ssh-keygen
    ```

    Follow the prompts, and if you want to use the default path (`~/.ssh/id_rsa`), simply press `Enter`.

  - **Set Correct Permissions**: 
    If you get a "bad permission" warning, set the correct permissions for the PEM file.

    ```sh
    chmod 600 <PATH TO PEM FILE>
    ```

#### Using Password

To set up password-based authentication on EC2 instances, follow these steps:

- **Edit SSH Configuration**: 
  Open the SSH configuration file and update the settings.

  ```sh
  sudo nano /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
  ```

  Locate the line for `PasswordAuthentication` and change it to:

  ```sh
  PasswordAuthentication yes
  ```

  If you are not using an EC2 instance, open the SSH configuration file directly:

  ```sh
  sudo vi /etc/ssh/sshd_config
  ```

  Locate the line for `PasswordAuthentication` and uncomment it (remove the `#` at the beginning) and set it to `yes`:

  ```sh
  PasswordAuthentication yes
  ```

- **Set User Password**: 
  Create a password for the `ubuntu` user.

  ```sh
  sudo passwd ubuntu
  ```

- **Restart SSH Service**: 
  After updating the configuration, restart the SSH service to apply the changes.

  ```sh
  sudo systemctl restart ssh
  ```

- **Copy Public Key Using Password**: 
  Log out and use the `ssh-copy-id` command to copy your public key, providing the password when prompted.

  ```sh
  ssh-copy-id ubuntu@<INSTANCE-IP>
  ```

- **Login Using Public Key**: 
  After the public key is copied, you can log in using SSH without a password.

  ```sh
  ssh ubuntu@<INSTANCE-IP>
  ```
