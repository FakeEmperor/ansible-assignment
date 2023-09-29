# TODOs

Some thoughts about what can be improved:

- Add molecule testing with Vagrant / AWS. In case Vagrant, need to look into a provider 
  (most likely QEMU full virtualization) that allows full C-state and P-state control over host CPU;
- Do more testing for other distributions in case more distributions should be supported;
- Add schema validation for role variables.
  Role `shinesolutions_opensource.vars_schema_validator` does it using
  [cerberus](http://docs.python-cerberus.org/en/stable/validation-rules.html).
  Example (from my home-infra SSH role):

  ```yaml
  # If set, will ensure SSH port matches common_ssh_ensure_port's value
  common_ssh_ensure_port:
    type: integer
    required: no
  # Will allow new port in firewalld if common_ssh_ensure_port is set
  common_ssh_ensure_port_firewall:
    type: boolean
    required: yes
  # Will allow new port in SELinux if common_ssh_ensure_port is set
  common_ssh_ensure_port_selinux:
    type: boolean
    required: yes
  # Disable or enable password auth
  common_ssh_root_password_auth:
    type: string
    required: yes
    allowed:
    - enabled
    - disabled
  # A list of authorized_keys to make sure are in the list
  common_ssh_authorized_keys:
    type: list
    required: no
  ```

For improvements of a particular role, see respective `TODO.md` of the role.
