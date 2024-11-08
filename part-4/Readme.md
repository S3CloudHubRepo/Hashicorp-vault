
# HashiCorp Vault Secret Engine Basics

In this guide, we'll explore how to manage Secret Engines in HashiCorp Vault. Secret Engines allow you to securely store various types of credentials and secrets for different cloud providers, as well as custom secrets.

## Overview

HashiCorp Vault integrates with several cloud providers like AWS, Google Cloud, Oracle Cloud, and Azure. You can enable Secret Engines to securely store credentials for these providers within your Vault instance. In this guide, we'll go over commands to list, enable, and disable Secret Engines in HashiCorp Vault.

## Commands

### 1. List Available Secret Engines

To list all Secret Engines currently configured in your Vault server:

```bash
vault secrets list
```

This command will display all paths associated with Secret Engines. Some default paths, such as `identity`, `secret`, and `sys`, are provided by Vault on initial setup.

### 2. Enable a Secret Engine

To enable a Secret Engine, use the `vault secrets enable` command. For example, to enable the AWS Secret Engine on the path `aws`:

```bash
vault secrets enable -path=aws aws
```

After running this command, you can verify that the AWS Secret Engine is enabled by listing the Secret Engines again:

```bash
vault secrets list
```

### 3. Disable a Secret Engine

If you no longer need a specific Secret Engine, you can disable it with the `vault secrets disable` command. For instance, to disable the AWS Secret Engine on the path `aws`:

```bash
vault secrets disable aws
```

Ensure you use the correct path name when disabling a Secret Engine; otherwise, Vault may not recognize the path.

To verify that the Secret Engine has been disabled, list the Secret Engines once more:

```bash
vault secrets list
```

This should show the updated list without the disabled path.

## Next Steps

In the next session, we will cover how to manage dynamic secrets in HashiCorp Vault. Dynamic secrets are temporary credentials generated on-demand, often used with IAM roles and policies for enhanced security.

## Summary of Commands

- **List Secret Engines:** `vault secrets list`
- **Enable Secret Engine:** `vault secrets enable -path=<path> <engine_type>`
- **Disable Secret Engine:** `vault secrets disable <path>`

---

Thank you for following along! This reference will help you manage Secret Engines in HashiCorp Vault confidently.
