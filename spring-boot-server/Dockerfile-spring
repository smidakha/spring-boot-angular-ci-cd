# Use an official Maven image with JDK
FROM maven:3.8.5-openjdk-17

# Set the working directory
WORKDIR /app

# Copy the Maven project files into the container
COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src

# Expose port
EXPOSE 8081

# Run the Spring Boot application
ENTRYPOINT ["mvn", "spring-boot:run"]
