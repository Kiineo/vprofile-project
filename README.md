# Docker Project README

This README provides an overview of the Docker project and its components. The project's primary objective is to establish a Docker-based infrastructure for hosting various services, including a web application, a MySQL database, Memcached, and RabbitMQ. These Docker containers can be used in conjunction with other projects, such as Kubernetes.

## Project Overview

![DOCKEREXAMPLE](https://github.com/Kiineo/vprofile-project/assets/103956412/48196178-011a-477f-8754-9cf22be63495)

## Project Components

### EC2 Instance
- An EC2 instance is established to host Docker-Engine, serving as the foundation for the entire project.

### Docker Compose Files
- Docker Compose files have been authored to optimize the orchestration of containers, ensuring reliable service delivery and scalability. The following services are defined:
  - MySQL (vprodb)
  - Memcached (vprocache01)
  - RabbitMQ (vpromq01)
  - Web Application (vproapp)
  - Nginx (vproweb)

### Web Application
- The web application is built using OpenJDK 11 and Maven.
- A Docker image is created from the application code and deployed on Tomcat 9.
- The application listens on port 8080.

### Database (MySQL)
- MySQL 8.0.33 is used as the database management system.
- An environment variable is set for the root password (`MYSQL_ROOT_PASSWORD`) and database name (`MYSQL_DATABASE`).
- A SQL backup script (`db_backup.sql`) is added for initialization.

### Cache (Memcached)
- Memcached is used for caching purposes.
- It listens on port 11211.

### Message Queue (RabbitMQ)
- RabbitMQ is used as a message broker.
- It provides management UI on port 15672.
- Default credentials are configured (`RABBITMQ_DEFAULT_USER` and `RABBITMQ_DEFAULT_PASS`).

### Nginx (Web Server)
- Nginx is employed as the web server.
- A custom configuration file (`vproapp.conf`) is used.
- The Nginx container listens on port 80.

## Docker Compose
- Docker Compose is employed to manage and orchestrate the Docker containers.
- All services are defined in the `docker-compose.yml` file.

## Building and Running the Project
1. Ensure Docker is installed on your host system.
2. Clone this repository.
3. Navigate to the project directory.
4. Use the following commands to build and run the project:

```bash
docker-compose build
docker-compose up -d
