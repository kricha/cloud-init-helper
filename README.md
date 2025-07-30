# Cloud Init Helper for Proxmox

> 🚀 A powerful shell script for automating cloud-init VM template creation in Proxmox VE.
> Streamline your VM deployment with smart defaults, custom configurations, and comprehensive error handling.

[![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=flat&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Proxmox](https://img.shields.io/badge/proxmox-%23E57000.svg?style=flat&logo=proxmox&logoColor=white)](https://www.proxmox.com/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE.md)

## Features

- Automated VM template creation from cloud images

- Smart defaults with customizable options

- SSD optimization support

- Custom cloud-init configuration

- Automatic resource detection

- Dry-run capability

- Comprehensive error handling

## Prerequisites

The following commands must be available on your Proxmox host:

- `qm` (Proxmox VM management)

- `wget` (File downloads)

- `qemu-img` (Image manipulation)

- `pvesm` (Proxmox storage management)

## Usage

```bash
./pveci [OPTIONS]

Options:
  -u, --url URL           Cloud image URL (required)
  -i, --id ID            VM ID (auto-detected if not specified)
  -n, --name NAME        VM name (auto-generated if not specified)
  -m, --memory MB        Memory in MB (default: 1024)
  -c, --cores NUM        Number of CPU cores (default: 1)
  -s, --size SIZE        Disk size (default: 10G)
  -b, --bridge BRIDGE    Network bridge (default: vmbr0)
  -t, --storage STORAGE  Storage pool (auto-detected if not specified)
  --cloud-config PATH    Use custom cloud-init config (file path or URL)
  --dry-run             Show what would be done without executing
  --no-ssd              Disable SSD optimization (default: enabled)
  -h, --help            Show this help message
```

## Examples

1. Basic usage with Ubuntu cloud image:

   ```bash
   ./pveci -u https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img
   ```

2. Custom configuration:

   ```bash
   ./pveci --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
        --id 100 \
        --name ubuntu-template \
        --memory 2048 \
        --cores 2 \
        --size 20G
   ```

3. Using custom cloud-init config:

   ```bash
   ./pveci -u https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
        --cloud-config ./templates/base-and-docker.yaml
   ```

## Cloud-Init Configurations

The repository includes two predefined cloud-init configurations:

1. `base.yaml` - Minimal configuration with:

   - qemu-guest-agent installation
   - SSH service enablement

2. `base-and-docker.yaml` - Extended configuration with:
   - Everything from base.yaml
   - Docker installation and configuration
   - User docker group management
   - Custom MOTD
   - Secure SSH configuration

## Installation

### Quick Install (Script Only)

If you just need the script without templates:

```bash
# Download and install the script
wget https://raw.githubusercontent.com/kricha/cloud-init-helper/main/pveci && \
chmod +x pveci && \
sudo mv pveci /usr/local/bin/

# Verify installation
pveci --help
```

#### Download Templates Only

```bash
# Create templates directory and download
mkdir -p templates/ && cd templates/ && \
wget https://raw.githubusercontent.com/kricha/cloud-init-helper/main/templates/base.yaml \
     https://raw.githubusercontent.com/kricha/cloud-init-helper/main/templates/base-and-docker.yaml

# Create templates directory
mkdir -p templates/
mv base*.yaml templates/
```

### Full Repository Installation

To get the complete repository with all examples and documentation:

1. Clone the repository:

   ```bash
   git clone https://github.com/kricha/cloud-init-helper.git
   ```

2. Make the script executable:

   ```bash
   chmod +x pveci
   ```

3. Optional: Move to system path:

   ```bash
   sudo cp pveci /usr/local/bin/
   ```

## Verifying Installation

After installation, you can verify that everything is working correctly:

1. Check script availability:

   ```bash
   pveci --help
   ```

2. Verify templates:

   ```bash
   # For quick install
   ls ~/.config/pveci/templates/

   # For repository install
   ls templates/
   ```

3. Test with dry-run:

   ```bash
   pveci --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img --dry-run
   ```

## Contributing

Contributions are welcome! Please feel free to submit pull requests.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
