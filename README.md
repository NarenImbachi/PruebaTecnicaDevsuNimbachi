# Prueba Tecnica Full-Stack BP

Repositorio unico de la solucion full-stack para la prueba tecnica bancaria, compuesto por:

- backend en Spring Boot
- frontend en Angular
- base de datos PostgreSQL
- orquestacion con Docker Compose

## Objetivo de la solucion

La aplicacion permite gestionar:

- clientes
- cuentas
- movimientos
- reportes de estado de cuenta

Tambien implementa reglas de negocio solicitadas en el enunciado, como validacion de saldo disponible, limite diario de retiro y generacion de reporte por cliente y rango de fechas.

## Tecnologias usadas

### Backend

- Java 17
- Spring Boot 3.5.13
- Spring Data JPA
- PostgreSQL
- MapStruct
- JUnit 5
- Mockito

### Frontend

- Angular 19.2
- TypeScript
- SCSS
- Jest
- jsPDF

### Infraestructura

- Docker
- Docker Compose

## Estructura del repositorio

```text
PruebaTecnicaDevsuNimbachi/
|-- banco-app/           # Backend Spring Boot
|-- banco-frontend/      # Frontend Angular
|-- docs/                # Coleccion Postman
|-- docker-compose.yaml  # Ejecucion conjunta
`-- README.md
```

## Modulos principales

### Backend

Ubicado en [banco-app](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-app>).

Incluye:

- API REST para clientes, cuentas, movimientos y reportes
- persistencia con JPA
- validaciones y manejo global de excepciones
- pruebas unitarias y pruebas de controladores
- `BaseDatos.sql` como script de base de datos solicitado

Documentacion especifica:

- [README backend](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-app/README.md>)
- [Endpoints backend](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-app/ENDPOINTS.md>)

### Frontend

Ubicado en [banco-frontend](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-frontend>).

Incluye:

- vistas para clientes, cuentas, movimientos y reportes
- formularios reactivos con validaciones
- busqueda rapida en listados
- generacion de PDF desde reportes
- pruebas unitarias con Jest

Documentacion especifica:

- [README frontend](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-frontend/README.md>)

## Ejecucion

La forma principal de ejecutar la solucion es levantar todo con Docker Compose desde la raiz del repositorio:

```bash
docker compose up --build -d
```

Este modo deja los contenedores ejecutandose en segundo plano y facilita revisar logs desde Docker Desktop o con comandos como:

```bash
docker compose logs -f
```

Servicios expuestos:

- frontend: `http://localhost:4200`
- backend: `http://localhost:8080`
- base de datos: `localhost:5432`

Credenciales por defecto de PostgreSQL:

- base de datos: `banco_db`
- usuario: `postgres`
- contrasena: `root`

## Flujo de uso

1. Ejecutar `docker compose up --build -d` desde la raiz.
2. Abrir `http://localhost:4200`.
3. Validar CRUD de clientes.
4. Validar CRUD de cuentas.
5. Registrar movimientos de deposito y retiro.
6. Generar reporte por cliente y rango de fechas.
7. Descargar el PDF desde la vista de reportes.

## Endpoints principales del backend

- `POST /api/clientes`
- `GET /api/clientes`
- `PUT /api/clientes/{id}`
- `DELETE /api/clientes/{id}`
- `POST /api/cuentas`
- `GET /api/cuentas`
- `PUT /api/cuentas/{id}`
- `DELETE /api/cuentas/{id}`
- `POST /api/movimientos`
- `GET /api/movimientos/listado`
- `DELETE /api/movimientos/{id}`
- `GET /api/reportes/estado-cuenta`

El detalle funcional y ejemplos de request/response estan en:

- [banco-app/ENDPOINTS.md](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-app/ENDPOINTS.md>)

## Reglas de negocio implementadas

- los depositos manejan valores positivos
- los retiros manejan valores negativos
- cada movimiento almacena el saldo resultante
- si no hay saldo suficiente, se retorna `Saldo no disponible`
- el limite diario de retiro por cuenta es `1000`
- si se supera ese limite, se retorna `Cupo diario Excedido`
- el reporte de estado de cuenta se genera por cliente y rango de fechas

## Base de datos

La solucion usa PostgreSQL con base de datos `banco_db`.

Script principal entregado:

- [BaseDatos.sql backend](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-app/BaseDatos.sql>)

## Pruebas

### Backend

Desde `banco-app`:

```bash
./mvnw test
```

En Windows:

```powershell
.\mvnw.cmd test
```

### Frontend

Desde `banco-frontend`:

```bash
npm test
```

## Coleccion Postman

- [Coleccion Postman](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/docs/API_COLLECTION.postman_collection.json>)

## Esquemas visuales

- [Esquemas de modelo y base de datos](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/docs/ESQUEMAS.md>)

## Contenido del repositorio

Este repositorio incluye:

- codigo fuente backend
- codigo fuente frontend
- script de base de datos
- despliegue con Docker
- pruebas automatizadas
- coleccion Postman para validacion de endpoints
