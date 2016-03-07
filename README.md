# ansible-citrixcmdctr

Ansible playbook for Citrix Command Center 5.2

## Caveats

This playbook only supports installation on CentOS7 and MSSQL databases.

## Sample Configuration

In `group_vars/all/cmdctr_installation`:

```
---
cmdctr_installation:
    installer_path: /private/nfs/
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
