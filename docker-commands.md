# Docker Frontend Applications - Command Reference Guide

## Project Overview
This document contains all the Docker commands used in this frontend applications project, which includes a React application, Vue.js application, and a static HTML/CSS/JS application.

## Building the Images

### React Application
```bash
# Navigate to React app directory
cd react-app

# Build the React Docker image
docker build -t react-docker-app .
```

### Vue.js Application
```bash
# Navigate to Vue.js app directory
cd vue-app

# Build the Vue.js Docker image
docker build -t vue-docker-app .
```

### Static Application
```bash
# Navigate to static app directory
cd static-app

# Build the static Docker image
docker build -t static-docker-app .
```

## Running the Containers

### React Application
```bash
# Run React application on port 3000
docker run -p 3000:80 react-docker-app
```

### Vue.js Application
```bash
# Run Vue.js application on port 8081
docker run -p 8081:80 vue-docker-app
```

### Static Application
```bash
# Run static application on port 9000
docker run -p 9000:80 static-docker-app
```

## Useful Docker Commands

### Container Management
```bash
# List all running containers
docker ps

# List all containers (including stopped ones)
docker ps -a

# Stop a specific container
docker stop [CONTAINER_ID]

# Stop all running containers
docker stop $(docker ps -q)

# Remove a container
docker rm [CONTAINER_ID]
```

### Image Management
```bash
# List all images
docker images

# Remove an image
docker rmi [IMAGE_NAME]

# Remove all unused images
docker image prune
```

## Dockerfile Examples

### React Application Dockerfile
```dockerfile
# Build stage
FROM node:16-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . ./
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Vue.js Application Dockerfile
```dockerfile
# Build stage
FROM node:16-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . ./
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### Static Application Dockerfile
```dockerfile
# Use nginx as the base image
FROM nginx:alpine

# Copy static files to nginx html directory
COPY . /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
```

## Accessing the Applications

After running the containers, you can access the applications at:
- React Application: http://localhost:3000
- Vue.js Application: http://localhost:8081
- Static Application: http://localhost:9000

## Docker Network and Port Mapping
- The `-p` flag maps container ports to host ports
- Format: `-p [HOST_PORT]:[CONTAINER_PORT]`
- Example: `-p 3000:80` maps container's port 80 to host's port 3000

## Best Practices
1. Always use specific versions for base images
2. Implement multi-stage builds for smaller production images
3. Use .dockerignore to exclude unnecessary files
4. Expose only required ports
5. Use proper caching mechanisms in Dockerfile