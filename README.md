# Sectiunea 6. Using Environment Variables & Secrets

## Conexiune la MongoDB in cloud

- Am creat cont in cloud-ul MongoDb (user: liviu.moraru@gmail.com)
- MONGODB_CLUSTER_ADDRESS: cluster0.iivyk6h.mongodb.net

Stringul de conectare: mongodb+srv://liviu:<password>@cluster0.iivyk6h.mongodb.net/?retryWrites=true&w=majority

**Atentie!**: parola este parola utilizatorului liviu al bazei de date, nu este parola de conectare la cloud.  Ia se seteaza din meniul Database Access, apoi pt. userul respectiv -> Edit __ Authenticatin Method ->Password

## Variabilele de environment in workflow

- Pot fi definite la nivel de step, job sau workflow prin atributul env
- Accesate in workflow fie direct (in bash ca $VAR) sau prin context object ${{ env.VAR }}

## Default environment variables

[See](https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables)

## Using Secrets

- Secrets pot fi stocate in Github la nivel de organizatie sau la nivel de repository

### Stocare la nivel de repository (Repository secrets)

In Github -> Repo -> Settings -> Secrets -> Actions -> New secret

![Secrets Menu](./doc/secrets.png)

- Secreturile se referentiaza in workflow folosing context objectul secrets

```yaml
jobs:
  test:
    env:
      MONGODB_CLUSTER_ADDRESS: cluster0.iivyk6h.mongodb.net
      MONGODB_USERNAME: ${{ secrets.MONGODB_USERNAME }}
      MONGODB_PASSWORD: ${{ secrets.MONGODB_PASSWORD }}

```

### Environments si environments secrets

Environments sunt disponibile doar in repo. publice sau in cele private platite.

- Un environment se ataseaza unor repositories.
- Dupa aceea joburile din aceste repo pot referentia environmentul.
- In environment pot fi stocate secrets, protection rules (e.g. only events related to certain branches can use an environment)

Ex:

- Putem crea un environment de test, unul de staging, altul de production.
- Fiecare environment poate avea propriile secrete
- Alte lucruri care se pot seta intr-un environment:
  - Required reviewers
  - Wait timer
  - Deployment branches (daca se doreste ca numai anumite branchuri sa declanseze joburile din environment)
  
```yaml
jobs:
  test:
    environment: testing
    env:
      MONGODB_CLUSTER_ADDRESS: cluster0.iivyk6h.mongodb.net
      MONGODB_USERNAME: ${{ secrets.MONGODB_USERNAME }}
      MONGODB_PASSWORD: ${{ secrets.MONGODB_PASSWORD }}
      PORT: 8080
    runs-on: ubuntu-latest
```
