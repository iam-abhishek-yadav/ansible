**Create an Ansible Role**

- **Create a new role:**

  ```bash
  ansible-galaxy role init <role-name>
  ```

- **Ensure Your Role Structure:** First, ensure that your Ansible role directory structure is correctly organized. Here’s a typical example structure:

  ```
  my_role/
  ├── defaults/
  │   └── main.yml
  ├── files/
  ├── handlers/
  │   └── main.yml
  ├── meta/
  │   └── main.yml
  ├── tasks/
  │   └── main.yml
  ├── templates/
  ├── tests/
  │   ├── inventory
  │   └── test.yml
  └── vars/
      └── main.yml
  ```

  This structure includes directories for various aspects of your role, such as tasks, variables, handlers, templates, and tests.

- **Verify ansible-galaxy CLI:** Ensure that you have `ansible-galaxy` installed and available in your command-line interface. You can check its version to verify:

  ```bash
  ansible-galaxy --version
  ```

  If not installed, you can install it using pip:

  ```bash
  pip install ansible-galaxy-cli
  ```

- **Push Your Role to GitHub:** Navigate into your role directory and initialize a Git repository. Then, push your code to GitHub repository.

**Create a Token for Ansible Galaxy**

- **Log into Ansible Galaxy:** Go to the [Ansible Galaxy website](https://galaxy.ansible.com/) and log into your account using your credentials.

- **Create a token:** Collection >> API Token >> Load Token

**Import the Role to Ansible Galaxy**

- Once your role is on GitHub, you can import it to Ansible Galaxy using the `role import` command. This makes your role publicly available for others to discover and use:

  ```bash
  ansible-galaxy role import your_github_username my_role --token=<token_value>
  ```

**Remove a Role from Ansible Galaxy**

- To remove a role from Ansible Galaxy:

  ```bash
  ansible-galaxy role delete your_github_username my_role --token=<token_value>
  ```

**Install a Role from Ansible Galaxy**

- To install a role from Ansible Galaxy, use the following command:

  ```bash
  ansible-galaxy role install <role_name>
  ```

**List Installed Roles**

- To list the roles installed from Ansible Galaxy, you can check the `~/.ansible/roles` directory:

  ```bash
  ls ~/.ansible/roles
  ```
