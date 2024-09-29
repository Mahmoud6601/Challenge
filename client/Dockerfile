# Step 1: Use Node.js as the base image
FROM node:18

# Step 2: Set the working directory inside the container
WORKDIR /usr/src/app

# Step 3: Copy the package.json and package-lock.json files
COPY package*.json ./

# Step 4: Install project dependencies
RUN npm install

# Step 5: Copy the rest of the application files
COPY . .

# Step 6: Build the project for production
RUN npm run build

# Step 7: Expose port 3000 for the Nuxt.js app
EXPOSE 3000

# Step 8: Start the Nuxt.js application
CMD ["npm", "run", "serve"] 
