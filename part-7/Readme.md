
# HashiCorp Vault Policy Management Tutorial

This README provides a reference for the commands used in the tutorial on managing policies in HashiCorp Vault.

## Commands Used in the Tutorial

### Section 1: Listing Vault Policies
```
$ vault policy list
```

### Section 2: Writing Your Custom Policy
```
$ vault policy write my-policy -
```
Insert the following HCL definitions:
```hcl
EOF
Dev servers have version 2 of KV secrets engine mounted by default, so will
need these paths to grant permissions:
path "secret/data/*" {
  capabilities = ["create", "update"]
}

path "secret/data/foo" {
  capabilities = ["read"]
}
EOF
```
End this input with `EOF`.

### Section 3: Reading Vault Policy Details
```
$ vault policy read my-policy
```

### Section 4: Deleting a Vault Policy
```
$ vault policy delete my-policy
```

### Section 6: Attaching a Token to a Policy
```
$ export VAULT_TOKEN="$(vault token create -field token -policy=my-policy)"
```

### Section 5: Storing Credentials Using Your Policy
```
$ vault kv put -mount=secret creds password="my-long-password"
```

### Section 7: Associating Auth Method with Policy
```
$ vault write auth/approle/role/my-role \
    secret_id_ttl=10m \
    token_num_uses=10 \
    token_ttl=20m \
    token_max_ttl=30m \
    secret_id_num_uses=40 \
    token_policies=my-policy
```

### Section 8: Generating and Exporting Role ID and Secret ID
Generate Role ID:
```
export ROLE_ID="$(vault read -field=role_id auth/approle/role/my-role/role-id)"
```
Generate Secret ID:
```
export SECRET_ID="$(vault write -f -field=secret_id auth/approle/role/my-role/secret-id)"
```

## Conclusion

Follow these commands to manage policies effectively in your HashiCorp Vault setup.
