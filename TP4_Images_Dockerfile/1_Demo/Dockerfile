# Instruction FROM : choix d'une image parente
FROM debian:buster-slim

# Instruction LABEL : ajout de metadata
LABEL maintainer "Pierre"
LABEL description "Demo dockerfile avec ajout de script"

# Instruction COPY : ajout d'un fichier dans l'image de base
COPY script.sh /

# Instruction RUN : lancement de commandes Linux pour modifier les droits sur mon fichier
RUN chmod 700 /script.sh

# Instruction CMD : commande à exécuter lors de l'instancitation d'un conteneur
CMD ["./script.sh"]