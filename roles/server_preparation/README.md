# README for Ansible Role: server_preparation

## Overview
This role is designed to prepare a server by performing the following tasks:
- Encrypting specified disks and partitions using LUKS.
- Setting CPU performance mode and disabling C-states.
- Renaming network interfaces for consistency.
- Providing system information for verification.

---

## Role Variables

### Defaults
Default values for the role's variables are specified in `defaults/main.yml`:

```yaml
disk_to_encrypt: "/dev/sdb"  # Default disk to encrypt
partition_to_encrypt: "/dev/sda2"  # Default partition to encrypt near root
```

These can be overridden in the inventory file or directly in the playbook.

### Example Inventory Override
```yaml
all:
  hosts:
    server1:
      disk_to_encrypt: "/dev/sdc"
      partition_to_encrypt: "/dev/sda3"
```

---

## Tasks

### Major Tasks Include:
1. **Installing Required Packages:** Ensures tools like `cryptsetup` are installed.
2. **Disk Encryption:** Encrypts disks and partitions only if they are not already encrypted.
3. **CPU Optimization:** Disables C-states and sets the CPU governor to performance mode.
4. **Network Configuration:** Renames the primary network interface to `net0`.
5. **Information Output:** Provides detailed system information such as CPU and network configuration.

---

## Usage

### Include Role in a Playbook
Add the role to your playbook:

```yaml
- name: Prepare server
  hosts: all
  roles:
    - server_preparation
```

### Run the Playbook
Execute the playbook with:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

---

## Notes
- Ensure the `cryptsetup` package is available on your target server.
- Test role changes thoroughly using Molecule before deploying to production.

---

## Testing
This role includes Molecule configurations for automated testing.

### Molecule Tests
1. **Converge:** Ensures the role applies successfully.
2. **Verify:** Checks the correctness of encryption, CPU mode, and network interface configuration.
3. **Destroy:** Cleans up test containers.

Run Molecule tests with:
```bash
molecule test
```

