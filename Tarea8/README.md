# Docker Tarea 8

## Objetivo

El objetivo de este ejercicio es crear un entorno con Docker que incluya dos servidores `Tomcat`, una base de datos `MariaDB` y una `bbdd no sql` y así como los clientes para acceder a ambas bases de datos. Para esto, configuraremos los contenedores con redes personalizadas y un `volumen común` para persistir datos.

---

## Pasos

### Paso 1: Crea la red personalizada y un volumen común

Primero, crea una red Docker personalizada para que los contenedores puedan comunicarse entre sí.

```bash
docker network create tarea8
```

Luego, crea un volumen Docker para persistir los datos.

```bash
docker volume create my_db_volume
```

<img src=./images/image1.png width="500">

### Paso 2: Crear el Dockerfile

A continuación, creamos un Dockerfile que instalará Tomcat, MariaDB y CloudBeaver.

```bash
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
```

### Paso 3: Construir y ejecutar la imagen

Para construir la imagen desde el Dockerfile, usa el siguiente comando:

```bash
docker build -t solucion-servicios .
```
<img src=./images/image2.png width="500">

Lista las imagenes que tienes en tu equipo:

```bash
docker images
```

<img src=./images/image3.png width="700">

Luego, para ejecutar el contenedor que contiene Tomcat, MariaDB,CloudBeaver, etc y usa:

```bash
docker run -d -p 8080:8080 -p ... solucion-servicios
```  

Lista los contenedores que tienes en tu equipo:

```bash
docker ps -a
```