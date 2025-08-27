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

