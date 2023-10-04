# Dockerized Project README

This README provides an overview of a Dockerized project with multiple components, including Apache Tomcat, NGINX, and MySQL. The project involves building, testing, and storing Docker images on Docker Hub.

## Source (Docker File)

The Dockerfile defines how the application and services are packaged into Docker images.

### Apache Tomcat

- The application is built from an OpenJDK 11 base image.
- Maven is installed, and the project code is cloned and built.

```dockerfile
FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/Kiineo/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install
```
### NGINX

The NGINX web server configuration is set up for the application.
Default NGINX configuration is removed, and a custom configuration is copied.

```
FROM nginx
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginvproapp.conf /etc/nginx/conf.d/vproapp.conf
```
### MySQL
MySQL is configured with specific settings and a database is initialized with provided SQL script.
```
FROM mysql:8.0.33
ENV MYSQL_ROOT_PASSWORD="vprodbpass"
ENV MYSQL_DATABASE="accounts"
ADD db_backup.sql docker-entrypoint-initdb.d/db_backup.sql
```

### Build (Docker Build)
Images for Apache Tomcat, NGINX, and MySQL are built using Docker.

### Test (Docker Compose)
Docker Compose is used to orchestrate the different components and services for testing and development.
```
version: "3.8"

services:
  vprodb:
    # ... MySQL service configuration ...

  vprocache01:
    # ... Memcached service configuration ...

  vpromq01:
    # ... RabbitMQ service configuration ...

  vproapp:
    # ... Application service configuration ...

  vproweb:
    # ... Web service configuration ...

volumes:
  vprodbdata: {}
  vproappdata: {}
```
### Store (Docker Hub)
Docker images are stored and versioned on Docker Hub for easy access and distribution.

### Image Names and Tags
Apache Tomcat: kiineo/vprofileapp
MySQL: kiineo/vprofiledb
NGINX: kiineo/vprofileweb
Images can be pulled from Docker Hub as needed.
