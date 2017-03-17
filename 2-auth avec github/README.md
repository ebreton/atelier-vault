# README #

### Seconde étape: github ###

Jusqu'à présent, vous utilisiez (sans le savoir?) l'utilisateur *root* qui vient avec votre serveur Vault local.

Ce n'est pas... optimum.

On va donc restreindre l'accès grâce à github.

### A quoi ca sert ? ###

Restreindre l'accès (authentication) et contrôler les permissions (authorisation)

### Comment on a fait pratiquement ? ###

On crée, on tue et on utilise des *tokens* pour utiliser Vault

```
$ vault token-create
Key             Value
token           c2c2fbd5-2893-b385-6fa5-30050439f698
...
$ vault token-revoke c2c2fbd5-2893-b385-6fa5-30050439f698
Success! Token revoked if it existed.
$ vault auth d08e2bd5-ffb0-440d-6486-b8f650ec8c0c
Successfully authenticated! The policies that are associated
with this token are listed below:

root
```

Mais on peut aussi s'appuyer sur des solutions complémentaires, comme github.


1. Un peu de configuration tout d'abord

```
$ vault auth-enable github
...
$ vault write auth/github/config organization=hashicorp
...
$ vault write auth/github/map/teams/default value=default
...
```
2. créez votre clef github dans [Settings>Personnal access tokens](https://github.com/settings/tokens)

3. identifiez vous !

```
$ vault auth -method=github token=e6919b17dd654f2b64e67b6369d61cddc0bcc7d5
Successfully authenticated! The policies that are associated
with this token are listed below:

default
```

On a vu que les permissions sont pour l'instant régies par la *policy* `default`. On peut changer ça, par exemple avec le fichier acl.hcl. 

```
$ vault policy-write secret acl.hcl
...
$ vault write auth/github/map/teams/default value=secret
...
```
