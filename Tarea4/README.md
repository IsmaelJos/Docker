# Docker Tarea 4

## Objetivo

En este ejercicio, aprenderás a instalar y configurar una `base de datos MariaDB` dentro de un contenedor docker, junto con un `cliente de base de datos` para interactuar con ella. Además, se explicarán cada uno de los pasos y parámetros utilizados en los comandos.

## **Descargar e iniciar un contenedor MariaDB**

Ejecuta el siguiente comando para descargar la imagen oficial de MariaDB y crear un contenedor:

```bash
docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=exampledb -p 3306:3306 -d mariadb:latest
```

<img src=./images/image2.png width="700">

### **Verificar que el contenedor esté corriendo**  

Ejecuta el siguiente comando para listar los contenedores en ejecución:

```bash
docker ps
```

<img src=./images/image3.png width="700">


### **Descargar un cliente de base de datos para MariaDB (Adminer)**

En primer lugar debemos de encontrar un cliente de bbdd que este en docker. Uno de ellos, con una buena interfaz gráfica es `CloudBeaver`.

<img src="https://picx.zhimg.com/v2-b9d6d1d3aeb2344c2f4ff04595d4c765_720w.jpg?source=172ae18b" width="400px">

Vamos a realizar los pasos para configurarar CloudBeaver, una versión web de DBeaver Community, para gestionar bases de datos MariaDB utilizando Docker.

---

### **Descargar y ejecutar CloudBeaver en Docker**

Ejecuta el siguiente comando para iniciar un contenedor de CloudBeaver:

```bash
docker run -d --name cloudbeaver -p 8978:8978 dbeaver/cloudbeaver:latest
```

<img src=./images/image4.png width="700">

Comprobacion de la imagen de CloudBeaver

```bash
docker ps -a
```

<img src=./images/image5.png width="700">


### **Acceder a la interfaz de CloudBeaver**

- Abre un navegador web.
- Navega a la dirección `http://localhost:8978`.
- Sigue las instrucciones de configuración inicial.

Realiza la configuración del cliente:

<img src=./images/image6.png width="700">

---

### **Conectar CloudBeaver a MariaDB**

- Desde la interfaz de CloudBeaver, selecciona `New Connection (Nueva conexión)`.
- Selecciona `MariaDB/MySQL` como tipo de base de datos.
- Introduce los datos de conexión:
 Host: `ip` -> `192.168....`.
- Puerto: `3306` *(el puerto configurado para MariaDB)*.
- Usuario: `root` *(u otro usuario configurado)*.
- Contraseña: `admin` *(o la contraseña configurada para el usuario)*.
- Base de datos: `exampledb` *(u otra base de datos que hayas configurado).

- Haz clic en `Test Connection` para verificar la conexión.

- Si la conexión es exitosa, haz clic en `Finish`.

<img src=./images/image1.png width="700">

