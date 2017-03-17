# README #

### Seconde étape: AWS ###

Dans la première étape, vous générez vos secrets avec vos petites mains pour vos utilisateurs préférés.

A l'ancienne.

```
$ vault write secret/manu value=toto
...
```

On va donc passer sur les Amazon Web Services, vont générer pour nous un secret dynamiquement, avec une date d'expiration.

### A quoi ca sert ? ###

Et bien vos secrets 1) n'auront plus de valuer *toto*, et 2) ils expirent automatiquement, et 3) ils sont générés par une API, donc manuellement ou automatiquement à la demande.


### Comment on a fait pratiquement ? ###

Je ne vais pas répéter tout le tuto qui explique ca plus calmement, mais en gros:

1. vous générez un token dans votre compte [AWS>Identification et sécurité](https://console.aws.amazon.com/iam/home#/security_credential)

2. vous définissez un rôle, c-a-d les permissions IAM (système amazon) dans un fichier (par exemple policy.json)

3. configurer votre serveur pour utiliser AWS, et les permissions

```
$ vault mount aws
...
$ vault write aws/config/root \
    access_key=AKIAI4SGLQPBX6CSENIQ \
    secret_key=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
...
$ vault write aws/roles/deploy policy=@policy.json
...
```

Et voila! Vous pouvez maintenant générer vos clefs avec votre client (et server) Vault en vous appuyant sur Amazon

```
$ vault read aws/creds/deploy
Key         Value
lease_id    aws/creds/deploy/0d042c53-aa8a-7ce7-9dfd-310351c465e5
access_key  AKIAJFN42DVCQWDHQYHQ
secret_key  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
```

### Pages couvertes du tuto ###

* [Secret Backends](https://www.vaultproject.io/intro/getting-started/secret-backends.html)
* [Dynamic Secrets](https://www.vaultproject.io/intro/getting-started/dynamic-secrets.html)