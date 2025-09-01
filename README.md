🐋 Introduction à Docker - Jour 1

Ce projet documente ma première journée d'apprentissage avec Docker, incluant les concepts fondamentaux et des exemples pratiques.
📋 Prérequis

    Docker Desktop installé

    Terminal/CLI de base

    Connaissances basiques en ligne de commande

🚀 Concepts Appris le Jour 1

# Vérifier l'installation de Docker
docker --version
docker info

# Lancer un container Nginx
docker run -d -p 8080:80 --name mon-premier-nginx nginx

# Voir les containers en cours d'exécution
docker ps

# Arrêter le container
docker stop mon-premier-nginx

# Redémarrer le container
docker start mon-premier-nginx

🎯 Exemple Pratique
Lancer un serveur web simple

# Créer et lancer un container Apache
docker run -d -p 8081:80 --name mon-apache httpd

# Accéder au serveur : http://localhost:8081

🐋 Introduction à Docker - Jour 2

Ce projet documente ma deuxième journée d'apprentissage avec Docker, couvrant des concepts plus avancés et des cas d'utilisation pratiques.
📋 Rappel du Jour 1

    Vérification de l'installation de Docker

    Lancement de containers Nginx et Apache

    Gestion basique des containers (démarrer, arrêter)

🚀 Concepts Appris le Jour 2
Gestion des images Docker
bash

# Lister les images téléchargées
docker images

# Rechercher une image sur Docker Hub
docker search redis

# Télécharger une image sans l'exécuter
docker pull mysql:8.0

# Supprimer une image
docker rmi nom-image

Inspection des containers
bash

# Voir les logs d'un container
docker logs mon-premier-nginx

# Voir les processus en cours dans un container
docker top mon-premier-nginx

# Inspecter les détails d'un container
docker inspect mon-premier-nginx

# Voir les statistiques d'utilisation des resources
docker stats

Containers interactifs
bash

# Lancer un container Ubuntu en mode interactif
docker run -it --name mon-ubuntu ubuntu /bin/bash

# Exécuter une commande dans un container en cours d'exécution
docker exec -it mon-premier-nginx /bin/bash

# Créer un conteneur MySQL avec variables d'environnement
docker run -d --name mysql-container -e MYSQL_ROOT_PASSWORD=mon_mot_de_passe -p 3306:3306 mysql:8.0

Gestion avancée des containers
bash

# Renommer un container
docker rename mon-premier-nginx nginx-server

# Créer une image à partir d'un container modifié
docker commit nginx-server nginx-personnalise

# Supprimer un container arrêté
docker rm nginx-server

# Supprimer tous les containers arrêtés
docker container prune

🎯 Exemple Pratique: Application Multi-Conteneurs

Création d'une application web simple avec un serveur Nginx et une base de données Redis:
bash

# Lancer le container Redis
docker run -d --name redis-server redis

# Lancer un container Nginx qui se connecte à Redis
docker run -d --name web-app --link redis-server:redis -p 8080:80 nginx

📦 Gestion des volumes
bash

# Créer un volume
docker volume create mon-volume

# Lister les volumes
docker volume ls

# Lancer un container avec un volume
docker run -d --name nginx-with-volume -v mon-volume:/usr/share/nginx/html -p 8082:80 nginx

# Inspecter un volume
docker volume inspect mon-volume

🔄 Redémarrage automatique des containers
bash

# Configurer un container pour qu'il redémarre toujours
docker run -d --name nginx-always --restart always -p 8083:80 nginx

# Configurer un container pour qu'il redémarre seulement en cas d'échec
docker run -d --name nginx-on-failure --restart on-failure:5 -p 8084:80 nginx

