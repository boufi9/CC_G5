# Étape 1: Utiliser une image de base Java
FROM openjdk:17-jdk

# Étape 2: Copier le fichier jar dans l'image
COPY target/Eurekaserver-0.0.1-SNAPSHOT.jar Eurekaserver-0.0.1-SNAPSHOT.jar

# Étape 3: Exécuter l'application
ENTRYPOINT ["java","-jar","/Eurekaserver-0.0.1-SNAPSHOT.jar"]
