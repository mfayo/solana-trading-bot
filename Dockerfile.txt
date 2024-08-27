# Use node.js as base image
FROM node:14.17.0

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Update npm to the latest version
RUN npm install -g npm@latest

# Install the dependencies
RUN npm ci

# Copy the source code to the working directory (except the files in .dockerignore)
COPY . .

# Copy the .env.copy file to .env
RUN cp .env.copy .env

# Expose the port
EXPOSE 3000

# Start the application
CMD ["npm", "run", "buy"]