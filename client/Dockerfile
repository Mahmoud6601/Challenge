# Step 1: Use Node.js version 18 as the base image for the container
FROM node:18

# Step 2: Set the working directory inside the container to store app files
WORKDIR /usr/src/app

# Step 3: Copy the package.json and package-lock.json files for installing dependencies
COPY package*.json ./

# Step 4: Install project dependencies using npm
RUN npm install

# Step 5: Copy the rest of the project files from the host to the working directory in the container
COPY . .

# Step 6: Build the project for production (this compiles the Nuxt.js application)
RUN npm run build

# Step 7: Expose port 3000, the default port for the Nuxt.js app
EXPOSE 3000

# Step 8: Start the Nuxt.js application using npm's serve script from package.json
CMD ["npm", "run", "serve"]
