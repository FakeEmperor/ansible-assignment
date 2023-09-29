# Offline assignment for a finance company

A system administration / SRE task that assesses:
- Organization skills;
- Ansible knowledge;
- Core knowledge about modern UNIX components: encryption, network and performance optimizations.

## Assignment

**Goal**: Write an Ansible role and playbook to prepare the server for operation

**Task**: Prepare the OS using Ansible

Using Ansible, implement the ability to perform the following actions (and repeat them on other servers in the future):

1. Implement the procedure of encrypting the second disk in the system (where there is no root partition) 
   (partition name should be specified in the inventory).
2. Implement a procedure to encrypt the partition that is present on the disk next to the root partition.
3. Disabling C-state for all available CPUs.
4. Switching CPU operation from power-saving mode to more productive mode.
5. Rename the active network interface to "net0". Display information about the renamed interface during the playbook
6. At the end of the playbook execution, a list of CPUs should be displayed, as well as information about 
   Intel Hyper-Threading (AMD multithreading).

**General Requirements**

- When designing playbooks and roles, attention should be paid to error handling and correct task execution messages.
- Each playbook or role should be described in a separate README file along with startup and validation instructions.
- All required files (playbooks, roles, scripts) must be submitted along with the result of the assignment.

**Evaluation**: The candidate will be evaluated on the following criteria:

- Quality of writing Ansible playbooks and roles.
- Overall code organization.
- Understanding of basic Ansible concepts and system administration.

After completing the assignment, the candidate must provide an git-repository or archive of the roles, 
playbooks and README files so that they can be evaluated and tested.

## How to run

1. Ensure you have access to test machine of your choice;
2. Create `secrets` folder inside the repository and fill it with:
  - `luks_keyfile`: LUKS passphrase (can be any file, e.g. `openssl genrsa -out secrets/luks_keyfile 2048`)
3. Either edit `inventory/test-aws.yml` inventory file and set IP address of the test machine explicitly or set 
   `TEST_AWS_MACHINE_IP` environment variable.
4. Run the playbook:
   `ansible-playbook -i inventory/test-aws.yml playbooks/prepare-host.yml`
5. NOTE: role `roles/performance/scaling_governor` is commented out because it will fail on VMs that 
   do not allow controlling P-states. Either remove the check (`roles/performance/scaling_governor/tasks/main.yml:12`)
   or run on a VM that supports P-state control.

## Useful links

1. CPU frequency scaling https://wiki.archlinux.org/title/CPU_frequency_scaling
2. C-States and disabling them: https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7 
3. P-States and C-States on EC2 Instances: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/processor_state_control.html
4. Udev rules syntax checking: https://github.com/pavlinux/udev/blob/master/test/rule-syntax-check.py
