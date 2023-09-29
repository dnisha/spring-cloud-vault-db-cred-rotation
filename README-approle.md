### Enable the approl secrets engine and secret path
```
vault auth enable approle
```

### Configure policy named jenkins
```
vault policy write spring-boot  -<<EOF
path "database/creds/myrole" {
  capabilities = [ "read" , "create"]
}
EOF
```
### Create approle with policy
```
vault write auth/approle/role/spring-boot token_policies="spring-boot" token_ttl=1h token_max_ttl=4h secret_id_num_uses=0 token_num_uses=0
```
### Read attached policy
```
vault read auth/approle/role/spring-boot
```
### Get the role-id
```
vault read auth/approle/role/spring-boot/role-id
```
### Get the secred-id
```
vault write -f auth/approle/role/spring-boot/secret-id
```
### Get the token from vault
```
vault write auth/approle/login role_id="8db16328-bac6-d568-a738-6c597620bb28" \
    secret_id="ed37b6e4-2b19-8fc8-184c-feaa0ee5ef21"
```
