# README #

### Seconde étape: AWS ###

La première étape stocke vos secrets dans la mémoire... donc oui, si vous redémarrez le serveur Vault (ou fermez votre terminal). Gameover.

Vous avez un peu mieux à disposition en stockant dans un fichier (si vous avez suivi le tuto) mais ce n'est pas la panacée...

On va donc passer sur les Amazon Web Services, qui en plus nous fournissent des fonctionnalités sympas, genre : générer pour nous un secret dynamiquement avec une date d'expiration.

A noter qu'on délocalise le stockage (ils appellent ça *backend*) mais le serveur tourne toujours en local.

### A quoi ca sert ? ###

Et bien vos secrets 1) ne sont plus sur votre machine, ni dans la mémoire ni dans un fichier et 2) vous n'aurez plus de mots de passe *toto1234*, et 3) ils expirent automatiquement, et 4) ils sont générés par une API, donc manuellement ou automatiquement à votre bon vouloir.


### Comment on a fait pratiquement ? ###

Je ne vais pas répéter tout le tuto qui [explique ca plus calmement](https://www.vaultproject.io/intro/getting-started/dynamic-secrets.html), mais en gros

1. vous générez un token dans votre compte [AWS>Identification et sécurité](https://console.aws.amazon.com/iam/home#/security_credential)

2. vous définissez un rôle, c-a-d les permissions IAM (système amazon) dans un fichier (par exemple policy.json)

3. configurer votre serveur pour utiliser AWS, et les permissions

```
$ vault mount aws
Successfully mounted 'aws' at 'aws'!
$ vault write aws/config/root \
    access_key=AKIAI4SGLQPBX6CSENIQ \
    secret_key=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
Success! Data written to: aws/config/root
$ vault write aws/roles/deploy policy=@policy.json
Success! Data written to: aws/roles/deploy
```

Et voila! Vous pouvez maintenant générer vos clefs avec votre client (et server) Vault en vous appuyant sur Amazon

```
$ vault read aws/creds/deploy
Key         Value
lease_id    aws/creds/deploy/0d042c53-aa8a-7ce7-9dfd-310351c465e5
access_key  AKIAJFN42DVCQWDHQYHQ
secret_key  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
```
