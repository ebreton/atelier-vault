# README #

### Dernière étape: Consul ###

Jusque là, vos secrets étaient stockés dans la mémoire... donc oui, si vous redémarrez le serveur Vault (ou fermez votre terminal). Gameover.

Vous avez un peu mieux à disposition en stockant dans un fichier (si vous avez suivi le tuto) mais ce n'est pas la panacée...

On va donc passer sur Consul.

A noter qu'on délocalise le stockage mais le serveur tourne toujours en local.

### A quoi ca sert ? ###

Et bien vos secrets ne sont plus sur votre machine, ni dans la mémoire ni dans un fichier.

Bienvenue dans quelque chose qui commence à être utilisable en production.


### Comment on a fait pratiquement ? ###

1. Démarrez un consul

2. Récupérez le fichier de configuration consul.hcl qui dit quelle backend de stockage utiliser.

3. Démarrez le serveur avec le fichier de configuration

```
$ vault server -config=example.hcl
...
```

4. Initialisez votre coffre, c-a-d générez puis utilisez les clefs qui vous permettront de dévérouiller le coffre.

### Dévérouiller le coffre ? ###

```
$ vault init
Key 1: 427cd2c310be3b84fe69372e683a790e01
Key 2: 0e2b8f3555b42a232f7ace6fe0e68eaf02
Key 3: 37837e5559b322d0585a6e411614695403
Key 4: 8dd72fd7d1af254de5f82d1270fd87ab04
Key 5: b47fdeb7dda82dbe92d88d3c860f605005
Initial Root Token: eaf5cc32-b48f-7785-5c94-90b5ce300e9b

Vault initialized with 5 keys and a key threshold of 3!
...
```

L'idée est la même que dans les banques, ou le banquier possède une clef, et vous la seconde. Il faut les deux pour ouvrir le coffre.

Ici, vous générez 'x' clefs et il en faut la majorité pour ouvrir le coffre. Vous pouvez distribuer les clefs à des gens de confiance, et à chaque fois que le coffre sera vérouillé, il vous faudra une majorité de gens qui utilise leur clef

```
$ vault unseal
Key (will be hidden):
Sealed: true
Key Shares: 5
Key Threshold: 3
Unseal Progress: 1
```

### Pages couvertes du tuto ###

* [Deploy Vault](https://www.vaultproject.io/intro/getting-started/deploy.html)
