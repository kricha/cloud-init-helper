# Cloud Image Sources

This document lists verified cloud image sources for use with the cloud-init-helper.

## Ubuntu

- **LTS Releases**

  ```shell
  # Ubuntu 24.04 LTS (Noble Numbat)
  Directory: https://cloud-images.ubuntu.com/daily/server/releases/24.04/release/
  Image: https://cloud-images.ubuntu.com/daily/server/releases/24.04/release/ubuntu-24.04-server-cloudimg-amd64.img
  
  # Ubuntu 22.04 LTS (Jammy Jellyfish)
  Directory: https://cloud-images.ubuntu.com/jammy/current/
  Image: https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img
  ```

- **Daily Build**

  ```shell
  Directory: https://cloud-images.ubuntu.com/noble/current/
  Image: https://cloud-images.ubuntu.com/noble/current/noble-server-cloudimg-amd64.img
  ```

## Debian

- **Stable (Debian 12 Bookworm)**

  ```shell
  Directory: https://cloud.debian.org/images/cloud/bookworm/daily/
  Image: https://cloud.debian.org/images/cloud/bookworm/daily/latest/debian-12-genericcloud-amd64-daily.qcow2
  ```

- **Testing (Debian 13 Trixie)**

  ```shell
  Directory: https://cloud.debian.org/images/cloud/trixie/daily/
  Image: https://cloud.debian.org/images/cloud/trixie/daily/latest/debian-13-genericcloud-amd64-daily.qcow2
  ```

## Rocky Linux

- **Rocky Linux 9**

  ```shell
  Directory: https://dl.rockylinux.org/pub/rocky/9/images/x86_64/
  Image: https://dl.rockylinux.org/pub/rocky/9/images/x86_64/Rocky-9-GenericCloud.latest.x86_64.qcow2
  ```
  
- **Rocky Linux 8 (Extended Support)**

  ```shell
  Directory: https://dl.rockylinux.org/pub/rocky/8/images/x86_64/
  Image: https://dl.rockylinux.org/pub/rocky/8/images/x86_64/Rocky-8-GenericCloud.latest.x86_64.qcow2
  ```

## Fedora

- **Latest Release (Fedora 39)**

  ```shell
  Directory: https://download.fedoraproject.org/pub/fedora/linux/releases/39/Cloud/x86_64/images/
  Image: https://download.fedoraproject.org/pub/fedora/linux/releases/39/Cloud/x86_64/images/Fedora-Cloud-Base-39-1.5.x86_64.qcow2
  ```

## OpenSUSE

- **Leap 15.6**

  ```shell
  Directory: https://download.opensuse.org/distribution/leap/15.6/appliances/
  Image: https://download.opensuse.org/distribution/leap/15.6/appliances/openSUSE-Leap-15.6-Minimal-VM.x86_64-Cloud.qcow2
  ```

## Alpine Linux

- **Latest Release (3.22)**

  ```shell
  Directory: https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/cloud/
  Image: https://dl-cdn.alpinelinux.org/alpine/v3.19/releases/cloud/alpine-virt-3.19.1-x86_64.img
  ```

## OS Image Sources

Here are some trusted places to get OS images from:

1. Have cloud-init pre-installed
2. Have python3
3. Have apt or yum installed
4. Should be accessible via a URL that can be used with curl

## Testing Status

✅ = Fully tested
🟡 = Basic testing
❓ = Untested

| Distribution | Version | Status | Notes |
|-------------|---------|---------|-------|
| Ubuntu | 24.04 LTS | ✅ | Recommended, Latest LTS |
| Ubuntu | 22.04 LTS | ✅ | Fully supported until 2027 |
| Debian | 12 | ✅ | Fully supported, Stable |
| Rocky Linux | 9 | ✅ | Fully supported, Recommended |
| Rocky Linux | 8 | 🟡 | Extended life cycle support |
| Fedora | 39 | ✅ | Fully supported |
| OpenSUSE | 15.5 | ✅ | Fully supported |
| Alpine | 3.19 | ✅ | Fully supported |
