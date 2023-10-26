FROM node:14 as build
WORKDIR /app

# Install Angular CLI
RUN npm install -g @angular/cli

# Copy package.json and package-lock.json
COPY package*.json ./

# Install app dependencies
RUN npm install

# Copy the rest of the app source code
COPY . .

# Build the Angular app for production
RUN ng build --prod

# Use a lightweight Nginx image to serve the built app
FROM nginx:alpine

# Copy the built app to the Nginx web server directory
COPY --from=build /app/dist/* /usr/share/nginx/html/

EXPOSE 80
#EXPOSE 4200

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
