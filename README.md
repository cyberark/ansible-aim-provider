cyberark_aimprovider
====================

Role to install/uninstall CyberArk's AIM Credential Provider

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------
```
# CyberArk's Privileged Account Security Web Services SDK api base URL
rest_api_url: ""

# Whether to validate certificates for REST api calls
validate_certs: true

# Zip file with distribution of AIM Provider
zip_file_name: ""

# Folder name within the ZIP file that will be used by default is taken from zip file name.
folder_name: '{{zip_file_name.split("/")[-1].split("-Rls")[0]}}'

# CyberArk location for App Provider user to be created
app_provider_user_location: "\\Applications"

# CyberArk Vault Address
vault_address: ""

# Whether to use shared logon authentication
use_shared_logon_authentication: false

# State
state: "present"
```

Dependencies
------------

None


Example Playbook
----------------

1) Install CyberArk AIM Provider

```
---
- hosts: all 

  roles:
    - role: cyberark_aimprovider
      api_base_url: "https://components.cyberark.local"
      validate_certs: false
      zip_file_name: "/tmp/binaries/RHELinux x64-Rls-v9.8.zip"
      vault_address: "10.0.1.10"
      use_shared_logon_authentication: true

```

2) Uninstall CyberArk AIM Provider
```
---
- hosts: all 

  roles:
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
