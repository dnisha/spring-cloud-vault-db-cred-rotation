### Enable the approl secrets engine and secret path
```
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
### Create token
```
vault token create -policy="jenkins" -period="1h"   
```
### Revoke token
```
vault token revoke <token>
```
### Create token with ttl
```
vault token create -period=30m
```
### Renew token
```
vault token renew <token>
```
### Lookup token details
```
vault token lookup <token>
```
### Lookup token details
```
vault read /database/mysql/webapp/
```

