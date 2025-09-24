    🐋 Introduction à Docker - Jour 1

Ce projet documente ma première journée d'apprentissage avec Docker, incluant les concepts fondamentaux et des exemples pratiques.
📋 Prérequis

    Docker Desktop installé

    Terminal/CLI de base

    Connaissances basiques en ligne de commande

🚀 Concepts Appris le Jour 1

Vérifier l'installation de Docker
docker --version
docker info

Lancer un container Nginx
docker run -d -p 8080:80 --name mon-premier-nginx nginx

Voir les containers en cours d'exécution
docker ps

Arrêter le container
docker stop mon-premier-nginx

Redémarrer le container
docker start mon-premier-nginx

🎯 Exemple Pratique
Lancer un serveur web simple

Créer et lancer un container Apache
docker run -d -p 8081:80 --name mon-apache httpd

Accéder au serveur : http://localhost:8081

🐋 Introduction à Docker - Jour 2

Ce projet documente ma deuxième journée d'apprentissage avec Docker, couvrant des concepts plus avancés et des cas d'utilisation pratiques.

📋 Rappel du Jour 1

- Vérification de l'installation de Docker
- Lancement de containers Nginx et Apache
- Gestion basique des containers (démarrer, arrêter)

🚀 Concepts Appris le Jour 2

Gestion des images Docker

```
bash
Lister les images téléchargées
docker images

Rechercher une image sur Docker Hub
docker search redis

Télécharger une image sans l'exécuter
docker pull mysql:8.0

Supprimer une image
docker rmi nom-image
```

Inspection des containers

```bash
Voir les logs d'un container
docker logs mon-premier-nginx

Voir les processus en cours dans un container
docker top mon-premier-nginx

Inspecter les détails d'un container
docker inspect mon-premier-nginx

Voir les statistiques d'utilisation des resources
docker stats
```

Containers interactifs

```bash
 Lancer un container Ubuntu en mode interactif
docker run -it --name mon-ubuntu ubuntu /bin/bash

 Exécuter une commande dans un container en cours d'exécution
docker exec -it mon-premier-nginx /bin/bash

 Créer un conteneur MySQL avec variables d'environnement
docker run -d --name mysql-container -e MYSQL_ROOT_PASSWORD=mon_mot_de_passe -p 3306:3306 mysql:8.0
```

Gestion avancée des containers

    bash
    Renommer un container
    docker rename mon-premier-nginx nginx-server

    Créer une image à partir d'un container modifié
    docker commit nginx-server nginx-personnalise

    Supprimer un container arrêté
    docker rm nginx-server

    Supprimer tous les containers arrêtés
    docker container prune
```

🎯 Exemple Pratique: Application Multi-Conteneurs

Création d'une application web simple avec un serveur Nginx et une base de données Redis:

```
bash
Lancer le container Redis
docker run -d --name redis-server redis

Lancer un container Nginx qui se connecte à Redis
docker run -d --name web-app --link redis-server:redis -p 8080:80 nginx
```

📦 Gestion des volumes

```bash
Créer un volume
docker volume create mon-volume

Lister les volumes
docker volume ls

Lancer un container avec un volume
docker run -d --name nginx-with-volume -v mon-volume:/usr/share/nginx/html -p 8082:80 nginx

Inspecter un volume
docker volume inspect mon-volume
```

🔄 Redémarrage automatique des containers

```
bash
Configurer un container pour qu'il redémarre toujours
docker run -d --name nginx-always --restart always -p 8083:80 nginx

Configurer un container pour qu'il redémarre seulement en cas d'échec
docker run -d --name nginx-on-failure --restart on-failure:5 -p 8084:80 nginx

Voici la **suite pour le Jour 3** de ton apprentissage Docker, dans la continuité de ce que tu as déjà documenté :

---

# 🐋 Introduction à Docker - Jour 3

Ce projet documente ma troisième journée d'apprentissage avec Docker, en approfondissant les concepts liés aux **Dockerfiles**, **réseaux Docker** et à la création d’images personnalisées.

---

## 📋 Rappel du Jour 2

* Gestion des images Docker (pull, rmi, search)
* Inspection et logs des containers
* Containers interactifs (Ubuntu, MySQL)
* Gestion avancée (rename, commit, prune)
* Application multi-conteneurs (Nginx + Redis)
* Volumes Docker
* Redémarrage automatique des containers

---

## 🚀 Concepts Appris le Jour 3

### 1️⃣ Création d’images personnalisées avec **Dockerfile**

Un `Dockerfile` permet de définir une image sur mesure.

```dockerfile
# Exemple : Créer une image Nginx personnalisée
FROM nginx:latest
COPY ./site-html /usr/share/nginx/html
EXPOSE 80
```

