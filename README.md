# Docker Installation and Apache Deployment on Ubuntu

This Ansible playbook is designed to automate the deployment of Docker on an Ubuntu target node, followed by pulling an Apache Docker image, and configuring a Docker container to serve a webpage. It further configures a custom Docker network for the container.

## Requirements

- Ansible 2.9 or newer
- Target nodes should be Ubuntu 18.04 or newer
- SSH access to the target node(s)
- Target node(s) should have Python installed (for Ansible modules)

## Features

- Updates the apt package index.
- Installs necessary packages for Docker installation.
- Adds Docker's official GPG key.
- Sets up the stable Docker repository.
- Installs Docker Engine.
- Pulls the latest Apache Docker image.
- Creates a persistent volume directory on the host.
- Copies HTML files to the host.
- Runs an Apache container.
- Configures a custom Docker network.

## How to Use

1. Ensure you have Ansible installed on your control machine.
2. Clone this repository to your control machine.
3. Replace `node1` in the playbook with your target node's inventory name.
4. Place your HTML files in the specified source directory or update the source path in the playbook.
5. Run the playbook using the following command:

    ```
    ansible-playbook docker_deploy.yml
    ```

## Customizing the Playbook

- To target multiple nodes, update the `hosts` field in the playbook with the appropriate group or hostnames as defined in your Ansible inventory.
- If you're using a version of Ubuntu other than 18.04, ensure the `ansible_lsb.codename` variable correctly reflects your target node's Ubuntu codename.
- To serve different content, replace the source directory in the `Copy HTML files to the Host` task with the path to your HTML files.

## Networking

The playbook docker_deploy.yml configures a custom Docker network named `apache_network` with a subnet of `172.168.10.0/30` and a gateway of `172.168.10.1`. The Apache container will be connected to this network. Ensure this subnet does not conflict with existing networks in your environment.

