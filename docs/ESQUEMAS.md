# Esquemas de Modelo y Base de Datos

Este documento resume visualmente la estructura principal de la solucion backend: modelo funcional y esquema relacional.

## 1. Modelo de dominio

```mermaid
classDiagram
    class Persona {
        +Long id
        +String nombre
        +String genero
        +Integer edad
        +String identificacion
        +String direccion
        +String telefono
    }

    class Cliente {
        +String clienteId
        +String contrasena
        +boolean estado
    }

    class Cuenta {
        +Long id
        +String numeroCuenta
        +TipoCuenta tipo
        +BigDecimal saldoInicial
        +BigDecimal saldoDisponible
        +boolean estado
        +Long clienteId
    }

    class Movimiento {
        +Long id
        +LocalDate fecha
        +TipoMovimiento tipo
        +BigDecimal valor
        +BigDecimal saldo
        +Long cuentaId
    }

    class TipoCuenta {
        <<enumeration>>
        AHORRO
        CORRIENTE
    }

    class TipoMovimiento {
        <<enumeration>>
        DEPOSITO
        RETIRO
    }

    Persona <|-- Cliente
    Cliente "1" --> "*" Cuenta
    Cuenta "1" --> "*" Movimiento
    Cuenta --> TipoCuenta
    Movimiento --> TipoMovimiento
```

## 2. Esquema relacional de base de datos

```mermaid
erDiagram
    CLIENTES {
        BIGINT id PK
        VARCHAR nombre
        VARCHAR genero
        INTEGER edad
        VARCHAR identificacion UK
        VARCHAR direccion
        VARCHAR telefono
        TIMESTAMP created_at
        TIMESTAMP updated_at
        VARCHAR cliente_id UK
        VARCHAR contrasena
        BOOLEAN estado
    }

    CUENTAS {
        BIGINT id PK
        VARCHAR numero_cuenta UK
        VARCHAR tipo
        NUMERIC saldo_inicial
        NUMERIC saldo_disponible
        BOOLEAN estado
        BIGINT cliente_id FK
    }

    MOVIMIENTOS {
        BIGINT id PK
        DATE fecha
        VARCHAR tipo
        NUMERIC valor
        NUMERIC saldo
        BIGINT cuenta_id FK
    }

    CLIENTES ||--o{ CUENTAS : posee
    CUENTAS ||--o{ MOVIMIENTOS : registra
```

## 3. Script SQL principal

El esquema relacional entregado oficialmente para la prueba se encuentra en:

- [BaseDatos.sql](</C:/Users/naren/OneDrive/Desktop/Naren Unicauca/CHAMBA/PruebaTecnicaDevsuNimbachi/banco-app/BaseDatos.sql>)

Ese archivo contiene:

- creacion de tablas
- claves primarias
- claves foraneas
- restricciones
- indices
- datos semilla de ejemplo

## 4. Correspondencia entre codigo y base de datos

Relaciones implementadas en el proyecto:

- `ClienteEntity` se mapea a la tabla `clientes`
- `CuentaEntity` se mapea a la tabla `cuentas`
- `MovimientoEntity` se mapea a la tabla `movimientos`
- `PersonaEntity` es una superclase mapeada con `@MappedSuperclass`

Relaciones JPA principales:

- un cliente tiene muchas cuentas
- una cuenta pertenece a un cliente
- una cuenta tiene muchos movimientos
- un movimiento pertenece a una cuenta

## 5. Observacion sobre el script SQL

Aunque el proyecto usa JPA e Hibernate, el archivo `BaseDatos.sql` se incluye porque:

- el enunciado lo pide expresamente
- deja un esquema reproducible e independiente del auto-DDL
- facilita validar la solucion en otro computador
- muestra de forma explicita las restricciones de la base de datos
