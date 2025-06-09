# Infos
[Download](https://developer.hashicorp.com/vault/downloads#windows)
[Documentation officielle](https://developer.hashicorp.com/vault/tutorials/auth-methods/approle?in=vault%2Fauth-methods)

## Prerequis
Il faut installer le [CLI de Vault](https://developer.hashicorp.com/vault/downloads).

## Health check
```
curl http://localhost:8200/v1/sys/health
```

## Mise en place role-id de confiance
0- Definir les variables d'environnement (ESSAI-LOCAL : https://hvaultintro.intro.techno.local:8200)
```
export VAULT_ADDR=http://127.0.0.1:8200
export VAULT_API_ADDR=http://127.0.0.1:8200
export VAULT_SKIP_VERIFY="True" 
Ou
$env:VAULT_ADDR="https://hvaultintro.intro.techno.local:8200"
$env:VAULT_API_ADDR="https://hvaultintro.intro.techno.local:8200"
$env:VAULT_SKIP_VERIFY="True" 
```

1- Authentification
```
Token -> vault login
UserPass -> vault login -method=userpass username=Sadri
LDAP -> vault login -tls-skip-verify -method=ldap username=sfe093pe
AppRole -> vault write auth/approle/login \
    role_id=2391896c-5958-d4ca-6071-77ac3e743f22 \
    secret_id=48192200-7d47-1820-2d18-3ce0e7feac0c
```

2- Activer approle
```
vault auth enable approle
```

3- Creation d'une policy : sd-policy
```
vault policy write sf-policy - <<EOF
path "auth/approle/*" {
  capabilities = [ "create", "read", "update", "delete", "list"]
}

path "G_Gestion/data/*" {
  capabilities = [ "read"]
}
EOF
```

4- Creation d'un role attache : 
- policy
- auth method
- ip
```
secret_id_num_uses=n => la n+1 eme fois il faut avoir un nouveau secret
secret_id_ttl= duree de vie du secret
vault write auth/approle/role/sd-role \
    secret_id_ttl=0m \
    token_num_uses=0 \
    token_ttl=0m \
    token_max_ttl=0m \
    secret_id_num_uses=0 \
    policies=sd-policy \
    bind_secret_id=false \
    secret_id_bound_cidrs=172.23.0.1/32
```

update
```
vault write auth/approle/role/sd-role \
    secret_id_bound_cidrs=10.167.100.23/32,10.182.41.181/32
```

Get Adresse IP (Gateway)
```
docker inspect -f '{{range .NetworkSettings.Networks}}{{.Gateway}}{{end}}' (docker ps --format "{{.ID}}" --filter="name=vault")
```

5- Verifier le role
```
vault read auth/approle/role/sd-role
```

6- Recuperer le role-id
```
vault read auth/approle/role/sd-role/role-id
```

7- Generer un secret-id (facultatif, car on a definit le role bind_secret_id=false et on a definit une machine de confiance secret_id_bound_cidrs)
```
vault write -force auth/approle/role/sd-role/secret-id

wrap
vault write -wrap-ttl=60s -force auth/approle/role/sd-role-3/secret-id
```

## Liste des polices
```
vault policy list
```

## Import policy
```
vault policy write my-policy /tmp/policy.hcl
```

## Create secret
```
vault kv put G_Gestion/test Login="SF-Login" Password="SF-Password"
```

## Read secrets
```
vault kv get G_Gestion/test
```

## Liste des roles
```
vault list auth/{auth_method}/role
```

## CRUD namespace (Entreprise version...)
```
vault namespace list
vault namespace create fonctionnel/
vault namespace create acceptation/
vault namespace delete ns1/
```

# Lock & Unlock
```
vault namespace lock ns1/
vault namespace unlock -unlock-key <unlock key> ns1/
```






``` cs
// Pour un compte de service
            //var authMethod = new LDAPAuthMethodInfo(_config.Login, _config.Password);

// Wrap method
            //string wrappingToken = "hvs.....";
            //var tokenAuthMethodInfo = new TokenAuthMethodInfo(wrappingToken);
            //IVaultClient vaultClientForUnwrapping = new VaultClient(new VaultClientSettings(_config.Address, tokenAuthMethodInfo));
            //Secret<Dictionary<string, object>> secretIdData = vaultClientForUnwrapping.V1.System
            //    .UnwrapWrappedResponseDataAsync<Dictionary<string, object>>(null).Result;
            //var secretId = secretIdData.Data["secret_id"]; // Grab the secret_id 
            //var authMethod = new AppRoleAuthMethodInfo(_config.RoleId, secretId.ToString());

            //var authMethod = new JWTAuthMethodInfo(".....", "....");

            // Approle+secretid
            //var authMethod = new AppRoleAuthMethodInfo(_config.RoleId, _config.SecretId);


            public class VaultParametres
    {
        public string Address { get; set; }
        public string RoleId { get; set; }
        public string SecretId { get; set; }
        public string Login { get; set; }
        public string Password { get; set; }
        public string MountPath { get; set; }
        public string DataSecretPath { get; set; }
    }
```