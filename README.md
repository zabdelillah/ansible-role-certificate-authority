# Certificate Authority Ansible Role
Ansible role to handle the creation of a certificate authority, and server/client certificates creation using Certificate Signing Requests.

## Requirements
This role doesn't install the required packages on the system yet that are required by the Ansible OpenSSL modules. 
| System Packages |
|--|
| Python(2)-crypto |
| OpenSSL |

## Role Configuration
All required variables for this role are displayed within the `defaults/main.yml` file. These will be set by default, but an override can be enforced for more flexibility.
| Variable | Purpose |
|--|--|
| root_certificate_authority_group | Ansible Inventory group that contains the root authority node |
| intermediate_certificate_authority_group | Ansible Inventory group that contains the intermediate authority node |
| root_authority_directory | Working area for CA Cert generation & certificate signing on the root authority node |
| intermediate_authority_directory | Working area for CA Cert generation & certificate signing on the intermediate authority node |
| private_key_passphrase_length | Length of randomly generated password for all private keys |
| *root_ca_private_key_size | Size of private keys generated by all nodes |
| private_key_cipher | OpenSSL Cipher to use to generate the private key on all nodes |
| fetch_root_ca_certificate_location | Location on the Ansible controller to transfer the root CA to the intermediate node |
| fetch_intermediate_ca_certificate_location | Location on the Ansible controller to transfer the intermediate CA to other nodes |
| fetch_combined_ca_certificate_location | Location on the Ansible controller to transfer the combined root & intermediate CA certificates to other nodes |
| ansible_default_ipv4 | IP Version to use when deferring tasks to Root & Intermediate CAs |
## Role Execution
When executing this role, a server/client certificate will always be generated. To invoke a Root & Intermediate CA certificate generation, the target machine must be inside the inventory group defined in the `root_certificate_authority_group` and `intermediate_certificate_authority_group` variables, and either of the tags must be applied.

 - generate_root_ca_certificate
 - generate_intermediate_ca_certificate

