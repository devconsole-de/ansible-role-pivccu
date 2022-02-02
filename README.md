# Role Name: pivccu

This role installs the piVCCU&reg; project from Alexander Reinert. It is a project to install the original Homematic CCU2 / CCU3 firmware inside virtualized container (lxc) on ARM based single board computers.
You can find the project at https://github.com/alexreinert/piVCCU/ .

# Requirements

It is designed for ARM based single board computers like the RaspberryPi.
Currently this role is tested on a Raspberry Pi 3 Model B.
You can find further requirements at https://github.com/alexreinert/piVCCU/#prequisites .

# Role Variables

default variables in `defaults/main.yml`:

| Variable         | Value                                     |
|------------------|-------------------------------------------|
| pivccu_apt_key   | 'https://www.pivccu.de/piVCCU/public.key' |
| pivccu_repo_url  | 'https://www.pivccu.de/piVCCU'            |
| pivccu_apt_suite | 'stable' # 'testing' as alternative       | 

---------------

variables in `vars/main.yml`:

| Variable                        | Value                                  |
|---------------------------------|----------------------------------------|
| pivccu_pkg                      | 'pivccu3' # 'pivccu' for CCU version 2 |
| pivccu_configure_network_bridge | 'false'                                |
| pivccu_create_backup_job        | 'true'                                 |

---------------

When `pivccu_configure_network_bridge` is set to `true`, you also have to set additional variables for temlating the network bridge configuration in `/etc/network/interfaces`.

- bridge_ip
- bridge_netmask
- bridge_gateway
- bridge_nameserver(s) (optional list with max. 2 IPs)

# Dependencies

None.

# Example Playbook

```
  - hosts: pi-ccu
    roles:
    - devconsole-de.pivccu
```
# License

Apache-2.0

# Author Information

This role was created in 2021 by [Daniel Boggasch](https://github.com/dabo-devconsole).