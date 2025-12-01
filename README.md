# Error Control API – Sak Global

Middleware de control y trazabilidad de errores para el ecosistema de microservicios de Sak Global, desarrollado en Java Spring Boot. Este servicio permite registrar, consultar, listar y actualizar errores generados por otros microservicios o por el backend principal, facilitando la auditoría, depuración y análisis del sistema.

## 📌 Descripción General
El microservicio **Error Control** actúa como un componente independiente encargado de:
- Registrar errores provenientes de otros servicios.
- Consultar errores por ID o por código de error (`errorId`).
- Listar todos los registros almacenados.
- Consultar errores de forma paginada.
- Actualizar registros de error cuando haya nueva información disponible.

Todos los endpoints trabajan mediante solicitudes **POST**, reciben un **String encode** en el cuerpo (JSON encriptado, serializado o codificado) y devuelven un `ResponseEntity<String>` o una lista de entidades completas, dependiendo de la operación.

La información se almacena en **MySQL** utilizando **Spring Data JPA**.

## 🛠️ Tecnologías Utilizadas
- Java 17
- Spring Boot
- Spring Web
- Spring Data JPA
- Lombok
- MySQL
- Swagger / OpenAPI 3

## 🚀 Instalación y Ejecución

### 1. Clonar el repositorio
git clone https://github.com/jsco1809/GuardianShopErrorControl.git
cd GuardianShopErrorControl

### 2. Configurar la base de datos en `application.properties`
spring.datasource.url=jdbc:mysql://localhost:3306/error_control
spring.datasource.username=TU_USUARIO
spring.datasource.password=TU_PASSWORD
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

### 3. Ejecutar el proyecto
mvn spring-boot:run

---

## 📡 Endpoints del API

**Base URL:** `/error`  
Todos los endpoints usan método **POST**.

### 🔍 Buscar error por ID
**URL:** `/error/list/id`  
**Body:** String encode (contiene el ID del error)  
**Respuesta:** ResponseEntity<String>

### 🔍 Buscar error por errorId
**URL:** `/error/list/errorId`  
**Body:** String encode (contiene el campo errorId)  
**Respuesta:** ResponseEntity<String>

### 📄 Listar todos los errores
**URL:** `/error/list/all`  
**Body:** vacío  
**Respuesta:** List<ErrorControlEntity>

### 📄 Listar errores con paginación
**URL:** `/error/list/paginated`  
**Body:** String encode (contiene page, size u otros filtros)  
**Respuesta:** ResponseEntity<String>

### ➕ Registrar un nuevo error
**URL:** `/error/addRecord`  
**Body:** String encode (datos del error a registrar)  
**Respuesta:** ResponseEntity<String>

### 🔧 Actualizar un error existente
**URL:** `/error/updateRecord`  
**Body:** String encode (datos del error actualizados)  
**Respuesta:** ResponseEntity<String>

---

## 🧱 Arquitectura del Servicio
El microservicio sigue una estructura en capas:

### ✔️ Controller
Exposición de endpoints:
- `/list/id`
- `/list/errorId`
- `/list/all`
- `/list/paginated`
- `/addRecord`
- `/updateRecord`

### ✔️ Service
Lógica de negocio:
- Validación
- Transformación
- Formateo estandarizado de respuestas

### ✔️ Repository
Conexión y persistencia en MySQL mediante JPA.

### ✔️ Entidad
`ErrorControlEntity` que mapea la tabla de registros de error.

---

## 📘 Documentación Swagger
Una vez ejecutado el proyecto, la documentación está disponible en:

http://localhost:8080/swagger-ui/index.html

---

## 👤 Autor
**Sak Global – Microservicio de Control de Errores**  
Desarrollado para fortalecer la trazabilidad, auditoría y confiabilidad en los microservicios de la plataforma.

