Consul
=========

This role performs the following tasks:
1. Installs, configures and starts consul as a systemd service
2. Performs status checks
3. Enables TLS (using self-signed CA) for incoming, outgoing connections, verifies hostname 
4. Configurable for deploying in client/server mode
5. Creates cluster of consul nodes
6. Adds/removes nodes dynamically based on changes in inventory file

Notes: 

- Currently, The private keys, certs and root certificates are copied to servers from "files" folder of consul role.  