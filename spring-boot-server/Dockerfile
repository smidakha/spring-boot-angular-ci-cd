# Utilisez une image de base officielle d'OpenJDK 17
FROM openjdk:17-jdk-slim

# Définir l'emplacement de travail
WORKDIR /app

# Copy the project jar file into the container at /app
#Copy target/*.jar app.jar

# Téléchargez Maven
ENV MAVEN_VERSION=3.8.6
RUN apt-get update && \
    apt-get install -y wget && \
    wget https://dlcdn.apache.org/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    tar -xzf apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /opt && \
    ln -s /opt/apache-maven-${MAVEN_VERSION} /opt/maven && \
    rm apache-maven-${MAVEN_VERSION}-bin.tar.gz

# Définir les variables d'environnement pour Maven
ENV MAVEN_HOME /opt/maven
ENV PATH $MAVEN_HOME/bin:$PATH


# Copier le projet dans le conteneur
 COPY . /app
 
 # Définir la commande par défaut (si vous avez un point d'entrée)
  CMD ["mvn", "spring-boot" ":run"]

# Make port 8080 available to the world outside this container
EXPOSE 8081

 