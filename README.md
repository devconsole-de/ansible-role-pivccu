# Role Name: pivccu

This role installs the piVCCU&reg; project from Alexander Reinert. It is a project to install the original Homematic CCU2 / CCU3 firmware inside virtualized container (lxc) on ARM based single board computers.
You can find the project at https://github.com/alexreinert/piVCCU/ .

# Requirements

It is designed for ARM based single board computers like the RaspberryPi.
Currently this role is tested on a Raspberry Pi 3 Model B with the [HM-MOD-RPI-PCB](https://de.elv.com/elv-homematic-komplettbausatz-funkmodul-fuer-raspberry-pi-hm-mod-rpi-pcb-fuer-smart-home-hausautomation-142141) connected via GPIO.
You can find further [prerequisites here](https://github.com/alexreinert/piVCCU/#prequisites).

# Role Variables

default variables in `defaults/main.yml`:

| Variable         | Value                                     |
|------------------|-------------------------------------------|
| pivccu_apt_key   | 'https://www.pivccu.de/piVCCU/public.key' |
| pivccu_repo_url  | 'https://www.pivccu.de/piVCCU'            |
| pivccu_apt_suite | 'stable' # 'testing' as alternative       | 

---------------

variables in `vars/main.yml`:

| Variable                        | Value                                            |
|---------------------------------|--------------------------------------------------|
| pivccu_pkg                      | 'pivccu3' # 'pivccu' for CCU version 2           |
| pivccu_hw_hb_rf_eth             | 'false' # HM-MOD-RPI-PCB/RPI-RF-MOD via Ethernet |     
| pivccu_create_backup_job        | 'true'                                           |
| pivccu_backup_path              | '/var/backups'                                   |
| bridge_interface_method         | 'dhcp' # 'static' (needs IP configuration - s.b.)|

---------------

When `bridge_interface_method` is set to `static`, you also have to set additional variables for templating the network bridge interface configuration in `/etc/network/interfaces`.

- bridge_ip 
- bridge_netmask # like 255.255.255.0 
- bridge_gateway
- bridge_nameserver(s) (optional list with max. 2 IPs)

# Dependencies

None.

# Example Playbook

```
  - hosts: pi-ccu
    remote_user: pi
    become: true
    roles:
    - dabo_devconsole.pivccu
    vars:
      bridge_interface_method: "static"
      bridge_ip: "192.168.2.10"
      bridge_netmask: "255.255.255.0"
      bridge_gateway: "192.168.2.1"

```
# License

Apache-2.0

# Author Information

This role was created in 2021 by [Daniel Boggasch](https://github.com/dabo-devconsole).