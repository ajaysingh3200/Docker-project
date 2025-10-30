# Docker Frontend Applications Practice

This repository contains three different frontend applications perfect for practicing Docker containerization:

1. **React TypeScript Application** (`/react-app`)
   - Modern React application with TypeScript
   - Multi-stage Docker build
   - Production-ready Nginx configuration

2. **Vue.js Application** (`/vue-app`)
   - Vue 3 application
   - Multi-stage Docker build
   - Production-ready configuration

3. **Static HTML/CSS/JS Application** (`/static-app`)
   - Simple static website
   - Single-stage Docker build
   - Lightweight Nginx server

## Building and Running the Applications

### React Application
```bash
cd react-app
docker build -t react-docker-app .
docker run -p 3000:80 react-docker-app
```

### Vue Application
```bash
cd vue-app
docker build -t vue-docker-app .
docker run -p 8080:80 vue-docker-app
```

### Static Application
```bash
cd static-app
docker build -t static-docker-app .
docker run -p 9000:80 static-docker-app
```

## Learning Points

1. **Multi-stage Builds**: React and Vue applications demonstrate multi-stage builds to create smaller production images.
2. **Nginx Configuration**: All applications use Nginx for serving static content in production.
3. **Different Build Processes**: Each application has different build requirements and configurations.
4. **Port Mapping**: Practice with different port mappings for each application.

## Getting Started

1. Install Docker on your machine
2. Clone this repository
3. Navigate to any of the application directories
4. Follow the build and run instructions above

Each application has its own Dockerfile with detailed comments explaining the build process.