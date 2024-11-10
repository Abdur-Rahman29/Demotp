# Step 1: Build the React app using Node.js
FROM node:16 as build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json (or yarn.lock)
COPY reactbot/package*.json ./

# Install dependencies
RUN npm install

# Copy the entire React app into the container
COPY reactbot/ .

# Build the React app for production
RUN npm run build

# Step 2: Serve the React app using Nginx
FROM nginx:alpine

# Copy the build output from the previous step into the Nginx HTML directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 for the React frontend
EXPOSE 80

# Run Nginx (default command for the Nginx image)
CMD ["nginx", "-g", "daemon off;"]
