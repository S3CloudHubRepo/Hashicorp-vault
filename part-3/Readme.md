
# HashiCorp Vault CLI Tutorial: Read, Write, and Delete Operations

Welcome to this tutorial on managing secrets in HashiCorp Vault using the command-line interface (CLI). This guide will walk you through enabling paths, and performing read, write, and delete operations for secrets in Vault. Follow along to learn essential commands for storing, retrieving, and removing secrets securely.

## Table of Contents

- [Introduction](#introduction)
- [Vault CLI Commands Overview](#vault-cli-commands-overview)
  - [1. Enable Secret Engine Path](#1-enable-secret-engine-path)
  - [2. Write Operation](#2-write-operation)
  - [3. Read Operation](#3-read-operation)
  - [4. Read in JSON Format](#4-read-in-json-format)
  - [5. List All Secret Paths](#5-list-all-secret-paths)
  - [6. Delete Operation](#6-delete-operation)
  - [7. Verify Deletion](#7-verify-deletion)
- [Conclusion](#conclusion)
- [Next Steps](#next-steps)

---

## Introduction

In this tutorial, we’ll explore the key operations for managing secrets in Vault, specifically the read, write, and delete commands. Before storing any data, we need to enable a custom path in the Vault secret engine. Once this path is enabled, we can securely store and retrieve secrets using simple CLI commands.

---

## Vault CLI Commands Overview

### 1. Enable Secret Engine Path

To store secrets at a custom path, enable the path within the Vault secrets engine:

```bash
vault secrets enable -path=my kv
```

- **vault secrets enable**: Enables a path in the Vault secrets engine.
- **-path=my**: Sets the custom path as my.
- **kv**: Specifies that the path will use the key-value (kv) storage engine.

> **Note**: Ensure your Vault server is running before executing any commands.

---

### 2. Write Operation

To store (or "write") a secret in Vault, use the following command:

```bash
vault kv put my/path key-1=value-1
```

- **vault kv put**: This command specifies that you’re storing data in the key-value storage engine.
- **my/path**: The custom path where your secret is stored.
- **key-1=value-1**: A key-value pair representing the secret, where key-1 is the key and value-1 is the associated value.

### 3. Read Operation

Retrieve (or "read") a stored secret with this command:

```bash
vault kv get my/path
```

- **vault kv get**: Fetches the stored data at the specified path.
- **my/path**: The path from which you want to retrieve the secret.

### 4. Read in JSON Format

To view the secret in JSON format, use:

```bash
vault kv get -format=json my/path
```

- **-format=json**: Outputs the data in JSON format, ideal for scripts or integration with other tools.

### 5. List All Secret Paths

List all registered secret paths with this command:

```bash
vault secrets list
```

- **vault secrets list**: Displays all paths enabled in the Vault secrets engine, including any default paths like secret/ and identity/, along with your custom paths.

### 6. Delete Operation

To delete a secret from Vault, use:

```bash
vault kv delete my/path
```

- **vault kv delete**: Removes the data at the specified path.
- **my/path**: The path from which you want to delete the stored secret.

### 7. Verify Deletion

After deleting, you can confirm the removal by attempting to read the data again. A ‘no value found’ message confirms that the deletion was successful:

```bash
vault kv get -format=json my/path
```

---

## Conclusion

You’ve successfully learned the essential CLI commands for managing secrets in Vault. With these commands, you can enable paths, store, retrieve, and delete secrets with ease. 

---

## Next Steps

In the next session, we’ll dive deeper into Vault’s secret engines, covering how to enable and manage different types of secret engines, like AWS. Stay tuned for more advanced topics in secrets management with Vault!

---

Happy learning, and feel free to refer back to this guide whenever you need a refresher on Vault CLI basics!
