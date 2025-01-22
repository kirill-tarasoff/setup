# README for Ansible Playbook

## Overview
The provided playbook is designed to prepare servers for production use. It utilizes the `server_preparation` role to perform the following tasks:
- Encrypt specified disks and partitions.
- Optimize CPU performance settings.
- Rename the primary network interface.
- Display detailed system information.

---

## Usage

### Step 1: Set Up Inventory
Define the target servers and variables in the inventory file located in the `environments/` folder:

```yaml
all:
  hosts:
    server1:
      ansible_host: 192.168.1.10
      disk_to_encrypt: "/dev/sdb"
      partition_to_encrypt: "/dev/sda2"
```

### Step 2: Run the Playbook
Run the playbook with:
```bash
ansible-playbook -i environments/inventory.yml playbook.yml
```

### Step 3: Verify the Results
Ensure:
- The disk and partition are encrypted and functional.
- The CPU operates in performance mode.
- The network interface is renamed to `net0`.
- System information outputs correctly in the playbook logs.

---

## Files and Structure

### Key Files
- `playbook.yml`: The main playbook to execute the role.
- `environments/inventory.yml`: Defines the hosts and variables for the playbook.

### Role
The `server_preparation` role is stored in the `roles/` directory and contains:
- `tasks/main.yml`: Tasks for server setup.
- `defaults/main.yml`: Default variable values for the role.

---

## Notes
- Ensure the `cryptsetup` package is installed on all target servers.
- Adjust inventory variables as needed for your specific environment.
- Use Molecule to test changes to the role before deployment.

---

## Support
If you encounter any issues or have questions, please open an issue in the repository.

