# Docker Tarea 8

## Objetivo

El objetivo de este ejercicio es crear un entorno con Docker que incluya dos servidores `Tomcat`, una base de datos `MariaDB` y una `bbdd no sql` y así como los clientes para acceder a ambas bases de datos. Para esto, configuraremos los contenedores con redes personalizadas y un `volumen común` para persistir datos.

## Docker Compose

**Docker Compose** es una herramienta que permite definir y ejecutar aplicaciones de Docker de múltiples contenedores. A través de un archivo YAML (generalmente llamado `docker-compose.yml`), puedes definir todos los servicios, redes y volúmenes que tu aplicación necesita. Docker Compose facilita la orquestación de contenedores, permitiendo gestionar proyectos más complejos que requieren la interacción de varios contenedores.

---

### Componentes principales de Docker Compose

#### 1. **Version**:

Define la versión del archivo de configuración de Docker Compose. Asegura que se utilicen las características adecuadas de Docker y Docker Compose.

