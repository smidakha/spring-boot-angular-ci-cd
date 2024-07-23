# Use an official openJDK runtime as a parent image
FROM openjdk:11-jdk-slim

# Set the working directory
 WORKDIR /app

# Copy the project jar file into the container at /app
Copy target/*.jar app.jar

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Run the jar file 
ENTRYPOINT ["java", "-jar", "app.jar"]


