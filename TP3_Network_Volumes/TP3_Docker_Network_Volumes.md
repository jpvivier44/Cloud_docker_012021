# TP Docker : Présentation des network et des volumes

**Exercice 1 : Service Web + présentation données de configuration**
Le but de cet exercice est lancer un service nginx avec un réseau dédié et une configuration présentée
1. Préparer le fichier de configuration à présenter au conteneur nginx
2. Creer un network dédié à notre application de type bridge nommé tp3_network
    ==> Action est à faire sur l'objet network du docker engine
    ==> $ docker network ????
3. Instancier un conteneur nommé web01 dans le network précedemment créé, avec publication de port et avec bind du fichier de configuration index.html vers /usr/share/nginx/html/index.html
    ==> Publication : option -p
    ==> Bind de volume : option ????
    ==> Ajout dans le bon network : option ????
4. Vérifier la page WEB


#### Correction de l'exercice 1
1. Création d'un répertoire dédié au projet avec le fichier index.html
2. Création du network de type bridge

```$ docker network create tp3_network```

```$ docker network ls```

```$ docker network inspect tp3_network```

3. Instancier un conteneur nommé web01 dans le network précedemment créé, avec publication de port et avec bind du fichier de configuration index.html vers /usr/share/nginx/html/index.html en mode détaché

```$ docker container run -d --name web01 --network tp3_network -p 8080:80 -v /home/pierre/formation_docker/TP3_Network_Volumes/conf/index.html:/usr/share/nginx/html/index.html nginx```


**Exercice 2 : Service Web + PHP**
Le but de cet exercice est lancer un service nginx avec un réseau dédié et une configuration présentée
ainsi qu'un service php dans le même réseau dédié avec présentation de fichier code php
Nous verrons ainsi que le réseau dédié met en place un mécanisme de DNS intégré : les conteneur peuvent se joindre par leur nom de conteneur sur leur réseau

1. Télécharger l'image php : phpdockerio/php73-fpm
2. Détruire le conteneur de l'exercice 1
3. Préparer les fichiers de configuration (nginx.conf et index.php) sur le docker host
4. Instancier les deux conteneur avec les options nécessaires
==> web01
==> php01
==> Bind des fichier de conf :
        => nginx : /etc/nginx/conf.d/nginx.conf
                   /usr/share/nginx/html/index.html
        => php : /srv/http/index.php


#### Correction de l'exercice 2

1. Pull de l'image :

```$ docker pull phpdockerio/php73-fpm```

2. Clean

```$ docker container rm -f web01```

3. Preparation des fichiers

4. Instancier :

    - 4.1 : Conteneur php
    
        ```$ docker container run -d --name php01 --network tp3_network -v /home/pierre/formation_docker/TP3_Network_Volumes/conf/index.php:/srv/http/index.php phpdockerio/php73-fpm```

    - 4.2 : Conteneur nginx

        ```$ docker container run -d --name web01 --network tp3_network -v /home/pierre/formation_docker/TP3_Network_Volumes/conf/nginx.conf:/etc/nginx/conf.d/nginx.conf -v /home/pierre/formation_docker/TP3_Network_Volumes/conf/index.html:/usr/share/nginx/html/index.html -p 8080:80 nginx```


**Exercice 3 : Découverte d'une image mariadb**
1. Télécharger l'image mariadb
2. Instancier un conteneur à partir de cette image
3. Utiliser exec pour se connecter au serveur : commande "mysql -u root -p"
4. Creer une nouvelle database
5. Quitter et détruire le conteneur
6. Utilisation d'un volume au sens objet docker (docker volume ls)
7. Instanciation d'un conteneur en utilisant le volume créé précédemment
8. On peut refaire l'exercice de création de database, puis supprimer le conteneur puis le recréer en prenant soint de spécifier le volume d'origine

#### Correction de l'exercice 3
1. Télécharger l'image mariadb

```$ docker image pull mariadb```

2. Instanciation

```$ docker run --name test-mariadb -e MYSQL_ROOT_PASSWORD=roottoor -d mariadb```

3. Commande exec :

```$  docker container exec -it test-mariadb mysql -u root -proottoor```

4. Creation database

```CREATE DATABASE formation;```

```show databases;```

5. Sortie + rm

```$ docker container rm -f test-mariadb```

6. Creation volume

```$ docker volume create tp3_volume```

7. Instanciation

```$ docker run -v tp3_volume:/var/lib/mysql --name test-mariadb-vol -e MYSQL_ROOT_PASSWORD=roottoor -d mariadb```

8. On peut refaire l'exercice de création de database, puis supprimer le conteneur puis le recréer en prenant soint de spécifier le volume d'origine

```$ docker container rm -f test-mariadb-vol```

```$ docker run -v tp3_volume:/var/lib/mysql --name test-mariadb-vol -e MYSQL_ROOT_PASSWORD=roottoor -d mariadb```


**Exercice 4 : Instanciation d'un conteneur maraidb dans le projet tp3**
1. Nettoyage complet des conteneur du projet : suppression container, volumes
2. Préparer le fichier d'initialisation de base : init.sql
3. Création d'un volume docker pour héberger la nouvelle base
==> tp3_vol_bdd
4. Instancier correctement le conteneur :
    ==> name : bdd01
    ==> network: tp3_network
    ==> variable d'environnement : MYSQL_ROOT_PASSWORD
    ==> bind du fichier sql: /chemin_complet/init.sql vers /docker-entrypoint-initdb.d
    ==> monter le volume tp3_vol_bdd vers /var/lib/mysql/
    ==> image de référence : mariadb:10.5
5. Modifier le fichier index.php pour qu'il tente de se connecter à la bdd
6. Recreer le conteneur php01 puis le conteneur web01
7. Tester le site web 
    ==> Il va y avoir un pb avec l'image php (manque package php7.3-mysql)

==> Aborder les Dockerfile

