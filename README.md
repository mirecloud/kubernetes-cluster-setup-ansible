# Kubernetes Cluster Setup with Ansible

This repository contains Ansible playbooks for setting up and resetting a Kubernetes cluster using `kubeadm` on Ubuntu 24.04 LTS.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [Installing the Kubernetes Cluster](#installing-the-kubernetes-cluster)
  - [Resetting the Kubernetes Cluster](#resetting-the-kubernetes-cluster)
- [Playbook Details](#playbook-details)
  - [Cluster Installation](#cluster-installation)
  - [Cluster Reset](#cluster-reset)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

The playbooks automate the installation and configuration of Kubernetes on multiple nodes, including:
- Installing dependencies
- Configuring container runtime (`containerd`)
- Setting up Kubernetes repositories
- Installing `kubeadm`, `kubectl`, and `kubelet`
- Initializing the Kubernetes master node
- Configuring worker nodes to join the cluster

Additionally, a reset playbook allows for a clean reinstallation of the cluster.

## Prerequisites

- Ubuntu 24.04 LTS installed on all nodes (Master & Workers)
- Ansible installed on the control machine
- Passwordless SSH access from the control machine to all nodes
- At least 2GB RAM per node (recommended)
- Internet access on all nodes

### Installing Ansible
If Ansible is not installed, you can install it using:
```sh
sudo apt update && sudo apt install ansible -y
```

Ensure all target machines are reachable via SSH:
```sh
ansible all -m ping
```

## Setup Instructions

### Installing the Kubernetes Cluster
1. Clone this repository:
    ```sh
    git clone https://github.com/yourusername/k8s-ansible-setup.git
    cd k8s-ansible-setup
    ```
2. Update the `inventory` file with the IP addresses or hostnames of your master and worker nodes.
3. Run the installation playbook:
    ```sh
    ansible-playbook -i inventory Cluster_installation.yaml
    ```
4. After successful installation, your cluster will be ready for use.

### Resetting the Kubernetes Cluster
If you need to reset the cluster, run the following command:
```sh
ansible-playbook -i inventory Cluster_reset.yaml
```
This will clean up the existing Kubernetes setup and allow a fresh installation.

## Playbook Details

### Cluster Installation
- **File:** `Cluster_installation.yaml`
- **Tasks Included:**
  - System update & upgrade
  - Installation of dependencies (`containerd`, Kubernetes components)
  - Configuration of `containerd`
  - Kubernetes repository setup
  - Kubernetes master node initialization
  - Worker node joining process

### Cluster Reset
- **File:** `Cluster_reset.yaml`
- **Tasks Included:**
  - Uninstall Kubernetes components
  - Reset cluster using `kubeadm reset`
  - Remove Kubernetes configuration files
  - Reinstall the cluster from scratch

## Contributing

Contributions are welcome! If you'd like to improve these playbooks, feel free to fork the repository and submit a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

