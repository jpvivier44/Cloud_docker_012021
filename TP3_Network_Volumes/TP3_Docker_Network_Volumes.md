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
=> Bind des fichier de conf :
        => nginx : /etc/nginx/conf.d/nginx.conf
                   /usr/share/nginx/html/index.html
        => php : /srv/http/index.php