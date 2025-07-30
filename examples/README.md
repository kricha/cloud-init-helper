# Usage Examples

This directory contains examples of how to use the `pveci` tool in different scenarios.

## 1. Create a Development VM

Create a development environment with common tools:

```bash
./pveci \
    --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
    --id 1000 \
    --name dev-vm \
    --memory 4096 \
    --cores 2 \
    --size 32G \
    --cloud-config templates/development-environment.yaml

# Access the VM
ssh developer@<vm-ip>
```

## 2. Minimal Server

Create a minimal server with basic configuration:

```bash
./pveci \
    --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
    --id 1001 \
    --name minimal-server \
    --memory 1024 \
    --cores 1 \
    --cloud-config templates/base.yaml
```

## 3. Docker Host

Create a Docker-ready host:

```bash
./pveci \
    --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
    --id 1002 \
    --name docker-host \
    --memory 8192 \
    --cores 4 \
    --size 50G \
    --cloud-config templates/base-and-docker.yaml
```

## 4. Custom Storage and Network

Create VM with specific storage and network settings:

```bash
./pveci \
    --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
    --id 1003 \
    --name custom-vm \
    --memory 2048 \
    --cores 2 \
    --storage local-lvm \
    --bridge vmbr1 \
    --cloud-config templates/base.yaml
```

## 5. Using Different Cloud Images

Examples for different distributions:

### Ubuntu 24.04 LTS

```bash
./pveci \
    --url https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img \
    --id 1004 \
    --name ubuntu-noble \
    --cloud-config templates/base.yaml
```

### Debian 12

```bash
./pveci \
    --url https://cloud.debian.org/images/cloud/bookworm/latest/debian-12-generic-amd64.qcow2 \
    --id 1005 \
    --name debian-bookworm \
    --cloud-config templates/base.yaml
```

### Rocky Linux 9

```bash
./pveci \
    --url https://dl.rockylinux.org/pub/rocky/9/images/x86_64/Rocky-9-GenericCloud.latest.x86_64.qcow2 \
    --id 1006 \
    --name rocky-9 \
    --cloud-config templates/base.yaml
```

Note: All images are downloaded directly from official sources. For offline installations,
you'll need to configure a local mirror or repository with the cloud images.
