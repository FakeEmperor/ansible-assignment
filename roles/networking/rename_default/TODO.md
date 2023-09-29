# TODOs

- [ ] Support situations when `ansible_default_ipv4` is not set (no default route): 
    - first available interface other than lo
    - set interface MAC addresses (also useful for IPMI)
- [ ] Add support for NetworkManager-managed interfaces. A few options:
    - Use nmcli / nmcli module of Ansible to rename interfaces
    - Disable NM management for the interface
- [ ] Add more robust testing against network issues due to errors in `netplan` config.
    - Generalize this role to manage network interfaces in general. 
      This will allow renaming different interfaces based on their MAC address,
      while still allowing to rename one "default route" interface.
    - Support other distributions by switching off `netplan` and using `systemd-network` units.
      This will coincidentally require to set more parameters for each network interface such as 
      using DHCP or setting static IP, nameservers and gateways.
