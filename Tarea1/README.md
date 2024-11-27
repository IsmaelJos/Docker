# Docker Tarea 1

## Paso 1: Trabajar con imágenes de Docker

    Para verificar si puede acceder a imágenes y descargarlas de Docker Hub, escriba lo siguiente:

```console
  sudo docker run hello-world
```

  El resultado indicará que Docker funciona de forma correcta:

  <img src=./images/image1.png width="1000">

## Paso 2: Administar contenedores de Docker

Después de usar Docker durante un tiempo, tendrá muchos contenedores activos (en ejecución) e inactivos en su computadora. Para ver los activos, utilice lo siguiente:

```console
  sudo docker run hello-world
```

  <img src=./images/image2.png width="1000">

Para ver el último contenedor que creó, páselo al conmutador -l:

```console
  sudo docker ps -l
```

  <img src=./images/image3.png width="500">

Listar las imágenes de Docker de nuevo mostrará la nueva imagen, así como la anterior de la que se derivó:

```console
    sudo docker images
```

  <img src=./images/image4.png width="500">
