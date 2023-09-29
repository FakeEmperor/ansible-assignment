# Ansible ad-hoc role to encrypt root partition neighbor

Root partition neighbor is a partition that is placed next to a partition of the root FS.

## Requirements

Nothing.

## Role Variables

- `adhoc_encrypt_root_neighbor_container_name` (required): LUKS container name for the partition. 
- `adhoc_encrypt_root_neighbor_luks_params` (default: `{}`): Additional parameters for encryption role.
  This parameter will act as overrides for `encryption_luks_params` variable and is merged with it.
  
  ⚠ NOTE: If required parameters are not set `encryption_luks_params` and in `adhoc_encrypt_root_neighbor_luks_params`,
  role will **fail**.

## Dependencies

Nothing.

## Example Playbook

In this example role will detect neighboring partition to a partition mounted to `/` and will create LUKS v1 container in it.

```yaml
- hosts: all
  roles:
    - role: roles/encryption/luks 
      encryption_luks_params:
        keyfile_src: ./secrets/my_secret_luks_keyfile
        keyfile_dest: /root/.luks/luks_keyfile
      adhoc_encrypt_root_neighbor_container_name: my-vault
      adhoc_encrypt_root_neighbor_luks_params:
        type: luks1
```

## Verifying

To verify that the role worked, you can simply ask if the device is luks:
- `cryptsetup isLuks <encryption_luks_device>`
