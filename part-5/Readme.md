
# Dynamic Secrets with HashiCorp Vault and AWS

Welcome to the **Dynamic Secrets with HashiCorp Vault and AWS** project! This repository provides a detailed guide and commands to enable dynamic secrets generation in AWS using HashiCorp Vault, ensuring secure, time-limited access for your AWS resources.

## 📘 About This Tutorial

In this session, you'll learn:

1. **How to Enable the AWS Secret Engine** in HashiCorp Vault.
2. **Configure AWS Root Access** for generating dynamic secrets.
3. **Set Up Roles** in AWS to dynamically create access and secret keys.
4. **Generate Dynamic Secrets** using HashiCorp Vault.
5. **Revoke Dynamic Secrets** before their expiration, enhancing your security control.

Each section of the tutorial builds upon the previous, providing a concrete example of securely managing temporary AWS credentials.

## 📋 Prerequisites

To follow this guide, ensure you have:

- **AWS Access Key and Secret Key** for the root user account.
- **HashiCorp Vault** installed and configured on your system.
- Access to the terminal.

## 🚀 Getting Started

Follow these steps to generate dynamic AWS secrets with HashiCorp Vault:

### Step 1: Enable the AWS Secret Engine Path

To begin, enable the AWS secret engine in Vault:

```bash
vault secrets enable -path=aws aws
```

Verify that the secret engine has been enabled by listing the secrets:

```bash
vault secrets list
```

### Step 2: Configure AWS Root Access

Now, configure the root access in Vault with your AWS root credentials. Replace `YOUR_ACCESS_KEY`, `YOUR_SECRET_KEY`, and `YOUR_REGION` with your actual details.

```bash
vault write aws/config/root access_key=YOUR_ACCESS_KEY secret_key=YOUR_SECRET_KEY region=YOUR_REGION
```

### Step 3: Set Up a Role for Dynamic Secrets

Define a role, `my-ec2-role`, to allow specific actions on EC2 instances. This example grants all actions, but customize as per your security requirements.

```bash
vault write aws/roles/my-ec2-role credential_type=iam_user policy_document=-<<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
EOF
```

### Step 4: Generate the Dynamic Secret

Once the role is set, generate dynamic secrets for `my-ec2-role` using:

```bash
vault read aws/creds/my-ec2-role
```

This command will output a new AWS access key and secret key, along with their lease duration.

### Step 5: Revoke the Dynamic Secret

If you need to revoke these credentials before they expire, use the `vault lease revoke` command with the lease ID generated in Step 4:

```bash
vault lease revoke LEASE_ID
```

This instantly invalidates the dynamically generated credentials.

## 🛠 Commands Overview

| Command                                    | Description                                    |
|--------------------------------------------|------------------------------------------------|
| `vault secrets enable -path=aws aws`       | Enables AWS secret engine in Vault             |
| `vault write aws/config/root ...`          | Sets up AWS root configuration in Vault        |
| `vault write aws/roles/my-ec2-role ...`    | Creates a role in Vault with defined policies  |
| `vault read aws/creds/my-ec2-role`         | Generates dynamic AWS credentials              |
| `vault lease revoke LEASE_ID`              | Revokes the generated credentials by lease ID  |

## 📹 Video Tutorial

For a detailed walkthrough, check out the video tutorial in this repository or visit our YouTube channel [here](https://www.youtube.com/watch?v=zgC78QRPBfM&list=PL_OdF9Z6GmVZV62x9JI_pk31e2YdHyKuf&pp=iAQB) for the full step-by-step guide.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a pull request.

## 📄 License

This project is licensed under the MIT License.

---

By following these steps, you’ll learn to create and manage secure, temporary AWS credentials using HashiCorp Vault. Stay tuned for more tutorials on cloud security and dynamic secrets! 
