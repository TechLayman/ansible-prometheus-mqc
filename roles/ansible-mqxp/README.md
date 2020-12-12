ansible-mqxp
=========

Ansible Role to install IBM MQ Exporter on targeted machines

Requirements
------------

No Prerequisites to install MQ exporter ( As this repo provides MQ Export exicutable )

Role Variables
--------------
mqxp_action: null
mqxp_install_path: /opt/insight/mqxpv9
mqxp_port: 8171

1. Provide the action ( install/uninstall ) when using the role.
2. The default install path the repo follows is /opt/insight/mqxpv9
3. The role creates MQ Service object on all queue managers which are running 
   Port for each queue manager starts from 8171 and increments 


Dependencies
------------

No Dependencies

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: ansible-mqxp
           mqxp_action: install

License
-------

BSD

Author Information
------------------

annu.singh@prolifics.com
