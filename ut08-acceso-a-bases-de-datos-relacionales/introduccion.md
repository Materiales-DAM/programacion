---
cover: ../.gitbook/assets/jdbc.jpeg
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Introducción

Vamos a estudiar cómo acceder a una base de datos relacional (MySQL) desde Java. La librería que vamos a usar para ello se denomina JDBC (Java Database Connectivity) y está integrada en el JDK de Java.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

#### Capas y roles <a href="#capas-y-roles" id="capas-y-roles"></a>

* **Aplicación Java**: tu código llama a la API (`Connection`, `PreparedStatement`, `ResultSet`, …).
* **API JDBC (java.sql / javax.sql)**: contratos estándar.
  * `java.sql`: uso básico (conexión, sentencias, resultados, metadatos, transacciones).
  * `javax.sql`: fuentes de datos, _connection pooling_, XA (transacciones distribuidas).
* **DriverManager / DataSource**:
  * **DriverManager**: obtiene conexiones a partir de una URL JDBC; más simple, sin _pool_.
  * **DataSource**: fábrica de conexiones; permite **pooling** (HikariCP, etc.), JNDI y config centralizada. Es lo recomendado en producción.
* **Driver JDBC** (normalmente **Type 4**, puro Java): implementa la **SPI** de JDBC y traduce llamadas de la API a un protocolo de red propio del motor.
* **Base de datos**: ejecuta el SQL y devuelve filas/estados.

#### Flujo típico de una petición <a href="#flujo-tipico-de-una-peticion" id="flujo-tipico-de-una-peticion"></a>

1. Tu app pide una conexión → `DataSource.getConnection()` (o `DriverManager.getConnection()`).
2. Se crea (o saca del pool) un **`Connection`**.
3. Preparas la consulta → **`PreparedStatement`** (parámetros, plan reusable).
4. Ejecutas → `executeQuery()` / `executeUpdate()` / `execute()`.
5. Lees resultados → **`ResultSet`** (cursor, tipos, _fetch size_, _streaming_).
6. Confirmas o deshaces → **transacciones** (`commit`/`rollback`), `autoCommit` on/off.
7. Cierras recursos (o los devuelve al pool) → `ResultSet` → `Statement` → `Connection`.
