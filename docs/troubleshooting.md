# Troubleshooting Guide

## Common Issues and Solutions

### 1. Image Download Issues

#### Symptoms
- Wget fails silently
- Incomplete downloads
- Corrupted images
- "404 Not Found" errors
- SSL certificate verification failures

#### Solutions
1. Check Image URL:
   ```bash
   # Test URL accessibility
   wget --spider <image-url>
   
   # For SSL issues, verify with curl
   curl -IL <image-url>
   ```

2. Verify disk space:
   ```bash
   # Check available space
   df -h /var/lib/vz/template/iso/
   ```

3. Download issues:
   - Use alternative mirrors (see cloud-images.md for official mirrors)
   - For SSL issues with trusted sources, you can use:
     ```bash
     wget --no-check-certificate <image-url>
     ```
   - For large files, use continue flag:
     ```bash
     wget -c <image-url>
     ```

4. Verify downloaded image:
   ```bash
   # Check file integrity
   qemu-img check downloaded-image.qcow2
   
   # View image info
   qemu-img info downloaded-image.qcow2
   ```

### 2. VM Creation Failures

#### Symptoms
- Error during VM creation
- VM creates but doesn't start
- Cloud-init doesn't run
- Permission denied errors
- Storage pool not found

#### Solutions
1. Verify Proxmox Permissions:
   ```bash
   # Check user permissions
   pveum user list
   
   # Verify storage permissions
   pveum aclmod / -user <username> -role Administrator
   ```

2. Storage Issues:
   ```bash
   # List available storages
   pvesm status
   
   # Check storage usage
   pvesm list <storage_name>
   ```

3. Cloud-init Configuration:
   - Check cloud-init drive is attached:
     ```bash
     qm showcmd <vmid> | grep cloud
     ```
   - Verify cloud-init config:
     ```bash
     cat /var/lib/vz/snippets/<cloud-init-file>
     ```

4. QEMU Guest Agent:
   - Check if installed in template:
     ```bash
     # Connect to VM console
     qm terminal <vmid>
     
     # Inside VM, verify agent
     systemctl status qemu-guest-agent
     ```
   - If missing, install in template:
     ```bash
     apt install qemu-guest-agent   # Debian/Ubuntu
     dnf install qemu-guest-agent   # RHEL/Rocky
     ```

### 3. Network Issues

#### Symptoms
- VM has no network connectivity
- Cannot reach the internet
- DNS resolution fails
- DHCP not working
- Network interface missing

#### Solutions
1. Check Bridge Configuration:
   ```bash
   # List network interfaces
   ip a
   
   # Verify bridge exists
   brctl show
   
   # Check bridge status
   ip link show <bridge_name>
   ```

2. VLAN Configuration:
   ```bash
   # View VM network config
   qm config <vmid> | grep net
   
   # Check VLAN connectivity
   vconfig show
   ```

3. Cloud-init Network Settings:
   - Verify network configuration:
     ```bash
     qm cloudinit dump <vmid> network
     ```
   - Common cloud-init network settings:
     ```yaml
     network:
       version: 2
       ethernets:
         ens18:
           dhcp4: true
     ```

4. Inside VM Checks:
   ```bash
   # Check network interfaces
   ip a
   
   # Test DNS resolution
   ping -c 3 8.8.8.8
   dig google.com
   
   # View network config
   cat /etc/netplan/*.yaml  # Ubuntu
   cat /etc/sysconfig/network-scripts/ifcfg-* # RHEL/Rocky
   ```

### 4. Storage Issues

#### Symptoms
- Insufficient space errors
- Storage pool not found
- Disk performance issues
- I/O errors
- Slow disk operations

#### Solutions
1. Storage Pool Management:
   ```bash
   # List storage pools
   pvesm status
   
   # Check specific storage details
   pvesm list <storage_name>
   
   # View available space
   df -h /var/lib/vz/
   ```

2. Permission Issues:
   ```bash
   # Check storage permissions
   ls -la /var/lib/vz/
   
   # Fix common permission issues
   chmod 755 /var/lib/vz/template/iso/
   ```

3. Performance Optimization:
   - Check disk performance:
     ```bash
     # Test read performance
     dd if=/var/lib/vz/template/iso/test.img of=/dev/null bs=1M count=1000
     
     # Test write performance
     dd if=/dev/zero of=/var/lib/vz/template/iso/test.img bs=1M count=1000
     ```
   - SSD configuration:
     ```bash
     # Check if discard is enabled
     pvesm status | grep discard
     
     # Enable TRIM for SSD
     pvesm set <storage> --ssd 1
     ```

## Log Locations and Monitoring

### System Logs
```bash
# Proxmox VE logs
tail -f /var/log/pve/tasks/index.log    # Task logs
tail -f /var/log/pve/status.log         # Status updates
tail -f /var/log/syslog | grep pve      # System logs

# Cloud-init logs (inside VM)
tail -f /var/log/cloud-init.log         # Main cloud-init log
tail -f /var/log/cloud-init-output.log  # Cloud-init output
```

### Monitoring Commands
```bash
# Watch VM status
qm status <vmid>

# Monitor VM resources
qm monitor <vmid>

# View VM processes
qm guest cmd <vmid> get-processes

# Check VM agent status
qm agent <vmid> ping
```

## Getting Help

1. First Steps:
   - Check this troubleshooting guide
   - Review relevant logs (see above)
   - Verify configurations and permissions

2. Community Support:
   - [Open an issue on GitHub](https://github.com/kricha/cloud-init-helper/issues)
   - Check existing issues for similar problems
   - Include relevant logs and configurations when reporting

3. Documentation:
   - [Proxmox VE Documentation](https://pve.proxmox.com/wiki/Main_Page)
   - [Cloud-init Documentation](https://cloudinit.readthedocs.io/)
   - Project README and examples
