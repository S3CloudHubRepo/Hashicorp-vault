# Vault Integration

Here are the detailed steps for each of these steps:

## Create an AWS EC2 instance with Ubuntu

To create an AWS EC2 instance with Ubuntu, you can use the AWS Management Console or the AWS CLI. Here are the steps involved in creating an EC2 instance using the AWS Management Console:

- Go to the AWS Management Console and navigate to the EC2 service.
- Click on the Launch Instance button.
- Select the Ubuntu Server xx.xx LTS AMI.
- Select the instance type that you want to use.
- Configure the instance settings.
- Click on the Launch button.

## Install Vault on the EC2 instance

To install Vault on the EC2 instance, you can use the following steps:

**Install gpg**

```
sudo apt update && sudo apt install gpg
```

**Download the signing key to a new keyring**

```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

**Verify the key's fingerprint**

```
gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
```

**Add the HashiCorp repo**

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

```
sudo apt update
```

**Finally, Install Vault**

```
sudo apt install vault
```

**Check vault installation**

```
vault --version
```
