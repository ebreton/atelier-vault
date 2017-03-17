# README #

### Première étape: local ###

Vous allez faire tourner votre Vault en local, de manière tout à fait non-sécurisée, et non-recommandée (pour une prod).

### A quoi ca sert ? ###

Surtout à jouer avec les commandes de bases, comme `vault write` et `vault read`, et avec la documentation en ligne de commande des API

```
$ vault help
...
$ vault path-help
...
```

### Comment on a fait pratiquement ? ###


Vous pouvez récupérer le binaire qui [correspond à votre machine](https://www.vaultproject.io/downloads.html). Il sert à la fois d'agent (client) et de serveur (serveur ;))

Mettez le dans votre `.../bin` repertoire-qui-va-bien (c-a-d dans votre PATH)

Avec deux terminaux et une variable d'environnement, vous êtes en route.

**côté serveur**
```
$ vault server -dev
...
Unseal Key: 2252546b1a8551e8411502501719c4b3
Root Token: 79bd8011-af5a-f147-557e-c58be4fedf6c
...
```

Copiez-collez votre `Root token` quelque part, c'est ce qui vous permettra de redevenir admin lorsque vous jouerez avec l'authentification plus tard

**côté client**
```
$ export VAULT_ADDR='http://127.0.0.1:8200'
$ vault write secret/hello value=world
Success! Data written to: secret/hello
```

### Pages couvertes du tuto ###

* [Install Vault](https://www.vaultproject.io/intro/getting-started/install.html)
* [Starting the Server](https://www.vaultproject.io/intro/getting-started/dev-server.html)
* [Your First Secret](https://www.vaultproject.io/intro/getting-started/first-secret.html)
* [Built-in Help](https://www.vaultproject.io/intro/getting-started/help.html)
