# README #

### Première étape: local ###

Vous pouvez récupérer le binaire qui [correspond à votre machine](https://www.vaultproject.io/downloads.html). Il sert à la fois d'agent (client) et de serveur (serveur ;))

Mettez le dans votre `.../bin` repertoire-qui-va-bien (c-a-d dans votre PATH)

Avec deux terminaux et une variable d'environnement, vous êtes en route.

```
côté serveur
$ vault server -dev
...
```

```
côté client
$ export VAULT_ADDR='http://127.0.0.1:8200'
$ vault write secret/hello value=world
Success! Data written to: secret/hello
```


### A quoi ca sert ? ###

Surtout à jouer avec les commandes de bases, comme `vault write` et `vault read`

```
$ vault help
...
```

Et avec la documentation en ligne de commande des API

```
$ vault path-help
...
```