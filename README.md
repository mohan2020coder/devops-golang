devops demo ansible, jenkins, sonarqube sonarscanner


https://youtu.be/Bgv4C0buCsU?si=qaVo1oQfJqcd4VfP




# Installing and Configuring Ansible on Ubuntu

## Installing Ansible

1. **Add the Ansible PPA (Personal Package Archive) and install Ansible:**

    ```sh
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install ansible -y
    ```

2. **Verify the installation:**

    ```sh
    ansible --version
    ```

    This should show the version of Ansible installed along with the location of its configuration file.

## Creating Configuration Directory and Files

If the `/etc/ansible/` directory does not exist, you can create it manually:

1. **Create the directory:**

    ```sh
    sudo mkdir -p /etc/ansible
    ```

2. **Create the main configuration file and inventory file if they do not exist:**

    ```sh
    sudo touch /etc/ansible/ansible.cfg
    sudo touch /etc/ansible/hosts
    ```

3. **Set up basic configuration:**

    You can start with a basic configuration in the `ansible.cfg` file. Open it with a text editor:

    ```sh
    sudo nano /etc/ansible/ansible.cfg
    ```

    Add the following basic configuration:

    ```ini
    [defaults]
    inventory = /etc/ansible/hosts
    ```

4. **Add some inventory to the `hosts` file:**

    ```sh
    sudo nano /etc/ansible/hosts
    ```

    Add the following content to define a simple inventory:

    ```ini
    [local]
    localhost ansible_connection=local
    ```

## Verify the Configuration

You can verify that Ansible is correctly reading the configuration and inventory files:

1. **Check the configuration:**

    ```sh
    ansible --version
    ```

    Ensure it points to `/etc/ansible/ansible.cfg`.

2. **List the inventory:**

    ```sh
    ansible all --list-hosts
    ```

    This should show the hosts listed in your `/etc/ansible/hosts` file.

Following these steps should ensure that Ansible is installed correctly and its configuration directory is set up properly.
