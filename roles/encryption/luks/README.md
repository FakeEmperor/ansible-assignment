# Ansible role to configure LUKS device

Creates LUKS container in a specified block device (disk or partition).
Does not handle filesystem creation or mounting.

## Requirements

- `community.crypto` collection. `ansible-galaxy collection install community.crypto`

## Role Variables

- `encryption_luks_device` (required): Device that is going to be holding LUKS container. 
  Example: `/dev/sdb2` or, for full-disk encryption, `/dev/sdc`
- `encryption_luks_container_name` (required): Container name for Device Mapper, 
  will set the name in crypttab and will be available to mount as `/dev/mapper/<container-name>`
- `encryption_luks_params.keyfile_src` (required): Source path for keyfile to copy from Ansible control host;
- `encryption_luks_params.keyfile_dest` (required): Destination path for keyfile that is being copied onto remote;
- `encryption_luks_params.type`: LUKS type. Can be either `luks1` or `luks2`;

## Dependencies

Nothing.

## Example Playbook

Encrypt full disk at `/dev/sdb` using `./secrets/my_secret_luks_keyfile` secrets file stored on Ansible control machine:

```yaml
- hosts: all
  roles:
    - role: roles/encryption/luks
      encryption_luks_device: /dev/sdb
      encryption_luks_container_name: my-vault
      encryption_luks_params:
        keyfile_src: ./secrets/my_secret_luks_keyfile
        keyfile_dest: /root/.luks/luks_keyfile
```

## Verifying

To verify that the role worked, you can simply ask if the device is luks:
- `cryptsetup isLuks <encryption_luks_device>`
