# Use an official Node.js runtime as the base image
FROM node:20 AS build

WORKDIR /app

# Copy package files and install dependencies
COPY package.json yarn.lock ./
RUN yarn install --immutable

# Copy the rest of the app's source code
COPY . .

# Build the React app
RUN yarn build

# Use an Nginx image to serve the app
FROM nginx:alpine

# Copy build output to Nginx's default directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
