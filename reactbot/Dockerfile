# Step 1: Build the React app using Node.js
FROM node:16 as build

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json (or yarn.lock)
COPY package*.json ./  # Adjusted this line to reference files in the context

# Install dependencies
RUN npm install

# Copy the entire React app into the container
COPY . .  # Adjusted this line to copy all files from the current context (Reactbot/)

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
