# README #

### Dernière étape: Consul ###

Jusque là, vos secrets étaient stockés dans la mémoire... donc oui, si vous redémarrez le serveur Vault (ou fermez votre terminal). Gameover.

Vous avez un peu mieux à disposition en stockant dans un fichier (si vous avez suivi le tuto) mais ce n'est pas la panacée...

On va donc passer sur Consul.

A noter qu'on délocalise le stockage (ils appellent ça *backend*) mais le serveur tourne toujours en local.

### A quoi ca sert ? ###

Et bien vos secrets ne sont plus sur votre machine, ni dans la mémoire ni dans un fichier. Bienvenue dans quelque chose qui commence à être utilisable en production.


### Comment on a fait pratiquement ? ###


### Pages couvertes du tuto ###

* [Deploy Vault](https://www.vaultproject.io/intro/getting-started/deploy.html)
