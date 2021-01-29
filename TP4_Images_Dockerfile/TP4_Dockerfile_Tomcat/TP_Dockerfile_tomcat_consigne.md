# TP Dockerfile TOMCAT

**Exercice 1 : Sample tomcat war**
Le but de ce TP est de construire un Dockerfile qui permettra de generer une image docker tomcat avec une application war intégrée
1. Creer un répertoire de projet TP4_Dockerfile_Tomcat
2. Dans ce répertoire projet (microservice) créer un fichier Dockerfile
3. Voici le schéma directeur à suivre :
    * Partir d'une image de base : centos:8
    * Préciser des labels (idéal pour donner des informations lors d'un docker image inspect)
    * Installer le package java (via yum)
    
        ```yum install -y java-11-openjdk```

    * Créer un répertoire /opt/tomcat
  
        ```mkdir```

    * Récupérer un fichier distant : https://downloads.apache.org/tomcat/tomcat-8/v8.5.61/bin/apache-tomcat-8.5.61.tar.gz
  
        ```curl -O https://downloads.apache.org/tomcat/tomcat-8/v8.5.61/bin/apache-tomcat-8.5.61.tar.gz```

    * Décompresser l'archive puis déplacer tous le contenu de apache-tomcat-8.5.61 dans /opt/tomcat/
  
        ```tar -zxf apache-tomcat-8.5.61.tar.gz```

           ```mv apache-tomcat-8.5.61/* /opt/tomcat/```
    
    * Utiliser la directive **WORKDIR** pour se positionner dans le répertoire "/opt/tomcat/webapps"
    * Récuperer le fichier distant https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/sample.war
  
        ```curl -O -L```

    * Exposer (rendre visible) le port par défaut tomcat 8080
    * Préciser la commande finale à exécuter : ENTRYPOINT ["/opt/tomcat/bin/catalina.sh"]
    * Préciser l'argument à donner par défaut derrière la commande ENTRYPOINT : CMD ["run"]

----
> Idéalement : Essayer de minimiser le nombre de Layers !!

----

1. Construire une image nommée  tomcat:8.5.61 à partir de ce Dockerfile
2. Démarrer un nouveau conteneur à partir de cette image :
    * Il faut publier un port !!! (pour acceder au conteneur depuis le docker hôte)
    * Il faudra sans doute le démarrer en mode "détaché"
    * Idéalement on lui donne un nom pour le manager plus facilement
3. Tester l'accès depuis un navigateur sur le docker hôte
> http://{ip_docker_hote}:8080/sample
