devops demo ansible, jenkins, sonarqube sonarscanner


https://youtu.be/Bgv4C0buCsU?si=qaVo1oQfJqcd4VfP


https://get.jenkins.io/debian-stable/




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




# Docker Installation Guide for Ubuntu

This guide provides step-by-step instructions to install Docker on an Ubuntu system.

## Prerequisites

- Ubuntu system with `sudo` privileges.
- Internet connectivity to download packages.

# Docker Installation Guide for Ubuntu

This guide provides step-by-step instructions to install Docker on an Ubuntu system.

## Prerequisites

- Ubuntu system with `sudo` privileges.
- Internet connectivity to download packages.

## Step-by-Step Installation

```bash
# 1. Install Required Packages
sudo apt-get update && \
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common && \

# 2. Add Docker's Official GPG Key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \

# 3. Set Up the Docker Repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \

# 4. Install Docker Engine
sudo apt-get update && \
sudo apt-get install -y docker-ce docker-ce-cli containerd.io && \

# 5. Verify Docker Installation
sudo docker --version && \

# 6. Start Docker Service
sudo service docker start && \

# 7. Test Docker
sudo docker run hello-world
