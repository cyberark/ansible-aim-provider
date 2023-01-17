cyberark_aimprovider
====================

**THIS IS NOW A PART OF THE `cyberark.pas` COLLECTION AT https://galaxy.ansible.com/cyberark/pas**

Role to install/uninstall CyberArk's AIM Credential Provider.

Requirements
------------

- CyberArk Privileged Account Security Web Services SDK.
- If modules not accesible from Ansible core, please use cyberark-bizdev.cyberark_modules from galaxy.

Role Variables
--------------
```
# CyberArk's Privileged Account Security Web Services SDK api base URL (example: https://components.cyberark.local)
rest_api_url: ""

# Whether to validate certificates for REST api calls. If false, SSL certificates will not be validated. This should only be used on personally controlled sites using self-signed certificates.
validate_certs: true

# Zip file with distribution of AIM Provider (example: /tmp/binaries/RHELinux x64-Rls-v9.8.zip); this file is located in the Ansible server, and it will be copied to the Ansible nodes. It should point to the current version of AIM distribution to be used when delivering to the nodes in a central folder within the Ansible server.
zip_file_name: ""

# Folder name within the ZIP file that will be used. By default, it's taken from zip file name, for example: "RHELinux x64"
folder_name: '{{zip_file_name.split("/")[-1].split("-Rls")[0]}}'

# CyberArk location for App Provider user to be created
app_provider_user_location: "\\Applications"

# CyberArk Vault Address
vault_address: ""

# Whether to use shared logon authentication. If true, it will use the "Shared Logon Authentication" as described in the CyberArk's document "Privileged Account Security Web Services SDK Implementation Guide"
use_shared_logon_authentication: false

# State - can be "present"/"absent" for install/uninstall.
state: "present"
```


Additionally:
- **app_provider_user_group**: The name of the group the Provider user will be added to.

Dependencies
------------

None.


Example Playbook
----------------

**Note**:
- As the role will include the galaxy user, you can create a symbolic link as follows:
```
ln -s /etc/ansible/roles/cyberark-bizdev.cyberark_aimprovider cyberark_aimprovider
```

1) Install CyberArk AIM Provider.

```
---
- hosts: all

  roles:

    - role: cyberark_modules # Include cyberark_modules if needed

    - role: cyberark_aimprovider
      api_base_url: "https://components.cyberark.local"
      validate_certs: false
      zip_file_name: "/tmp/binaries/RHELinux x64-Rls-v9.8.zip"
      vault_address: "10.0.1.10"
      use_shared_logon_authentication: true
```

2) Uninstall CyberArk AIM Provider.
```
---
- hosts: all

  roles:

    - role: cyberark_modules # Include cyberark_modules if needed

    - role: cyberark_aimprovider
      api_base_url: "https://components.cyberark.local"
      use_shared_logon_authentication: true
      state: "absent"
      validate_certs: false
```

License
-------

MIT

Author Information
------------------

- Edward Nunez (edward.nunez@cyberark.com)
