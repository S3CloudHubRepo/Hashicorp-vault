
# Deploying HashiCorp Vault in Production Mode

This guide provides step-by-step instructions for deploying HashiCorp Vault in a production environment, transitioning from a development setup to production-ready deployment.

## 1. Stop Vault Development Mode

First, stop any Vault instance running in development mode. Open the terminal where Vault is running and press `Ctrl + C` to shut down the development server. Verify it has stopped by running:
```bash
vault status
```
You should see a "connection refused" message, indicating that the development server is no longer active.

## 2. Reset the Vault Token

Reset the Vault token to clear any lingering development credentials:
```bash
unset VAULT_TOKEN
```

## 3. Create the Production Configuration File

Create a configuration file named `config.hcl` to specify Vault’s production settings. Use the following configuration:

```hcl
storage "raft" {
  path    = "./vault/data"
  node_id = "node1"
}

listener "tcp" {
  address     = "0.0.0.0:8200"
  tls_disable = "true"
}

api_addr = "http://127.0.0.1:8200"
cluster_addr = "https://127.0.0.1:8201"
ui = true
```
### Explanation of Configuration Parameters:
- **Storage**: Defines Raft storage for persistent data storage at `./vault/data`.
- **Listener**: Sets up TCP listener at localhost. TLS is disabled for this example.
- **API and Cluster Addresses**: Specifies API and cluster endpoints.
- **UI**: Enables the Vault web interface.

## 4. Create the Storage Directory

Create the storage directory for the 'Raft' backend with the following command:

```bash
mkdir -p ./vault/data
```

## 5. Start Vault in Production Mode

Start Vault using the config file:

```bash
vault server -config=config.hcl
```

This initiates Vault with the specified production settings. Vault is now running in production mode.

## 6. Export Vault Address

To ensure the client can communicate with the Vault server, export the Vault address:

```bash
export VAULT_ADDR='http://127.0.0.1:8200'
```

## 7. Initialize Vault

Initialize Vault to generate unseal keys and a root token:

```bash
vault operator init
```

This command provides the unseal keys and root token. Store these securely as they are critical for accessing and managing Vault.

## 8. Unseal Vault

Vault starts in a sealed state. Use the following command multiple times with unseal keys to unseal Vault:

```bash
vault operator unseal
```

Alternatively, use the Vault UI to unseal Vault for a more interactive experience.

## 9. Access the Vault UI (AWS Example)

If you’re running Vault on an AWS EC2 instance, access it via the public IP. Open a browser and enter the IP address followed by the port:

```
http://<public_ip>:8200/ui
```

Use the unseal keys and root token in the UI to access Vault.

## 10. Explore the REST API

Vault provides a REST API for interacting from other applications or the command line. Here’s an example command to check if Vault is initialized:

```bash
curl -X GET $VAULT_ADDR/v1/sys/init
```

The REST API is useful for development and troubleshooting.

## Conclusion

You’ve now successfully deployed HashiCorp Vault in a production mode! In future tutorials, we’ll cover integrating Vault with Terraform on AWS to automate secrets generation and storage.

Stay tuned for more DevOps and security tutorials, and reach out with questions or feedback!
