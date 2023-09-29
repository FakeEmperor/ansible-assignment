# Ansible role to limit C-state to C0 (low latency)

Disables CPU power optimizations which sets CPU into performance mode.

WARNING: this will greatly increase CPU temperature and power consumption for all time since
it prevents CPU to shut off not used circuits.

## Requirements

Nothing.

## Role Variables

- `performance_cstate_freeze_state` (default: `"present"`): If `"present"`, will enable C-State freezing.

## Dependencies

Nothing.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  roles:
    - role: roles/performance/cstate_freeze
      performance_cstate_freeze_state: "absent"  # ensures it will enable C-states back again
```

## Verification

You can verify that the role worked correctly by checking:

- `grep "intel_idle.max_cstate=0" /proc/cmdline`
- `grep "0" /sys/module/intel_idle/parameters/max_cstate`
