Vault
=========

Ansible role for secrets management(vault and consul) defines 6 lifecycle states for vault:

1. Deploy
2. Initialize
3. Provision keys
4. Running
5. Lock
6. Wipe

This role performs the following tasks:

Deploy:

1. Installs, configures and starts vault as a systemd service.
2. As a dependency role, can be configured to install as consul client
3. Configures consul as a physical storage backend
4. Enables TLS for Vault servers
5. Performs status check on vault
6. Enables gossip encryption by distributing symmetric key to all nodes

Initialize:

1. Creates a cluster of server and client consul nodes
2. Initializes vault


Running:

1. Fetches unseal token
3. Ensures Vault service is started
2. Unseals vault

Lock:

1. Fetches unseal token
2. Seals Vault
3. Ensures Vault service is stopped

Wipe:

1. Deletes vault binary, config files and pki files


## Notes: 

- Currently, the private keys, certs and root certificates are copied to servers from "files" folder of vault role. 
- Vault is currently accessible via REST API and Command Line Interface(CLI)
- Memory locking is disabled right now for following reasons:
	a) It is assumed that memory swap should be encrypted for all systems
	b) To avoid giving additional capability to vault for mlock access
- Replacing a previously failed vault node, is the same as adding a new vault node, since consul clients do not form a consensus and vault nodes do not form a cluster.
- When adding or replacing nodes, Control host will keep track of gossip encryption key that is installed on current hosts, and will install the same key on the new hosts
- Please consider using auto-unseal in production and protect gossip_encryption key at control host 
- Prior to Ansible v2.1, using uri module(for init, running, locking of vault) has a dependency on httplib2>=0.7 