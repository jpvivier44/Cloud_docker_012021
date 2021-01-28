# TP Docker : La fonction commit

**Exercice 1 : shell intéractif**
Le but de cet exercice est lancer des containers en mode intéractif
1. Lancez un container basé sur alpine en mode interactif en le nommant sans lui spécifier de commande
2. Que s’est-il passé ?
3. Quelle est la commande par défaut d’un container basé sur alpine ?
4. Naviguez dans le système de fichiers
5. Utilisez le gestionnaire de package d’alpine (apk) pour ajouter un package
```
$ apk update
$ apk add curl
$ apk add iputils
```

#### Correction de l'exercice 1
1. La commande permettant de lancer un container en mode "interactif" est la suivante:
```docker container run --name alpine_curl -ti alpine```
2. Nous obtenons un shell sh dans le container.
3. Par défaut, la commande par défaut utilisée dans l'image alpine est /bin/sh
Note: nous y reviendrons plus tard mais il est intéressant de voir que cette information est
présente dans le fichier Dockerfile qui est utilisé pour créer l'image
(https://github.com/gliderlabs/docker-
alpine/blob/2127169e2d9dcbb7ae8c7eca599affd2d61b49a7/versions/library-
3.6/x86_64/Dockerfile)
4. Nous pouvons naviguer dans le système de fichiers de la même façon que nous le faisonsdans une autre distribution Linux plus "traditionnelle" en utilisant les commandes cd, ls,
pwd, cat, less, ...
5. Le gestionnaire de package d'une distribution alpine est apk
Pour mettre à jour la liste des packages, nous pouvons utiliser la commande apk update .
Pour installer un package, comme curl , nous utilisons la commande suivante apk add curl

**Exercice 2 : COMMIT : prise en compte des modifications apportées dans le conteneur (Layer R/W) dans une nouvelle image**
Le but de cet exercice est de créer une nouvelle image alpine avec prise en compte des modifs précédentes
Nous pourrons ensuite l'utiliser avec des nouveaux conteneurs qui de fait possederont le package voulu
1. Sortie du conteneur précédent
2. Utiliser la commande "diff" pour visualiser les données différentes (ajout, modif, suppression) par rapport à l'image de référence
3. Lancer la commande pour faire un commit à partir de ce conteneur en spécifiant un nouveau nom d'image + Tag
4. Vérifier en listant les images
5. Vérifier le comportement en instanciant un nouveau conteneur à partir de cette nouvelle image

#### Correction de l'exercice 2
1. Sortir du conteneur : celui-ci sera stoppé mais pas supprimé donc pas encore du suppression des données dans la docker area

```$ exit```

2. Commande diff

```$ docker container diff alpine_curl```

3. Commande commit 

```$ docker container commit -a "Pierre" -m "Ajout package curl" alpine_curl alpine_curl:1.0```

4. Lister les images :

```$ docker image ls```

5. Instancier un nouveau conteneur depuis la nouvelle image

```$ docker container run -it --name new_alpine_curl alpine_curl:1.0```
