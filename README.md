# cloud_tutto


1) Installation de Docker sur une VM Amazon Linux 2 :
Créer une VM Amazon Linux 2 puis s’y connecter via SSH et lancer les
commandes suivantes :
Remarque : tapper ‘y’ en cas de :
Is this ok [y/d/N]: y
Les instructions d’installation:
## Update and enable Amazon Extras
sudo yum update -y
sudo amazon-linux-extras install epel -y
## Install needed app/libs for docker
sudo yum install docker
## add the ec2-user to docker
sudo usermod -a -G docker ec2-user
## create a docker group and join it
newgrp docker
## Start/Enable Docker
sudo systemctl enable docker
sudo systemctl start docker
## test that it works
docker-compose --version
Création d’une image Docker
1) Création d’une nouvelle image Docker sur votre machine:
Créer un répertoire de travail :
$ mkdir mydockerbuild
$ cd mydockerbuild/

Créer un fichier nommé Dockerfile
$ nano Dockerfile

Et mettre ces instructions :
FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortunes
CMD /usr/games/fortune -a | cowsay

Faire Ctrl X puis Y pour enregistrer

Pour créer l’image Docker :
$ docker build -t docker-whale .

Pour tester, lancer le conteneur correspondant :
$ docker run docker-whale

2) Création d’un compte (Docker ID) dans Docker Hub
Voir https://hub.docker.com/signup
3) Création d’une balise (tag) pour l’image créée :
Voir le ID de l’image docker-whale créé via « docker image ls »
Puis :
$ docker tag IMAGE_ID DOCKER_ID/docker-whale:latest
IMAGE_ID : l’ID de l’image que vous avez créée (montré par ‘docker image ls’)
DOCKER_ID : votre Docker ID du compte créé dans Docker Hub (le login)

Vérifier que votre image a pris un nouveau tag via :
$ docker image ls
4) Upload (ou publication) de l’image dans Docker Hub:
Accéder au site de Docker Hub (via votre compte) et créer un repository
publique « docker-whale »

Cliquer sur Create Repository (le répertoire d’une image Docker)

Se connecter à votre compte via la commande :
$ docker login
Publier l’image créé dans ce repository créé « docker-whale » avec le tag 1.0
$ docker push DOCKER_ID/docker-whale:1.0

puis vérifier dans votre compte de Hub Docker que l’image « docker-whale »
avec le tag « 1.0 » a été publié.
