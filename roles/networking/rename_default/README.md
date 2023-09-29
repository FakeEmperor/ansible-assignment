# Ansible role to rename default interface 

NOTE: "default interface" here means interface that has a "default route" attached to it.

❗ NOTE: role will run even if currently interface name and desired names are the same. It is to ensure that
on next reboot configuration is definitely persisted.

## Requirements

Nothing.

## Role Variables

- `networking_rename_default_name` (default: `"eth0"`): Target name for the default interface.

## Dependencies

Nothing.

## Example Playbook

Rename default interface to `net0`:

```yaml
- hosts: all
  roles:
    - role: roles/networking/rename_default
      networking_rename_default_name: "net0" 
```

## Verifying

To verify that it worked, just check that the interface name changed by using `ip link`.
