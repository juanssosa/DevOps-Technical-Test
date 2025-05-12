# 🧪 DevOps Technical Assessment – Parking Lot App

Este repositorio forma parte de una **prueba técnica interna para candidatos al área de DevOps en Quind**. Contiene una aplicación backend desarrollada en Java con Spring Boot, que simula un sistema de gestión de parqueaderos. El propósito de esta prueba es evaluar habilidades relacionadas con construcción de imágenes, automatización de despliegues, integración continua y monitoreo.

---

## ⚙️ Tecnologías principales

- Java 17
- Spring Boot 3
- Maven
- CI/CD con GitHub Actions


---

## 🚀 ¿Cómo compilar la aplicación?

Para compilar localmente:

```bash
mvn clean package -DskipTests
```
Esto generará el archivo target/parkinglot-0.0.1-SNAPSHOT.jar.

### Ejecutar la aplicación localmente

```bash
java -jar target/parkinglot-0.0.1-SNAPSHOT.jar
```

### Crear contenedor de base de datos MySQL

```bash
docker run --name parking-db -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=parkinglot -e MYSQL_USER=parkinguser -e MYSQL_PASSWORD=secret -p 3306:3306 -d mysql:8
```

### Construir y ejecutar imagen Docker localmente

```bash
docker build -t parkinglot-app:v1.0 .
docker run --name parking-app --env-file .env -p 1222:1222 parkinglot-app:v1.0
```

### Ejecutar imagen desde Docker Hub

```bash
docker run --name parking-app --env-file .env -p 1222:1222 duvangt/juan-sosa:v1.0
```

## ⚙️ Configuración

### Ejemplo de archivo `.env`

```
PARKING_LOT_DB_IP=host.docker.internal
PARKING_LOT_DB_PORT=3306
DATABASE_USERNAME=parkinguser
DATABASE_PASSWORD=secret
```


### Acceso a Swagger UI

```
http://localhost:1222/swagger-ui/index.html
```

## 📚 Comandos utilizados en la prueba técnica

```bash
# Compilación
mvn clean package -DskipTests
java -jar target/parkinglot-0.0.1-SNAPSHOT.jar

# Base de datos
docker run --name parking-db -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=parkinglot -e MYSQL_USER=parkinguser -e MYSQL_PASSWORD=secret -p 3306:3306 -d mysql:8

# Aplicación Docker
docker build -t parkinglot-app:v1.0 .
docker run --name parking-app --env-file .env -p 1222:1222 parkinglot-app:v1.0
docker run --name parking-app --env-file .env -p 1222:1222 duvangt/juan-sosa:v1.0

```

## 🔄 CI/CD con GitHub Actions

El pipeline de CI/CD realiza las siguientes tareas:

- Compila la aplicación con Maven
- Publica el archivo `.jar` como artefacto del pipeline
- Construye y publica una imagen Docker etiquetada como `duvangt/juan-sosa:v1.0`
- Sube automáticamente la imagen a Docker Hub usando GitHub Actions

Este pipeline se ejecuta en la rama master y está definido en `.github/workflows/devops-test.yml`