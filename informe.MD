# TAS4 - Red de contenedores mysql y phomyadmin
## 1. Título
**Implementación de Contenedores Docker para MySQL y phpMyAdmin en una Red Personalizada**

## 2. Tiempo de duración
30 minutos

## 3. Fundamentos
Un contenedor se basa en una imagen, que es una plantilla inmutable con las instrucciones necesarias para crear el entorno del software. Por ejemplo, la imagen oficial de MySQL contiene todo lo necesario para levantar un servidor de base de datos, mientras que la imagen de phpMyAdmin incluye la interfaz web para gestionar bases de datos MySQL.

En esta práctica se implementan dos contenedores interconectados:

- Uno ejecutando MySQL, encargado de gestionar bases de datos.
- Otro ejecutando phpMyAdmin, que actúa como interfaz gráfica web para conectarse al servidor MySQL.

Ambos contenedores se comunican dentro de una red personalizada de Docker, lo cual facilita que solo ellos se vean entre sí, manteniendo la seguridad y el aislamiento del entorno.

Este tipo de implementación es ampliamente usada en entornos de desarrollo y despliegue de aplicaciones modernas, ya que permite simular infraestructuras completas (bases de datos, aplicaciones, interfaces, etc.) sin instalar cada servicio directamente en el sistema operativo anfitrión.

## 4. Conocimientos previos
- Gestión de redes en Docker.
- Manejo básico de bases de datos MySQL.
- Uso de navegadores web para acceder a servicios locales.
- Concepto de contenedor, imagen, red y puerto en Docker.

## 5. Objetivos a alcanzar
- Implementar contenedores Docker utilizando imágenes oficiales de MySQL y phpMyAdmin.
- Configurar una red personalizada que permita la comunicación entre los contenedores.
- Acceder a phpMyAdmin desde el navegador y conectarlo con el contenedor MySQL.
- Crear una base de datos de prueba desde la interfaz web de phpMyAdmin.
- Comprender la estructura y comunicación entre servicios dentro de un entorno Dockerizado.

## 6. Equipo necesario
- Docker Desktop instalado y en ejecución.
- Computador con sistema operativo Windows 10/11, Linux o macOS.
- Navegador web (Chrome, Edge, Firefox).

## 7. Material de apoyo
- Documentación oficial de Docker: https://docs.docker.com
- Guía de la asignatura.
- Cheat Sheet de comandos Linux y Docker.
- Notas de clase sobre contenedores y redes.

## 8. Procedimiento

#### Paso 1: Crear la red personalizada
Abrir PowerShell o la terminal de docker y ejecutar:

```powershell
docker network create my-network
```

Esto crea una red interna llamada my-network.
![Figura 8-1.](img/Screenshot%202025-11-01%20184039.png)

#### Paso 2: Crear el contenedor de MySQL
```powershell
docker run -d `
--name mysql-container `
--network my-network `
-e MYSQL_ROOT_PASSWORD=rootpassword `
-e MYSQL_DATABASE=testdb `
-e MYSQL_USER=testuser `
-e MYSQL_PASSWORD=testpass `
mysql:8.0
```
Esto descarga la imagen oficial de MySQL y levanta el servidor de base de datos.

![Figura 8-3.](img/Screenshot%202025-11-01%20184553.png)

#### Paso 3: Crear el contenedor de phpMyAdmin
```powershell
docker run -d `
--name phpmyadmin-container `
--network my-network `
-e PMA_HOST=mysql-container `
-e PMA_USER=root `
-e PMA_PASSWORD=rootpassword `
-p 8080:80 `
phpmyadmin/phpmyadmin
```
Esto lanza phpMyAdmin y lo hace accesible desde el navegador en http://localhost:8080.

![Figura 8-1.](img/Screenshot%202025-11-01%20184801.png)

#### Paso 4: Acceder a phpMyAdmin
Abrir el navegador e ingresar: http://localhost:8080
phpMyAdmin se conectará al servidor mysql-container.

![Figura 8-1.](img/Screenshot%202025-11-01%20192919.png)

#### Paso 5: Crear una base de datos de prueba
Desde phpMyAdmin:
- Clic en Nueva base de datos.
- Ingresar el nombre base_prueba.
- Presionar Crear.

![Figura 8-1.](img/Screenshot%202025-11-01%20185640.png)

## 9. Resultados esperados
La práctica ha demostrado satisfactoriamente el mecanismo de persistencia de datos en Docker.

- Dos contenedores en ejecución (mysql-container y phpmyadmin-container).
- Una red personalizada creada (my-network).
- Acceso exitoso a phpMyAdmin desde el navegador.
- Comunicación estable entre phpMyAdmin y MySQL.
- Una base de datos creada desde la interfaz web.

Estas condiciones confirman la correcta configuración de contenedores, red y credenciales.

## 10. Bibliografía
- Docker Inc. (2024). Docker Documentation. Recuperado de https://docs.docker.com
- Oracle Corporation. (2024). MySQL 8.0 Reference Manual. Recuperado de https://dev.mysql.com/doc/
- phpMyAdmin Team. (2024). phpMyAdmin Documentation. Recuperado de https://www.phpmyadmin.net/docs/
- Pérez, L. (2023). Guía de prácticas de virtualización y contenedores. Universidad Técnica de Loja.