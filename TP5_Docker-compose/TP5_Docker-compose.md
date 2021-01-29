# TP Docker : Présentation de docker-compose

**Exercice 1 : Répercuter toute l'infra appli nginx - php - mariadb**
Le but de cet exercice est lancer un service nginx php mariadb avec toutes les briques nécessaire au travers de docker-compose


#### Correction de l'exercice 1

1. Nettoyer l'existant

```docker container stop web01 php01 bdd01```

```docker container rm web01 php01 bdd01```

2. Répercution des commande d'origine du TP3 dans un docker-compose

