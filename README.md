# Terraform Module: On-Premise K3s Cluster

This repository provides a Terraform module designed for provisioning and managing an on-premise K3s (Kubernetes) cluster. It encapsulates the configuration necessary to deploy a lightweight, yet powerful, Kubernetes environment on your own infrastructure, leveraging Terraform's Infrastructure as Code (IaC) capabilities.

## Project Structure

- `main.tf`: The primary Terraform configuration file, defining the resources and logic required to set up the K3s cluster. This may include VM provisioning, network configuration, and K3s installation commands.
- `variables.tf`: Defines input variables for the Terraform configuration, allowing for customization such as the number of nodes, operating system, or K3s version.
- `outputs.tf`: Defines output values from the Terraform configuration, such as cluster endpoints, Kubeconfig details, or node IPs, which can be used by other systems or for further configuration.
- `README.md`: This file, providing an overview, setup, and usage instructions.

## How It Works

This Terraform module automates the deployment of a K3s Kubernetes cluster on-premise. Depending on the `main.tf` implementation, it typically involves:

1.  **Infrastructure Provisioning:** Creating virtual machines (using providers like `libvirt`, `vsphere`, or `Proxmox`) or configuring existing physical servers.
2.  **Network Setup:** Configuring networking, firewalls, and connectivity for the cluster nodes.
3.  **K3s Installation:** Executing commands (often via `remote-exec` or `cloud-init`) to install and initialize K3s on the provisioned nodes.
4.  **Configuration Retrieval:** Extracting necessary information (like the `kubeconfig` file) to interact with the newly deployed K3s cluster.

## Prerequisites

Before using this Terraform module, ensure you have:

*   **Terraform Installed:** Terraform CLI installed on your local machine.
*   **On-Premise Infrastructure:** Access to your on-premise virtualization platform (e.g., KVM/libvirt, VMware vSphere, Proxmox) or bare-metal servers.
*   **Provider Configuration:** Appropriate Terraform providers configured for your on-premise infrastructure (e.g., `libvirt`, `vsphere`, `null_resource` with `local-exec`/`remote-exec`).
*   **SSH Access:** SSH keys and credentials configured for accessing target nodes.

## Getting Started

Follow these general steps to deploy an on-premise K3s cluster:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/samuelngarciar/terraform-onpremise-k3s.git
    cd terraform-onpremise-k3s
    ```
2.  **Configure Variables:**
    *   Review `variables.tf` and create a `terraform.tfvars` file (or use `-var` flags) to provide values for your specific environment (e.g., VM sizes, network settings, SSH keys).
3.  **Initialize Terraform:**
    ```bash
    terraform init
    ```
4.  **Review the plan:**
    ```bash
    terraform plan
    ```
    This command shows you what actions Terraform will take. Review it carefully.
5.  **Apply the configuration:**
    ```bash
    terraform apply
    ```
    Type `yes` when prompted to confirm the deployment.
6.  **Retrieve Outputs:** After successful application, retrieve important information:
    ```bash
    terraform output
    ```
7.  **Destroy the cluster (when no longer needed):**
    ```bash
    terraform destroy
    ```
    Type `yes` when prompted to confirm the destruction.

## Customization

The module is designed to be flexible. You can customize the cluster size, node specifications, networking, and K3s-specific configurations by adjusting the input variables.

## Contribution

Feel free to fork this repository, make improvements, and submit pull requests.