Construire et exécuter l’image :

```bash
# Construire l’image
docker build -t mon-nginx-personnalise .

# Lancer un container basé sur cette image
docker run -d -p 8085:80 --name nginx-custom mon-nginx-personnalise
```

---

### 2️⃣ Réseaux Docker

Docker propose différents types de réseaux pour connecter les containers.

```bash
# Lister les réseaux existants
docker network ls

# Créer un réseau bridge personnalisé
docker network create mon-reseau

# Lancer deux containers sur le même réseau
docker run -d --name redis-db --network mon-reseau redis
docker run -d --name app-web --network mon-reseau nginx
```

Tester la connectivité :

```bash
docker exec -it app-web ping redis-db
```

---

### 3️⃣ Variables d’environnement et fichiers `.env`

Définir des variables d’environnement dans un container :

```bash
docker run -d --name app-env -e APP_ENV=production -e APP_DEBUG=false nginx
```

Avec un fichier `.env` :

`.env` :

```
MYSQL_ROOT_PASSWORD=supersecret
MYSQL_DATABASE=appdb
```

Commande :

```bash
docker run -d --name mysql-env --env-file .env mysql:8.0
```

---

### 4️⃣ Partage de fichiers avec **bind mounts**

Contrairement aux volumes, les *bind mounts* permettent de partager un dossier local avec un container.

```bash
docker run -d --name nginx-bind \
  -v $(pwd)/site-html:/usr/share/nginx/html \
  -p 8086:80 nginx
```

---

## 🎯 Exemple Pratique : Application Web + DB avec réseau et Dockerfile

1. Créer un réseau dédié :

```bash
docker network create app-network
```

2. Lancer une base MySQL :

```bash
docker run -d --name db-app \
  --network app-network \
  -e MYSQL_ROOT_PASSWORD=monpass \
  -e MYSQL_DATABASE=appdb \
  mysql:8.0
```

3. Créer un `Dockerfile` pour une app PHP simple connectée à MySQL :

```dockerfile
FROM php:7.4-apache
RUN docker-php-ext-install mysqli
COPY ./src /var/www/html
EXPOSE 80
```

4. Construire et exécuter :

```bash
docker build -t php-app .
docker run -d --name web-app --network app-network -p 8087:80 php-app
```

L’application pourra se connecter à la base MySQL via `db-app`.
Parfait 👍 On a déjà bien couvert les **Jours 1, 2 et 3**. Voici une version condensée et claire pour la **suite (Jour 4)**, avec de nouvelles notions utiles, tout en gardant le style homogène et allégé :

---

# Docker - Jour 4

Ce projet documente ma quatrième journée d’apprentissage avec Docker, avec un focus sur **Docker Compose**, la gestion des logs et l’optimisation des images.

---

## 📋 Rappel du Jour 3

* Création d’images personnalisées via Dockerfile
* Réseaux Docker (bridge personnalisé, ping entre containers)
* Variables d’environnement et `.env`
* Bind mounts pour partager des fichiers locaux
* Exemple pratique : app web + base de données MySQL

---

## 🚀 Concepts Appris le Jour 4

### 1️⃣ Docker Compose (multi-conteneurs simplifié)

Un fichier `docker-compose.yml` permet de lancer plusieurs services ensemble.

```yaml
version: "3.8"
services:
  web:
    build: .
    ports:
      - "8088:80"
    depends_on:
      - db
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: appdb
```

Démarrer les services :

```bash
docker-compose up -d
```

Arrêter :

```bash
docker-compose down
```

---

### 2️⃣ Gestion des logs centralisée

```bash
# Voir les logs d’un service avec Docker Compose
docker-compose logs web

# Suivre les logs en temps réel
docker logs -f web
```

---

### 3️⃣ Optimisation d’images Docker

Réduire la taille des images avec une approche **multi-stage build** :

```dockerfile
# Étape de build
FROM node:16 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Étape de prod légère
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
```

---

### 4️⃣ Nettoyage et maintenance

```bash
# Supprimer containers, images, volumes inutilisés
docker system prune -a

# Vérifier l’espace disque utilisé
docker system df
```

---

## 🎯 Exemple Pratique : Stack Web avec Compose

1. Créer un projet avec :

   * un container Nginx pour le front
   * un container MySQL pour la base

2. Fichier `docker-compose.yml` minimal :

```yaml
version: "3.8"
services:
  frontend:
    image: nginx
    ports:
      - "8090:80"
  database:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: admin
      MYSQL_DATABASE: myapp
```

3. Lancer l’ensemble :

```bash
docker-compose up -d
```


