### Enable the approl secrets engine and secret path
```
vault auth enable approle
vault secrets enable -path=database/mysql kv
```
### Create database secret
```
vault kv put database/mysql/webapp db-name="users" username="admin" password="password@123"
```
### Read path
```
vault kv get -mount=database/mysql/ webapp 
```
### Configure policy named jenkins
```
vault policy write jenkins -<<EOF
path "database/mysql/webapp" {
  capabilities = [ "read" ]
}
EOF
```
### Create approle with policy
```
vault write auth/approle/role/jenkins token_policies="jenkins" token_ttl=1h token_max_ttl=4h secret_id_num_uses=5
```
### Read attached policy
```
vault read auth/approle/role/jenkins
```
### Get the role-id
```
vault read auth/approle/role/jenkins/role-id
```
### Get the secred-id
```
vault write -f auth/approle/role/jenkins/secret-id
```
### Get the token from vault
```
vault write auth/approle/login role_id="85c578ef-84ec-f538-0576-6c4cfac50ef0" \
    secret_id="a02c745e-2f73-04b5-badf-e2572c4de8df"
```
### Get the secrets
```
vault kv get /database/mysql/webapp 
```

