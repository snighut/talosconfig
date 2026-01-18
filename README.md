# Talos Homelab Configuration

This repository contains the TalosOS related information in order to control it from outside machine

## Overview


This homelab setup consists of:
- **Proxmox server** running 3 TalosOS virtual machines
  - 1 control plane node
  - 2 worker nodes
- **Mac Mini** (local machine) that connects to the homelab cluster

## Repository Contents

- **`talosconfig`** - Talos client configuration file containing cluster connection details, certificates, and authentication credentials
- **`controlplane.yaml`** - TalosOS machine configuration for the control plane node
- **`worker.yaml`** - TalosOS machine configuration for the worker nodes
- **`README.md`** - This documentation file

## Purpose

This repository serves as a centralized location to store and manage:
- Talos cluster access credentials
- Node configuration templates
- Connection endpoints and certificates

These files enable secure communication between your local Mac Mini and the Kubernetes cluster running on your Proxmox homelab.

## Prerequisites

- [talosctl](https://www.talos.dev/latest/introduction/getting-started/) installed on your Mac Mini
- Network connectivity to your Proxmox homelab
- Access to the Proxmox server hosting the TalosOS VMs

## Usage

### Connecting to the Cluster

1. Clone this repository to your Mac Mini:
   ```bash
   git clone <repository-url>
   cd talosconfig
   ```

2. Copy the `talosconfig` file to your Talos config directory:
   ```bash
   cp talosconfig ~/.talos/config
   ```

3. Test the connection:
   ```bash
   talosctl --context my-cluster version
   ```

### Applying Node Configurations

To apply or update node configurations:

```bash
# For control plane
talosctl apply-config --file controlplane.yaml --nodes <control-plane-ip>

# For worker nodes
talosctl apply-config --file worker.yaml --nodes <worker-node-ip>
```

## Security Note

⚠️ **Important**: This repository contains sensitive credentials including:
- Cluster CA certificates
- Client certificates and private keys
- Cluster tokens

Ensure this repository is kept private and secure. Do not commit to public repositories.

## Cluster Information

- **Cluster Name**: my-cluster
- **TalosOS Version**: v1.35.0
- **Cluster Type**: Single control plane with 2 worker nodes

## Additional Resources

- [TalosOS Documentation](https://www.talos.dev/)
- [Proxmox Documentation](https://www.proxmox.com/en/proxmox-ve)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)