# README #

### Pour quoi ? ###

Ce repo est construit à partir de l'Atelier de l'Innovation Innovante (AII) du 17 mars.

L'objectif était de mettre en place un Vault en suivant le [tutoriel](https://www.vaultproject.io/intro/getting-started/install.html), de voir si on aime, et si on peut l'utiliser plus loin...

Le tuto a une douzaine de pages, que j'ai regroupées en 4 étapes, chacune ayant un objectif annoncé:

0. local (prise en main)
1. secrets avec aws
2. auth avec github
3. stockage avec consul

### Pressé ? ###

*saississez vos tokens [AWS](https://console.aws.amazon.com/iam/home#/security_credential), [GitHub](https://github.com/settings/tokens)*, et up up up

```
$ cp conf/variables.env.sample conf/variables.env && vi conf/variables.env
...

$ docker-compose up -d
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