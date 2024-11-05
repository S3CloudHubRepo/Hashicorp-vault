Here's a `README.md` file that captures the essentials from the script for easy reference:

# Getting Started with HashiCorp Vault on Ubuntu

This guide walks through the steps to start and stop HashiCorp Vault on Ubuntu, highlighting the key components and commands needed for development mode. 

## Table of Contents
1. [Vault Operating Modes](#vault-operating-modes)
2. [Starting Vault in Development Mode](#starting-vault-in-development-mode)
3. [Key Components in Development Mode](#key-components-in-development-mode)
4. [Exporting Environment Variables](#exporting-environment-variables)
5. [Checking Vault Status](#checking-vault-status)

---

### Vault Operating Modes

Vault can operate in two main modes:

- **Development Mode**: Designed for testing and development purposes. Not secure for production environments.
- **Server Mode**: Intended for production use with more secure configurations.

> **Note:** Development Mode should only be used for non-production scenarios, as data is stored in memory and lost when Vault stops.

### Starting Vault in Development Mode

To start Vault in Development Mode, open a terminal where Vault is installed and run:

```bash
vault server -dev


This command starts Vault in Development Mode. You’ll see a message indicating that Development Mode should not be used in production.

### Key Components in Development Mode

Once Vault starts, you’ll see details for the following key components:

1. **Port**: The API address showing which port Vault is running on.
2. **Storage**: Vault uses in-memory storage by default in Development Mode. All data is stored temporarily and will be lost when Vault stops. In production, storage would persist on disk or in a database.
3. **Unseal Key**: A unique key required to unseal Vault.
4. **Root Token**: An admin-level token for initial setup and operations.

It’s recommended to **save the Unseal Key and Root Token** in a secure place for reference.

### Exporting Environment Variables

To simplify interaction with Vault, export the `VAULT_ADDR` and `VAULT_TOKEN` environment variables. This allows Vault commands to automatically use these values.

```bash
export VAULT_ADDR="http://127.0.0.1:<port>"
export VAULT_TOKEN="<root_token>"
```

Replace `<port>` and `<root_token>` with the actual values from your Vault terminal output.

### Checking Vault Status

To verify that Vault is running correctly, run:

```bash
vault status
```

This command outputs the current status of the Vault server. If the server is correctly initialized, you’ll see a successful status message.

---

### Next Steps

You’re now set up to start using Vault in Development Mode! In our next guide, we’ll cover reading, writing, and deleting secrets with HashiCorp Vault.

---

## Additional Resources

- [HashiCorp Vault Documentation](https://www.vaultproject.io/docs)
- [Getting Started with Vault](https://learn.hashicorp.com/collections/vault/getting-started)

---

Thank you for following this guide. For more tutorials, make sure to subscribe to our channel!
```

This `README.md` provides a concise yet comprehensive overview, covering the essential commands and concepts.
