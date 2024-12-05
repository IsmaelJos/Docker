# Docker Tarea 7

## Objetivo

El objetivo de este ejercicio es crear un entorno con Docker que incluya un servidor `Tomcat`, una base de datos `MariaDB` y un cliente para acceder a la base de datos. Para esto, configuraremos los contenedores con redes personalizadas y un `volumen común` para persistir datos.

---

## Requisitos

- Crear una red Docker personalizada para los contenedores.
- Crear un contenedor Tomcat para desplegar una aplicación web.
- Crear un contenedor MariaDB para gestionar la base de datos.
- Utilizar un volumen común para persistir los datos de la base de datos.

---

## Pasos

### Paso 1: Crea la red personalizada

Primero, crea una red Docker personalizada para que los contenedores puedan comunicarse entre sí.

```bash
docker network create tarea7_network
```

### Paso 2: Crear un volumen común

Luego, crea un volumen Docker para persistir los datos.

```bash
docker volume create tarea7_volume
```

<img src=./images/image1.png width="500">


### Paso 3: Crear el Dockerfile

A continuación, creamos un Dockerfile que instalará Tomcat, MariaDB y CloudBeaver.

```bash
    # Usar una imagen base de Ubuntu para las instalaciones adicionales
    FROM ubuntu:20.04

    # Instalar dependencias necesarias (como wget y curl)
    RUN apt-get update -y && \
        apt-get install -y \
        wget \
        curl \
        unzip \
        mysql-client \
        && rm -rf /var/lib/apt/lists/*

    # Configurar MariaDB usando la imagen oficial
    FROM mariadb:latest

    # Volúmenes para MariaDB
    VOLUME /var/lib/mysql

    # Configuración de MariaDB: Establecer la contraseña root y crear la base de datos (esto es suficiente con las variables de entorno)
    ENV MYSQL_ROOT_PASSWORD=root
    ENV MYSQL_DATABASE=exampledb

    EXPOSE 3306

    # Configurar Tomcat usando la imagen oficial
    FROM tomcat:latest

    COPY ./sample.war /usr/local/tomcat/webapps/

    EXPOSE 8081

    # Descargar y configurar CloudBeaver utilizando la imagen oficial de CloudBeaver desde Docker Hub
    FROM dbeaver/cloudbeaver:latest

    # Exponer puertos
    EXPOSE 8978


    # Iniciar los servicios de MariaDB, Tomcat y CloudBeaver
    CMD service mysql start && \
        /opt/tomcat/bin/catalina.sh run & \
        /opt/cloudbeaver/cloudbeaver/bin/cloudbeaver & \
        wait
```

## ¿Qué estamos haciendo?

Explicación del Dockerfile:

- `Instalación de dependencias`: Se instalan los paquetes necesarios como **wget, curl, mysql-client, y unzip***.
- `Tomcat`: Se descarga e instala `Tomcat`, y se añade la aplicación de ejemplo (`sample.war`).
- `MariaDB`: Se instala `MariaDB` utilizando el script oficial.
- `CloudBeaver`: Se descarga e instala CloudBeaver, un cliente de base de datos basado en la web.
- `Volúmenes`: Se crea un volumen para persistir los datos de MariaDB en `/var/lib/mysql`.
- Comando `CMD`: El comando ejecuta `MariaDB`, luego `Tomcat` y finalmente `CloudBeaver`, para que los tres servicios estén activos y funcionen correctamente.

### Paso 4: Construir y ejecutar la imagen
Para construir la imagen desde el Dockerfile, usa el siguiente comando:

```bash
docker build -t tomcat-mariadb-cloudbeaver .
```

Lista los contenedores que tienes en tu equipo:

```bash
docker ps -a 
```

Luego, para ejecutar el contenedor que contiene Tomcat, MariaDB y CloudBeaver, usa:

```bash
docker run -d -p 8080:8080 -p 8081:8081 tomcat-mariadb-cloudbeaver
```  

