# MariaDB-y-Docker
# Creación de Servidor MariaDB con Docker y Documentación para Git

## 1. Instalación de Docker y Docker Compose
### 1.1. Verificar la instalación de Docker
```bash
docker --version
```
Descargar e instalar desde [Docker](https://www.docker.com/get-started) si no está instalado.

### 1.2. Verificar Docker Compose
```bash
docker compose version
```
Si es necesario, instalar desde la [documentación oficial](https://docs.docker.com/compose/).

---
## 2. Crear el Contenedor de MariaDB
### 2.1. Descargar la imagen de MariaDB
```bash
docker pull mariadb:latest
```
### 2.2. Crear la red Docker (opcional)
```bash
docker network create database-net
```
### 2.3. Crear y ejecutar el contenedor
```bash
docker run -d \
  --name mariadb-server \
  --network database-net \
  -e MARIADB_ROOT_PASSWORD=admin123 \
  -e MARIADB_DATABASE=universidad_db \
  -e MARIADB_USER=admin \
  -e MARIADB_PASSWORD=admin123 \
  -p 3306:3306 \
  mariadb:latest
```
---
## 3. Crear una Tabla en MariaDB
### 3.1. Conectarse al servidor MariaDB
```bash
docker exec -it mariadb-server mariadb -u admin -p
```
- Contraseña: `admin123`

### 3.2. Crear la tabla "estudiantes"
```sql
CREATE TABLE estudiantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    correo VARCHAR(100) UNIQUE,
    edad INT
);
```
### 3.3. Verificar la tabla
```sql
SHOW TABLES;
DESCRIBE estudiantes;
```
### 3.4. Salir de MariaDB
```sql
EXIT;
```
---
## 4. Exponer la Base de Datos
- El contenedor ya está expuesto en el puerto `3306`. Puedes conectarte usando cualquier cliente MySQL/MariaDB.

---
