# Docker Tarea 6

## Objetivo

Conectar una Base de Datos NoSQL con un Cliente de Base de Datos.

## Redes disponibles

Lista el conjunto de redes disponibles en este momento.

```bash
docker network ls
```

<img src=./images/image1.png width="500">


## Pasos del Ejercicio

### Crear una Red Personalizada

Ejecuta el siguiente comando para crear una red llamada `mongodb-network`:

```bash
docker network create mongodb-network
```

Ejecuta `docker network ls`, y muestra las redes disponibles en `docker`.

<img src=./images/image2.png width="500">

### Crear un Volumen para MongoDB

Ejecuta el siguiente comando para crear un volumen llamado mongodb-data:

```bash
docker volume create mongodb-data
```

> ***Esto permitirá que los datos de MongoDB persistan incluso si el contenedor se elimina***.


Ejecuta `docker volume ls`, y muestra el resultado:

```bash
docker volume ls
```

<img src=./images/image3.png width="300">

### Levantar el Contenedor MongoDB

Usa el siguiente comando para ejecutar MongoDB con el volumen y la red configurados:

```bash
docker run -d --name mongodb-container \
  --network mongodb-network \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=admin123 \
  -v mongodb-data:/data/db \
  -p 27017:27017 \
  mongo:latest
```


<img src=./images/image4.png width="700">

### Levantar el Contenedor Mongo Express

Mongo Express es un cliente web para gestionar MongoDB. Usa este comando para levantar el contenedor:

```bash
docker run -d --name mongo-express-container \
  --network mongodb-network \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=admin123 \
  -e ME_CONFIG_MONGODB_SERVER=mongodb-container \
  -p 8081:8081 \
  mongo-express:latest
```

<img src=./images/image5.png width="700">

Obtendremos una solución similar a la siguiente:

```bash
latest: Pulling from library/mongo-express
619be1103602: Pull complete 
7e9a007eb24b: Pull complete 
5189255e31c8: Pull complete 
88f4f8a6bc8d: Pull complete 
d8305ae32c95: Pull complete 
45b24ec126f9: Pull complete
```


### Verificar los Contenedores Activos

Lista los contenedores activos para asegurarte de que están funcionando correctamente:

```bash
docker ps
```

<img src=./images/image6.png width="700">

Podemos observar ambos contenedores, con `MongoDB` en el puerto `27017` y `Mongo Express` en el puerto `8081`.

### Verifica los logs de Mongo Express

Verifica los logs de Mongo Express:

```bash
docker logs mongo-express-container
```

Acceder al Cliente Mongo Express
Abre tu navegador y visita:

```bash
localhost:8081
```

<img src=./images/image7.png width="700">


### Prueba la persistencia de BBDD

Accede a MongoDB desde el Cliente
Crea una nueva base de datos llamada `testdb`.

<img src=./images/image8.png width="700">

#### Crear la Colección users

Una vez dentro de la base de datos (por ejemplo, exampledb):

- Haz clic en el botón Create.
- Collection (Crear colección). Escribe el nombre de la colección, por ejemplo: `users`.
Haz clic en Create (Crear).

<img src=./images/image9.png width="700">


