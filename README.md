**visa/ansible-hashi-vault**

---
# Overview

Ansible project for deploying, configuring, running Open source Hashicorp Vault and Consul

# Usage

## Running the playbook

	$ cd ansible-hashi-vault

Example Playbook
---------------- 

1. To deploy, initialize and run vault server and consul server on the same host:
    
    `ansible-playbook playbooks/auto_vault_server_consul_server.yml`

2. To deploy, initialize and run vault server and consul client on the same host and consul server on separate hosts:

    `ansible-playbook playbooks/auto_vault_server_consul_client_consul_server.yml`

3. To add new vault node, change inventory file, to add new host in the group secrets and run this playbook:

   a. With consul client on same host:

    `ansible-playbook playbooks/auto_vault_server_consul_client_consul_server.yml`

   b. With consul server on same host:

    `ansible-playbook playbooks/auto_vault_server_consul_server.yml` 
  Note, this will automatically install a consul node and it will be joined to the cluster

4. To replace a previously failed consul server node, if the previously failed node and the newly instantiated node have the same IP address:
  
  i. With consul client on same host as vault:

      `ansible-playbook playbooks/auto_vault_server_consul_client_consul_server.yml`
  
  ii. With consul server on same host as vault:

      `ansible-playbook playbooks/auto_vault_server_consul_server.yml`

5. To remove consul client/server node, change inventory file, remove the node from appropriate group and run the playbook:

   a. With consul client on same host:

    `ansible-playbook playbooks/auto_vault_server_consul_client_consul_server.yml`

   b. With consul server on same host:

    `ansible-playbook playbooks/auto_vault_server_consul_server.yml`

6. Wipe vault and consul nodes:

    `ansible-playbook playbooks/wipe_consul_vault.yml`

7. Lock vault:

    `ansible-playbook playbooks/run_to_lock_vault.yml`

8. Run vault:

    `ansible-playbook playbooks/lock_to_run_vault.yml`


Inventory groups
---------------- 

`vault`: includes vault node and consul client nodes
`consul`: includes consul server nodes

When deploying vault server-consul client and consul server the mapping of inventory groups is as follows:

`secrets = vault + consul`

When deploying vault server to consul server mapping of inventory groups is as follows: 

`secrets=vault=consul`
