# Docker Tarea 5

## Objetivo

Configurar un balanceador de carga NGINX que distribuya el tráfico entre dos servidores Tomcat ejecutados en contenedores Docker.

Consulta los comandos de docker en el siguiente [enlace](https://github.com/jpexposito/code-learn/blob/main/comun/docker/COMANDOS.md), y las redes en docker en el siguiente [enlace](https://github.com/jpexposito/code-learn/tree/main/comun/docker/ud-5).

> Recuerda que debes de tener el contenedor docker corriendo

```bash
docker -version
docker ps
```
---

## Redes disponibles

Lista el conjunto de redes disponibles en este momento.

```bash
docker network ls
```

<img src=./images/image1.png width="400">


## Pasos a Seguir

### Crear una Red Docker

Docker necesita una red personalizada para que los contenedores puedan comunicarse entre sí. Ejecuta el siguiente comando:

```bash
docker network create tomcat-network
```

- `docker network create`: Crea una nueva red Docker.
- `tomcat-network`: Es el nombre de la red personalizada.

<img src=./images/image2.png width="400">

### Levanta los Servidores Tomcat

Levanta dos contenedores Tomcat y conéctalos a la red tomcat-network.

#### Servidor Tomcat 1

```bash
docker run -d --name tomcat1 --network tomcat-network -p 8081:8080 tomcat:latest
```

#### Servidor Tomcat 2

```bash
docker run -d --name tomcat2 --network tomcat-network -p 8081:8080 tomcat:latest
```

- `docker run`: Crea y ejecuta un contenedor.
- `-d`: Ejecuta el contenedor en segundo plano (modo "detached").
- `--name tomcat1 y --name tomcat2`: Asigna nombres a los contenedores para identificarlos.
- `--network tomcat-network`: Conecta los contenedores a la red personalizada.
- `-p 8081:8080 y -p 8082:8080`: Expone los puertos 8080 de los contenedores en los puertos 8081 y 8082 de la máquina anfitriona.
- `tomcat:latest`: Usa la última versión de la imagen oficial de Tomcat.

>**Importante**: Levanta los servidores tomcat asociando un **alias** como en las tareas anteriores. Para eso añade el `--name`.

<img src=./images/image3.png width="700">

### Muestra los contenedores dockers activos en ese momento

Muestra el listado de `contenedores` docker que tienes `activos` y `todos los que tienes disponibles`.

```bash
docker ...
```

<img src=./images/image4.png width="1000">


### Fichero de Configuración del Balanceador NGINX

Crea el fichero de balance `nginx.conf` en el `mismo direcctorio` donde estes ejecutando la `consola de comandos`.

```bash
events {}

http {
    upstream tomcat_backend {
        server tomcat1:8080;
        server tomcat2:8080;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://tomcat_backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
}
```
```bash
docker run -d --name nginx --network tomcat-network -p 80:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf nginx:latest
```

<img src=./images/image5.png width="700">

### Verificar que todo esta funcionando correctamente

#### Servidor NGINX

Verifica el comportamiento en:

```bash
http://localhost:8081
```

```bash
http://localhost:8082
```

```bash
http://localhost
```

```bash
http://localhost:80
```

Describe lo que esta sucediendo.

Realiza el despliegue de la aplicación `sample` como se describe en el siguiente [enlace](../tarea-3/README.md).

Repite los pasos del apartado anterior comprobando los puertos `8081`,`8082` y `80` de `localhost`.

<img src=./images/image6.png width="500">

<img src=./images/image7.png width="500">
