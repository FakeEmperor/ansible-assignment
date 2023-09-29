# Ansible role to change CPU frequency scaling governor

Controls CPU scaling governor on a machine to change it from usually default `ondemand` governor.

❗ NOTE: it was not tested on a real VM that supported P-state control.

## Requirements

If running on a VM guest, a machine that is able to control P-states of a physical CPU. 
For AWS EC2 instances, please refer to this page 
(https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/processor_state_control.html) 
to understand which instances support P-state control. 

## Role Variables

- `performance_scaling_governor_name` (default: `"performance"`): Name of the governor to enable.

## Dependencies

Nothing.

## Example Playbook

Change scaling governor to `powersave` (useful on overheating notebooks)

```yaml
- hosts: servers
  roles:
    - role: roles/performance/scaling_governor
      performance_scaling_governor_name: "powersave"
```

## Verification 

To verify that the scaling governor has changed, you can (in case of "performance" governor set):
- `grep "performance" /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor`
