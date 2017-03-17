# README #

### Pour quoi ? ###

Ce repo est construit à partir de l'Atelier de l'Innovation Innovante (AII) du 17 mars.

L'objectif était de mettre en place un Vault en suivant le [tutoriel](https://www.vaultproject.io/intro/getting-started/install.html), de voir si on aime, et si on peut l'utiliser plus loin...

### Comment je commence ? ###

Avec

* une machine (un Mac dans mon cas)
* un collègue pair-programmer
* et le navigateur sur la [page du tuto](https://www.vaultproject.io/intro/getting-started/install.html)

### Comment je vérifie que tout s'est bien passé ? ###

à la fin, un [consul](https://www.hashicorp.com/products/consul/) tourne sur votre machine pour stocker vos secrets, et vous pouvez y acceder avec votre compte GitHub. Si vous avez accroché, vous pouvez créer des tokens à la volée grâce à EC2, car vous avez défini votre compte AWS comme backend des secrets.