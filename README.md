# BookAPI

## Overview

This project is a web application consisting of a PHP Laravel API and a Nuxt.js Client. The application is containerized using Docker and orchestrated with Docker Compose. It includes an Nginx web server that acts as a reverse proxy, connecting the Client and API, and uses a self-signed SSL certificate for secure communication.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Structure](#project-structure)
3. [Step 1: Create Dockerfile for API](#step-1-create-dockerfile-for-api)
4. [Step 2: Create Dockerfile for Client](#step-2-create-dockerfile-for-client)
5. [Step 3: Create Docker Compose File](#step-3-create-docker-compose-file)
6. [Step 4: Nginx Configuration](#step-4-nginx-configuration)
7. [Step 5: Create Self-Signed SSL Certificate](#step-5-create-self-signed-ssl-certificate)
8. [Step 6: Implement CI/CD Pipeline](#step-6-implement-cicd-pipeline)
9. [Step 7: Run the Application](#step-7-run-the-application)
10. [Warnings and Troubleshooting](#warnings-and-troubleshooting)
11. [Screenshots](#screenshots)

## Prerequisites

- Docker and Docker Compose installed on your machine.
- Git installed for version control.
- Basic knowledge of PHP, JavaScript, and Docker.

## Project Structure

```
.
├── api
│   ├── Dockerfile
│   └── ... (other API files)
├── client
│   ├── Dockerfile
│   └── ... (other Client files)
├── nginx
│   ├── nginx.conf
│   └── ssl
│       ├── nginx-selfsigned.crt
│       └── nginx-selfsigned.key
├── docker-compose.yml
└── .github
    └── workflows
        └── ci-cd.yml
```

## Step 1: Create Dockerfile for API

1. **Create a `Dockerfile` in the `api` directory.**
2. **Use an official PHP image** as the base.
3. **Install necessary system dependencies** and PHP extensions.
4. **Set the working directory** inside the container.
5. **Install Composer** to manage PHP dependencies.
6. **Copy project files** and install Laravel dependencies.
7. **Set file permissions** to allow the web server to access them.

## Step 2: Create Dockerfile for Client

1. **Create a `Dockerfile` in the `client` directory.**
2. **Use Node.js as the base image**.
3. **Set the working directory**.
4. **Copy the package.json and package-lock.json files**.
5. **Install project dependencies**.
6. **Copy the rest of the application files**.
7. **Build the project for production**.
8. **Expose the required port** and start the Nuxt.js application.

## Step 3: Create Docker Compose File

1. **Create a `docker-compose.yml` file** at the root directory.
2. **Define services for the MySQL database, API, Client, and Nginx**.
3. **Set environment variables** for the API service to connect to the database.
4. **Configure volume mounts** for persistent storage.

## Step 4: Nginx Configuration

1. **Create an `nginx.conf` file** in the `nginx` directory.
2. **Configure Nginx to redirect HTTP traffic to HTTPS**.
3. **Set up server blocks** to handle HTTPS requests for the Client and API.
4. **Include SSL configuration** to specify certificate paths and protocols.

## Step 5: Create Self-Signed SSL Certificate

1. **Create a directory for SSL certificates** within the Nginx directory.
2. **Run the OpenSSL command** to generate a self-signed certificate and key.

```bash
mkdir -p nginx/ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout nginx/ssl/nginx-selfsigned.key \
-out nginx/ssl/nginx-selfsigned.crt \
-subj "/C=US/ST=State/L=City/O=Organization/OU=Unit/CN=localhost"
```

## Step 6: Implement CI/CD Pipeline

1. **Create a GitHub Actions workflow file** in `.github/workflows/ci-cd.yml`.
2. **Set up the workflow to trigger on pushes to the `main` branch**.
3. **Define jobs to build Docker images for both the API and Client**.
4. **Log in to Docker Hub and push the built images**.

### Adding Docker Hub Credentials in GitHub

To allow the CI/CD pipeline to push Docker images to Docker Hub:

1. **Navigate to your GitHub repository**.
2. **Go to `Settings` > `Secrets and variables` > `Actions`**.
3. **Click on `New repository secret`**.
4. **Add two secrets**:
   - `DOCKER_USERNAME`: Your Docker Hub username.
   - `DOCKER_TOKEN`: Your Docker Hub access token.

### Explanation of CI/CD Pipeline

- The pipeline is set up to automatically build Docker images for the API and Client whenever changes are pushed to the `main` branch.
- It logs into Docker Hub using the credentials stored as secrets.
- The images are then tagged and pushed to Docker Hub for deployment.

## Step 7: Run the Application

1. **Open a terminal** in the project root directory.
2. **Run the following command to start all services**:

```bash
docker-compose up --build
```

3. **Access the application** via your browser at `http://localhost` for HTTP and `https://localhost` for HTTPS.

## Warnings and Troubleshooting

- Ensure that the ports used in the `docker-compose.yml` file are not already in use by other services on your machine.
- If you encounter permission issues, check the file permissions for your project files.
- Ensure Docker is running before executing any commands.
- Ensure all containers are on the same network to avoid communication issues.

## Screenshots

![Application Running](./screenshot/screenshot.png)


