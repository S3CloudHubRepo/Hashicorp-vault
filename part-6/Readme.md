
# HashiCorp Vault Token and GitHub Authentication Guide

This guide provides a comprehensive walkthrough for using token authentication and GitHub authentication in HashiCorp Vault.

---

## 1. Token Authentication in Vault

### Step 1: Start Vault in Development Mode
When starting Vault in development mode, a root token is generated automatically. This token is used to authenticate.

```bash
vault server -dev
```

### Step 2: Logging in with Root Token
After starting Vault, use the following command to log in. Enter the root token when prompted.

```bash
vault login
```

### Step 3: Regenerating Root Token
In case you forget to save the root token, you can generate a new one.

```bash
vault token create
```

### Step 4: Revoking a Token
To revoke a token, use the following command:

```bash
vault token revoke <TOKEN>
```

---

## 2. GitHub Authentication in Vault

### Step 1: GitHub Setup
1. **Create a GitHub Organization and Team** if not already created.
2. **Generate a Personal Access Token** in GitHub by navigating to:
   `Settings > Developer Settings > Personal Access Tokens`.

### Step 2: Enabling GitHub Authentication in Vault
Enable GitHub as an authentication method in Vault.

```bash
vault auth enable github
```

### Step 3: Configuring GitHub Authentication in Vault
Map your GitHub organization and team with Vault policies.

#### Organization Create:
```bash
 vault write auth/github/config organization=vault-demo-s3cloudhub
```

#### Team Mapping:
```bash
vault write auth/github/map/teams/YOUR_TEAM policies=default,application
```

### Step 4: Login with GitHub Personal Access Token
Log in to Vault using the GitHub access token:

```bash
vault login -method=github
```

### Step 5: Removing GitHub Authentication
If you need to disable GitHub authentication, use:

```bash
vault auth disable github
```

---

## Resources
- [HashiCorp Vault Documentation](https://www.vaultproject.io/docs)
- [GitHub Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

---

By following these steps, you can successfully authenticate into Vault using both root token and GitHub methods, enhancing security and flexibility.

