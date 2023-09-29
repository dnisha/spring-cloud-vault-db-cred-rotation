### Enable github authentication
```
vault auth enable github
```
### Setup organization name
```
vault write auth/github/config organization=<organization-name>
```
### Read details
```
vault read auth/github/config
```
### Provide policy
```
vault write auth/github/map/teams/dev value=dev 
```
### Read policy
```
vault read auth/github/map/teams/dev
```