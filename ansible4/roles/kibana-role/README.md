Kibana role 
========= 

Роль для установки Kibana на хостах с ОС: Debian, Ubuntu, CentOS, RHEL. 

Requirements 
------------ 

Поддерживаются только ОС семейств Debian и EL. 

Role Variables 
--------------

| Variable name | Default | Description | 
|-----------------------|----------|-------------------------| 
| kibana_version | "7.14.0" | Параметр, который определяет какой версии kibana будет установлен |

Example Playbook 
---------------- 

    - hosts: all 
      roles: 
        - { role: kibana-role } 

License 
------- 

BSD 

Author Information 
------------------ 

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
