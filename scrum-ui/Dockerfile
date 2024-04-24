### STAGE 1: Build ###
# Use a more current version of node if possible
FROM node:12.7-alpine AS build
WORKDIR /usr/src/app

# Install dependencies separately to leverage Docker cache
COPY package*.json ./
RUN npm install

# Copy the rest of your app's source code
COPY . .
RUN npm run build

### STAGE 2: Run ###
# Use a more current version of Nginx if compatible
FROM nginx:1.17.1-alpine

# Copy the Nginx configuration file
COPY default.conf /etc/nginx/conf.d/

# Copy static assets from builder stage
COPY --from=build /usr/src/app/dist/scrum-ui /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Nginx runs by default, no need to add CMD unless you need a custom command
