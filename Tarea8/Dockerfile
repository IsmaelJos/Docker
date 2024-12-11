FROM ubuntu:20.04

RUN apt-get update -y && \
    apt-get install -y \
    wget \
    curl \
    unzip \
    mysql-client \
    && rm -rf /var/lib/apt/lists/*

# MariaDB
FROM mariadb:latest

VOLUME /var/lib/mysql

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=exampledb

EXPOSE 3306

# Tomcat
FROM tomcat:latest

COPY ./sample.war /usr/local/tomcat/webapps/

EXPOSE 8081

# CloudBeaver
FROM dbeaver/cloudbeaver:latest

EXPOSE 8978

# Iniciar los servicios 
CMD service mysql start && \
    /opt/tomcat/bin/catalina.sh run & \
    /opt/cloudbeaver/cloudbeaver/bin/cloudbeaver & \
    wait