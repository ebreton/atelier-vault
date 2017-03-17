# README #

### Pour quoi ? ###

Ce repo est construit à partir de l'Atelier de l'Innovation Innovante (AII) du 17 mars.

L'objectif était de mettre en place un Vault en suivant le [tutoriel](https://www.vaultproject.io/intro/getting-started/install.html), de voir si on aime, et si on peut l'utiliser plus loin...

Le tuto a une douzaine de pages, que j'ai regroupées en 4 étapes, chacune ayant un objectif annoncé:

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
  "keys_base64": [
    "FwwsSzMysLgYAvJFrs+q5UfLMKIxC+dDFbP6YzyjzvQ="
  ],
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
  "cluster_id": "1c2523c9-adc2-7f3a-399f-7032da2b9faf",
  "cluster_name": "vault-cluster-9ac82317",
  "version": "0.6.2",
  "progress": 0,
  "n": 1,
  "t": 1,
  "sealed": false
}

$ echo "enabling authentication...." > /dev/null

$ curl -X POST -H "X-Vault-Token:$VAULT_TOKEN" ...


```

### Curieux ? ###

Alors, vous pouvez lire cette page jusqu'au bout, et enchainer sur le [0-local](https://github.com/ebreton/atelier-vault/tree/master/0-local)

### Comment je commence ? ###

Avec

* une machine (un Mac dans mon cas)
* un collègue pair-programmer
* et le navigateur sur la [page du tuto](https://www.vaultproject.io/intro/getting-started/install.html)

### Comment je vérifie que tout s'est bien passé ? ###

à la fin, un [consul](https://www.hashicorp.com/products/consul/) et un Vault tournent sur votre machine pour stocker/gérer vos secrets, et vous pouvez y acceder avec votre compte GitHub. Si vous avez accroché, vous pouvez créer des tokens à la volée grâce à EC2, car vous avez défini votre compte AWS comme backend des secrets.

## Aller plus loin ? ##

A chaque étape, vous trouverez une section "Aller plus loin" ou je tente d'appliquer la leçon dans le monde docker...