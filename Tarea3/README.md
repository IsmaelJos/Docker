# Docker Tarea 3

## Objetivo

Desplegar una aplicación en Apache Tomcat.

> Realiza los pasos de arranque de Tomcat descritos en la [tarea anterior](../Tarea2/README.md).

> Recuerda que debes de tener el contenedor docker corriendo


## **Prueba con una aplicación de ejemplo**

Como prueba, puedes descargar una aplicación `.war` de ejemplo y desplegarla en Tomcat. Sigue estos pasos:

### **Descargar un archivo `.war` de ejemplo**  

Puedes descargar una aplicación de ejemplo desde el sitio oficial de Apache Tomcat. Por ejemplo, la [Sample Web Application](https://tomcat.apache.org/tomcat-11.0-doc/appdev/sample/) de Tomcat.


> **Nota**:Si prefieres, puedes crear tu propio archivo `.war` usando herramientas como `Maven` o `Gradle`, lo que añade un paso extra de aprendizaje sobre cómo empaquetar aplicaciones web.

### **Copiar el archivo `.war` en el contenedor**

Una vez descargado el archivo `.war` (por ejemplo, `sample.war`), cópialo al directorio `webapps` de tu contenedor Tomcat. Si estás ejecutando Tomcat en Docker, puedes hacerlo con un comando como este:

```bash
docker cp /ruta/a/sample.war <nombre_contenedor>:/usr/local/tomcat/webapps/
```

> **Nota**: Recuerdas como se llamaba tu `contenedor` de tomat. Revisa la [tarea](../tarea-2/).

- `docker cp`: Copia un archivo desde tu máquina local al contenedor Docker donde está ejecutándose Tomcat.
- `/ruta/a/sample.war`: Especifica la ubicación del archivo .war en tu máquina.
- `<nombre_contenedor>`: El identificador o nombre del contenedor Docker que está ejecutando Tomcat.
- `/usr/local/tomcat/webapps/`: Es el directorio estándar donde Tomcat busca archivos .war para desplegar automáticamente.


<img src=./images/image1.png width="500">


### **Acceder a la aplicación**

Una vez copiado el archivo `.war` y desplegado en Tomcat, puedes acceder a la aplicación de ejemplo a través de la URL:

```bash
http://localhost:9090/sample
```

- `localhost`: Indica que el servidor está ejecutándose en tu máquina local.
- `9090`: Es el puerto donde Tomcat está escuchando (ajusta esto si configuraste otro puerto).
- `/sample`: Es el nombre de la aplicación, derivado del archivo .war.

> Debes ver algo como:

<img src=./images/image2.png width="500">

### **Verificar logs en caso de problemas**

Si la aplicación de ejemplo tampoco funciona, revisa los logs de Tomcat para detectar posibles errores:

```bash
docker logs -f <nombre_contenedor>
```

Busca cualquier mensaje relacionado con el despliegue o errores en la configuración.

<img src=./images/image3.png width="1000">


---
