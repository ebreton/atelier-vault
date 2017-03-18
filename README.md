# README #

### Pour quoi ? ###

Ce repo est construit à partir de l'Atelier de l'Innovation Innovante (AII) du 17 mars.

L'objectif était de mettre en place un Vault en suivant le [tutoriel](https://www.vaultproject.io/intro/getting-started/install.html), de voir si on aime, et si on peut l'utiliser plus loin...

Le tuto a une douzaine de pages, dont j'ai tiré la quintescense substance dans 4 pages du wiki. 

Vous trouverez les éléments de code de chaque étape dans les sous-répertoires suivant:

0. local (prise en main)
1. secrets avec aws
2. auth avec github
3. stockage avec consul

### Pressé ? (in progress) ###

**en cours de rédaction. pas encore bon**

Créez vos tokens [AWS](https://console.aws.amazon.com/iam/home#/security_credential), [GitHub](https://github.com/settings/tokens), et go go go

```
$ cp conf/variables.env.sample conf/variables.env && vi conf/variables.env
...

$ echo "creating vault server..." > /dev/null
$ docker-compose up -d && docker-compose logs --tail 40

$ echo "initializing vault..."  > /dev/null
$ curl \
  -X PUT \
  -d "{\"secret_shares\":1, \"secret_threshold\":1}" \
  https://127.0.0.1:8200/v1/sys/init
{
  "root_token": "4f66bdfa-f5e4-209f-096c-6e01d863c145",
  ...
  "keys": [
    "170c2c4b3332b0b81802f245aecfaae547cb30a2310be74315b3fa633ca3cef4"
  ]
}

$ echo "unsealing vault..." > /dev/null
$ export VAULT_TOKEN=4f66bdfa-f5e4-209f-096c-6e01d863c145
$ curl \
    -X PUT \
    -d '{"key": "FwwsSzMysLgYAvJFrs+q5UfLMKIxC+dDFbP6YzyjzvQ="}' \
    http://127.0.0.1:8200/v1/sys/unseal
{
  ...
  "sealed": false
}

$ echo "enabling authentication...." > /dev/null
$ curl -X POST -H "X-Vault-Token:$VAULT_TOKEN" ...


```

### Curieux ? ###

Alors, vous pouvez lire le [wiki](https://github.com/ebreton/atelier-vault/wiki)


## Aller plus loin ? ##

A chaque étape, vous trouverez une section "Aller plus loin" ou je tente d'appliquer la leçon dans le monde docker... En attendant, direction [0-local](https://github.com/ebreton/atelier-vault/tree/master/0-local)