# Docker Project: Basic Microservices Demo

This repository contains the Dockerfiles and Docker Compose configuration needed to build and run the demo applications from the [basic-microservices](https://github.com/kkenan/basic-microservices) repository. It includes:

- A Dockerfile for the Spring Boot application (`Dockerfile.spring-boot-app`)
- A Dockerfile for the Node.js application (`Dockerfile.node-app`)
- A Docker Compose file (`docker-compose.yml`) to orchestrate the multi-container setup along with PostgreSQL 10

> **Note:** This setup is designed for Linux environments. For Windows, see the "Additional Notes for Windows Users" section below.

## Prerequisites

- Docker
- Docker Compose

## How to Run

1. **Clone this repository:**

   ```bash
   git clone <your-docker-project-repo-url>
   cd docker-project
   ```

2. **Build and run all services using Docker Compose:**

    ```bash
    docker-compose up --build
    ```
    The first run will build the Docker images (cloning the source code from the basic-microservices repository) and start all containers.

3. **Verify the Running Containers:**

    Open a new terminal session and run:

    ```bash
    docker ps
    ```
    You should see containers for spring-boot-app, node-app, and postgres running.

4. **Access the Applications**

    Access the applications using your browser or curl:

    Spring Boot App:
    Open your browser and navigate to:
    http://localhost:8080/java/api/v1/status
    or
    http://localhost:8080/java/api/v1/node

    Node.js App:
    Open your browser and navigate to:
    http://localhost:8081/node/api/v1/result

5. **Run Health Check**

    Once all containers are running, execute the following command on your host machine to verify that everything is working correctly:

    ```bash
    bash <(curl -s https://raw.githubusercontent.com/kkenan/basic-microservices/master/health_check.sh)
    ```

    You should see a message stating 

    ```bash
    "All checks passed. Congrats!"
    ```

6. **Stopping and Removing Containers**

    To stop the containers, open a terminal in the repository directory and run:

    ```bash
    docker-compose down
    ```
    To remove any associated images, volumes, and networks, run:
    ```bash
    docker-compose down --rmi all --volumes --remove-orphans
    ```

## **Additional Notes for Windows Users**
- **Host Networking**:

    On Linux, you can use Docker’s host networking mode so that a container’s localhost points to the host. This is not supported on Windows.
    
    If you need to connect to a PostgreSQL running on your Windows host, override the JDBC URL by setting the environment variable `SPRING_DATASOURCE_URL` in the Docker Compose file (e.g., set it to `jdbc:postgresql://host.docker.internal:5432/demodb`).

    Note: In the Docker Compose file, uncomment the environment variable settings for Windows and comment out the host networking settings (network mode) or any Linux-specific configurations.
