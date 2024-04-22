# CREER LE SERVEUR WEB DANS LE LANGUAGE DE PROGRAMMATION DE VOTRE CHOIX

Vous pouvez crée un repertoire back et un second pour le frontend si vous le souhaité
Evitez l'approche monolitic qui n'est pas adapter au cloud 

```yaml
python:
  - flask: https://flask.palletsprojects.com/en/3.0.x/ #tres simple a mettre en place
    exemple: |
      ```python
       # save this as app.py
        from flask import Flask

        app = Flask(__name__)

        @app.route("/")
        def hello():
            return "Hello, World!"
        ```
  - django: https://docs.djangoproject.com/en/5.0/
node:
  - nest.js: https://docs.nestjs.com/
    prof: https://github.com/Maissacrement/nestjs/tree/master

  - express: https://expressjs.com/fr/4x/api.html
    prof: https://github.com/Maissacrement/TwitterStream/tree/master
... # AUX CHOIX
```

# Tache
Il faut que vous coder un endpoint qui pour une requete de type get '/whoiam?user=${name}' retourne en code 200 'Bonjour ${name}'

# Contrainte
Vous devez containeriser votre application.

# EXECUTION

Un conteneur [Docker](https://docs.docker.com/engine/install/) est un environnement personnalisé conçu pour héberger votre application. Le Dockerfile est le fichier de spécification de ce conteneur, dont le but est de préparer l'environnement pour accueillir votre application dans un format prêt pour la production. Ce Dockerfile est constitué d'un ensemble de couches (layers) permettant d'atteindre cet objectif : fournir un environnement contenant toutes les dépendances nécessaires au bon fonctionnement de votre application dans son environnement final.

## Comment construire son Dockerfile

Voici quelque lien

```yaml
dockerfile:
  - https://blog.eleven-labs.com/fr/comprendre-et-personnaliser-son-environnement-docker#les-instructions-dockerfile
  - https://jfrog.com/fr/devops-tools/article/understanding-and-building-docker-images/#dockerfile-method
```

Instruction applicable par couche

<table border="1">
  <tr>
    <th>Commande</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>RUN</td>
    <td>Lancer des commandes shell</td>
  </tr>
  <tr>
    <td>FROM</td>
    <td>Déclarer une image source</td>
  </tr>
  <tr>
    <td>ARG</td>
    <td>Déclarer une variable utilisable uniquement durant le build docker</td>
  </tr>
  <tr>
    <td>ENV</td>
    <td>Déclarer une variable d’environnement utilisable durant le build et lors de l’utilisation du conteneur</td>
  </tr>
  <tr>
    <td>COPY</td>
    <td>Pour copier des fichiers et des répertoires de l’extérieur de l’image (ou d’une autre image) dans l’image en cours de création</td>
  </tr>
  <tr>
    <td>ADD</td>
    <td>Idem COPY mais avec la possibilité de télécharger des documents par URL</td>
  </tr>
  <tr>
    <td>CMD</td>
    <td>Définitions des options de la commandes principales du conteneurs (processus du conteneur)</td>
  </tr>
  <tr>
    <td>ENTRYPOINT</td>
    <td>Définition de la commande principale du conteneur issu de l’image</td>
  </tr>
  <tr>
    <td>WORKDIR</td>
    <td>Définit le répertoire de travail pour les instructions suivantes</td>
  </tr>
  <tr>
    <td>EXPOSE</td>
    <td>Déclare les ports sur lesquels le conteneur écoute les connexions</td>
  </tr>
  <tr>
    <td>VOLUME</td>
    <td>Déclare des points de montage dans le conteneur</td>
  </tr>
  <tr>
    <td>USER</td>
    <td>Définit l'utilisateur sous lequel les instructions suivantes sont exécutées</td>
  </tr>
</table>

## Comment construire son image docker

```bash
docker build . -t $(APP_NAME)
```

## Comment lancer son image docker
```bash
docker run -it --rm -p$(PORT_INNER_CONTAINER):$(PORT_OUTTER_CONTAINER) $(APP_NAME)
```

# PACKAGING

## Comment tagguer un containeur
```bash
docker tag $(DOCKER_REPO)/$(APP_NAME):$(VERSION) $(DOCKER_REPO)/$(APP_NAME):$(VERSION) # Tag current version
docker tag $(DOCKER_REPO)/$(APP_NAME):$(VERSION) $(DOCKER_REPO)/$(APP_NAME):latest # Tag latest
```

## Comment se connecter au registre de containeur de docker 

```bash
docker login
```

## Comment mettre en ligne son application

```bash
docker push $(DOCKER_REPO)/$(APP_NAME):$(VERSION)
docker push $(DOCKER_REPO)/$(APP_NAME):latest
```