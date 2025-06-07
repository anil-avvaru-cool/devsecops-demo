## CVE Common Vulnerabilities and Exposures 

## Scan for sensitive info like API keys and credentials

## Pull all sensitive info from vault

## Scan vulnerabilities packages

## Vite
Build and run locally

## npm run build
It looks for command from package.json
example: vite build npm 

## Best practice: Multi stage Docker image
Advantage of multistage: to reduce the size

1. Download dependencies
2. Build
3. Copy binaries (Dist) to web server (Nginx)

Docker example:
# Build stage
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
# Add nginx configuration if needed
# COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

## Docker commands
docker build -t tiktaktoe-demo:v1 .
docker run -d -p 9099:80 tiktaktoe-demo:v1

## CI/CD Github yml
````yml
on:
  push:
    branches: [ main ]
    paths-ignore:
      - 'kubernetes/deployment.yaml'  # Ignore changes to this file to prevent loops
  pull_request:
    branches: [ main ]

jobs:
  test:
    name: Unit Testing
  static:
  
  build:

  
````



