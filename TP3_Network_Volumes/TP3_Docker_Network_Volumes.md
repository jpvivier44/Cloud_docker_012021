# TP Docker : Présentation des network et des volumes

**Exercice 1 : Service Web + présentation données de configuration
Le but de cet exercice est lancer un service nginx avec un réseau dédié et une configuration présentée
1. Préparer le fichier de configuration à présenter au conteneur nginx
2. Creer un network dédié à notre application de type bridge
3. Instancier un conteneur nommé web01 avec publication de port et avec bind du fichier de configuration index.html vers /usr/share/nginx/html/index.html
4. Vérifier la page WEB


#### Correction de l'exercice 1
1. Création d'un répertoire dédié au projet avec le fichier index.html
2. Création du network de type bridge
