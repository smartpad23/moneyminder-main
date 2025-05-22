# 💰 MoneyMinder

**MoneyMinder** es una aplicación de gestión financiera personal que permite registrar gastos e ingresos, asignar presupuestos y visualizar información detallada de tus finanzas. Está compuesta por microservicios desarrollados con **Spring Boot**, un API Gateway con **Spring Cloud Gateway**, bases de datos **PostgreSQL**, y un frontend construido con **React + Vite**.

---

## 📦 Arquitectura
- **Frontend:** Realizado con React/Vite. Conecta con el Api Gateway para obtener los datos de back.
- **Api Gateway:** Realizado con Spring Cloud. Sirve como puerta de enlace a los microservicios y al Auth Service.
- **Expenses Service:** Realizado con Spring Boot. Contiene los end points de gastos e ingresos, detalles de gastos e ingresos y presupuestos.
- **Users Service:** Realizado con Spring Boot. Contiene el Auth Service y los end points de usuarios, grupos y solicitudes de grupos.
- **PostgreSQL Expenses:** Base de datos en PostgreSQL enlazada a Expenses Service.
- **PostgreSQL Users:** Base de datos en PostgreSQL enlazada a Users Service.

\* El servicio de autenticación está integrado en el Users Service, utilizando JWT y OAuth2.

---

## 🚀 Tecnologías utilizadas

- **Backend:** Spring Boot, Spring Security, Spring Data JPA
- **API Gateway:** Spring Cloud Gateway
- **Bases de datos:** PostgreSQL
- **Frontend:** React 18 + Vite
- **Contenedores:** Docker y Docker Compose
- **Documentación:** Swagger/OpenAPI via SpringDoc
- **Pipes CI/CD** GitHub Actions

---

## 🧩 Microservicios

### ✅ Users Service
- Registro y autenticación de usuarios
- Emite tokens JWT
- Gestión de perfiles
- Creación y gestión de grupos
- Creación y gestión de solicitudes de grupos
- Puerto: `18082`

### ✅ Expenses Service
- Registro de gastos e ingresos
- Asociaciones gastos e ingresos con usuarios
- Creación y gestión de presupuestos
- Asociación de presupuestos con grupos
- Creación y gestión de detalles de un ingreso o gasto
- Puerto: `18081`

### ✅ API Gateway
- Enrutamiento centralizado
- Verificación de JWT
- Reenvía tráfico a los servicios
- Puerto: `18080`

### ✅ Frontend
- SPA desarrollada con React + Vite
- Interactúa a través del API Gateway
- Puerto dev: `5173`
- Puerto prod: `8180`

---
## 🏛️ Estructura del proyecto y repositorios

El proyecto está organizado en torno a un repositorio principal que contiene y coordina a los subrepositorios (expenses-services, users-service, api-gateway y front).
- **Repositorio principal**: moneyminder-main (https://github.com/moneyminder-project/moneyminder-main)
   - expenses-service (https://github.com/moneyminder-project/moneyminder-expenses)
   - users-service (https://github.com/moneyminder-project/moneyminder-users)
   - api-gateway (https://github.com/moneyminder-project/moneyminder-gateway)
   - front(https://github.com/moneyminder-project/moneyminder-front)

---

## 🧪 Entornos disponibles

La aplicación soporta dos entornos:

- **Development (`--profile development`)**
- **Production (`--profile production`)**

---

## 🐳 Cómo ejecutar (modo desarrollo)

1Me p. Inicia los servicios:
   ```bash
      docker compose --profile development up --build
   ```

3. Accede a:
    - **Frontend:** [http://localhost:5173](http://localhost:5173)
    - **Gateway:** [http://localhost:18080](http://localhost:18080)
    - **Swagger (Expenses):** [http://localhost:18081/swagger-ui.html](http://localhost:18081/swagger-ui.html)
    - **Swagger (Users):** [http://localhost:18082/swagger-ui.html](http://localhost:18082/swagger-ui.html)
    - **Adminer (UI DB):** [http://localhost:9090](http://localhost:9090)

---

## 🛠 Variables de entorno

Cada microservicio permite sobreescribir propiedades mediante variables de entorno. Algunas comunes:

- `SPRING_DATASOURCE_URL`
- `SPRING_DATASOURCE_USERNAME`
- `SPRING_DATASOURCE_PASSWORD`
- `JWK_SET_URI`
- `GROUP_SERVICE_URL` / `BUDGET_SERVICE_URL`

Estas se definen en el `docker-compose.yml` y se inyectan automáticamente en los servicios.

---

## 🗃️ Bases de datos

Se levantan dos instancias de PostgreSQL:

- `postgres-users` (puerto local: 5433)
- `postgres-expenses` (puerto local: 5434)

Puedes acceder a ellas con Adminer o cualquier cliente PostgreSQL usando:
- Usuario: `postgres`
- Contraseña: `12345`

---

## 📜 Documentación de APIs

Ambos microservicios exponen documentación Swagger en:

- **Users:** [http://localhost:18082/swagger-ui.html](http://localhost:18082/swagger-ui.html)
- **Expenses:** [http://localhost:18081/swagger-ui.html](http://localhost:18081/swagger-ui.html)

---

## 🧼 Limpieza

Para parar y eliminar contenedores y volúmenes:

```bash
   docker compose --profile development down -v
```

---

## ✅ Estado actual

- [x] Autenticación con JWT
- [x] Gestión de usuarios
- [x] Registro de ingresos/gastos
- [x] Presupuesto donde añadir gastos/ingresos
- [x] Solicitudes para añadir usuarios a presupuestos
- [x] API Gateway con seguridad
- [x] Frontend responsive
- [x] Docker Compose listo para dev/prod

---

## 📌 Próximas mejoras

- Añadir foto de perfil subida por el usuario
- Descargar datos en formato Excel
- Añadir etiquetas a los registros y presupuestos para facilitar la organización y búsqueda
- Añadir traducción a la web (castellano e inglés)
- Añadir la posibilidad de adjuntar imágenes y geolocalización en registros (gastos e ingresos)
- Permitir generar un presupuesto a partir de otro, copiando sus datos
- Permitir generar un registro (gasto o ingreso) a partir de otro, copiando sus datos
- Añadir gráficos para el análisis de gastos e ingresos

---

## 👥 Autores

El proyecto ha sido desarrollado para la asignatura de TFG del Grado de Ingeniería Informática
- **Universidad:** Universitat Oberta de Catalunya (UOC)
- **Autor:** Saúl M.P.
- **Tutor:** Gregorio R.M.
