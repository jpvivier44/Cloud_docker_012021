# Image de base
FROM centos:8

# Label
LABEL maintainer "Pierre"
LABEL description "Image de déploiement Tomcat + WAR intégré"

# Instruction RUN pour Install package yum indépendant de tomcat (optimisation du cache docker : une layer dédié qui sera réutilisable)
RUN yum install -y java-11-openjdk

# Instruction RUN pour installer le moteur tomcat
RUN mkdir /opt/tomcat \
    && curl -O https://downloads.apache.org/tomcat/tomcat-8/v8.5.61/bin/apache-tomcat-8.5.61.tar.gz \
    && tar -zxf apache-tomcat-8.5.61.tar.gz \
    && mv apache-tomcat-8.5.61/* /opt/tomcat/ \
    && rm -rf apache-tomcat-8.5.61*

# Instruction WORKDIR => le curseur se déplace vers la cible choisi
WORKDIR /opt/tomcat/webapps

# Instruction run pour télécharger le war
RUN curl -O -L https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/sample.war

# Instruction EXPOSE : ouvrir le port nécessaire à l'application
EXPOSE 8080

# Instruction ENTRYPOINT : commande qui fait référence au binaire,script à exécuté
ENTRYPOINT ["/opt/tomcat/bin/catalina.sh"]

# Instruction CMD : devient un argument de ENTRYPOINT 
CMD  ["run"]