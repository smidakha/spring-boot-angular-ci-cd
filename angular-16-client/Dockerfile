# Use the official Node.js 18 image as the base image
FROM node:18

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json (if available) to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Expose port 8081
EXPOSE 8082

# Command to run the Angular application
CMD ["ng", "serve", "--host", "0.0.0.0", "--port", "8082"]



