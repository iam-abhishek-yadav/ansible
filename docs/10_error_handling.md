- **Ignoring Errors (`ignore_errors: yes`)**

  - **Purpose:** Allows tasks to continue executing even if errors occur.
  - **Usage:**
    ```yaml
    - name: Install packages
      ansible.builtin.apt:
        name: '{{ item }}'
        state: latest
      loop:
        - openssl
        - openssh
      ignore_errors: yes
    ```
    - In this example, `ignore_errors: yes` ensures that the playbook continues to execute even if the installation of `openssl` or `openssh` fails.

- **Registering and Handling Command Output**

  - **Purpose:** Captures command output and allows conditional logic based on the command result.
  - **Usage:**
    ```yaml
    - name: Check if package is installed
      ansible.builtin.command: dpkg -l | grep docker
      register: docker_check
      ignore_errors: yes
    ```
    - `register: docker_check` captures the result of the command, which can be used later for decision-making.

- **Conditional Task Execution (`when`)**

  - **Purpose:** Executes tasks conditionally based on previous task results or variables.
  - **Usage:**
    ```yaml
    - name: Install Docker
      ansible.builtin.apt:
        name: docker.io
        state: present
      when: docker_check.rc != 0
    ```
    - Here, `when: docker_check.rc != 0` ensures that Docker (`docker.io`) is installed only if the previous `docker_check` command failed (exit code not zero).

- **Handling Errors with `failed_when`**

  - **Purpose:** Explicitly defines conditions under which a task should fail.
  - **Usage:**
    ```yaml
    - name: Run a critical script
      ansible.builtin.shell: /path/to/critical_script.sh
      register: script_output
      failed_when: "'Error' in script_output.stdout"
    ```
    - `failed_when: "'Error' in script_output.stdout"` ensures that the task fails if the word 'Error' is found in the script output.

- **Debugging and Troubleshooting (`ansible.builtin.debug`)**

  - **Purpose:** Provides visibility into variable values and task outputs for debugging.
  - **Usage:**
    ```yaml
    - ansible.builtin.debug:
        var: script_output
    ```
