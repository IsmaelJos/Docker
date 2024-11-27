# Docker Tarea 2

## Paso 1: Preparación del Entorno

1. Verifica que Docker está instalado y funcionando:

```bash
docker --version
```
<img src=./images/image.png width="300">

2. Asegúrate de que ningún servicio en tu máquina está utilizando el puerto 8080 (o el puerto que desees asignar).

---

## Paso 2: Descargar la Imagen de Tomcat

1. Descarga la imagen oficial de Apache Tomcat desde Docker Hub:

```bash
docker pull tomcat
```

<img src=./images/image2.png width="500">


2. Confirma que la imagen fue descargada correctamente:

```bash
docker images
```

Busca `tomcat` en la lista de imágenes disponibles.

<img src=./images/image3.png width="500">

---

## Paso 3: Ejecutar el Contenedor de Tomcat

1. Inicia un contenedor basado en la imagen de Tomcat, asignando un puerto específico (por ejemplo, 9090 en la máquina anfitriona):

    ```bash
      docker run -d -p 9090:8080 --name tomcat-server tomcat
    ```

    <img src=./images/image4.png width="500">

2. Verifica que el contenedor está en ejecución:

    ```bash
    docker ps
    ```

    <img src=./images/image5.png width="500">

---

## Paso 4: Probar la Configuración

1. Abre un navegador web y accede a la dirección:

`http://localhost:9090`

<img src=./images/image6.png width="500">

2. Tanto si accedes por el navegador como si no, accede a los `logs`del servidor para ver si el arranque ha sido correcto:

```bash
docker logs tomcat-server
````

<img src=./images/image7.png width="1000">

---

## Paso 5: Detener y Eliminar el Contenedor

1. Detén el contenedor:

```bash
docker stop tomcat-server
```

2. Elimina el contenedor:

```bash
docker rm tomcat-server
```

3. Si deseas eliminar la imagen de Tomcat de tu sistema:

```bash
docker rmi tomcat
```

<img src=./images/image8.png width="500">

---

## Reto Adicional

- Arranca `apache tomcat` en `otro puerto`, y verifica realiza los pasos anteriores.

<img src=./images/image9.png width="500">
