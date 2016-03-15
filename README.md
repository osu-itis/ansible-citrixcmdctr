# ansible-citrixcmdctr

[![Build Status](https://jenkins.sig.oregonstate.edu/job/lint%20ansible-citrixcmdctr/badge/icon)](https://jenkins.sig.oregonstate.edu/job/lint%20ansible-citrixcmdctr/)

Ansible playbook for Citrix Command Center 5.2

## Caveats

This playbook only supports installation on CentOS7 and MSSQL databases.

## Configuration

In `hosts`:
```
[command_center]
changeme.someplace.edu

[scripthost]
changeme2.someplace.edu
```

* **command_center** is the hostname of the target box to install Command Center on
* **scripthost** is the hostname of the box where the `citrixcc-taskmaster` generator script is installed

In `group_vars/all/cmdctr_installation`:

```
---
cmdctr_installation:
    installer_path: /private/nfs
    installer_filename: CC_Setup64_5.2_44_11.bin
    installer_temp_path: /tmp
cmdctr_database:
    hostname: dbhost.somewhere.edu
    port: 1433
    dbname: changeme
    username: changeme
    password: changeme
firewalld_open_port:
    ports: [ "8443/tcp", "9090/tcp", "161/udp", "162/udp" ]
```

In `group_vars/all/taskmaster`:
```
---
taskmaster:
    serviceobjects_source_path: /private/nfs
    scripthost_scripts_home: /home/scripts
```

* **serviceobjects_source_path** is the location *on the ansible box* where `serviceobjects.yml` master NetScaler service objects file can be found
* **scripthost_scripts_home** is the path to the scripts home dir on the script host box. Must match what's configured in the `ansible-scriptbox` playbook.

## Usage

### Installing Command Center
```
$ ansible-playbook -i hosts install_cmdctr.yml
```

### Generating Command Center Tasks
```
$ ansible-playbook -i hosts generate_tasks.yml
```
