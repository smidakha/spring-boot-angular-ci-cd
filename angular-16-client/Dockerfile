FROM node:14

#  Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

#Install dependencies
RUN npm install 

# Copy the rest of the app code
COPY . .

# Build the angular app in production mode
RUN npm run build --prod

# stage 2: Serve app with nginx

# Use an official nginx image as a parent image
FROM nginx:alpine

# Copy the built angular app from the previous stage 
COPY --from=0 /app/dist/* /usr/share/nginx/html

# Copy custom nginx configuration file
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]


