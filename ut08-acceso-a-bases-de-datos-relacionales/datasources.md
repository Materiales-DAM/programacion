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

# Datasources

`javax.sql.DataSource` es la interfaz estándar para **obtener conexiones JDBC** sin usar directamente `DriverManager`. Sus ventajas:

* Centraliza la **configuración** (URL, credenciales, timeouts).
* Permite **pools de conexiones** (reutilización eficiente en producción).
* Se puede publicar en **JNDI** (app server) para separar código y credenciales.
* Facilita **transacciones** y ajustes como `readOnly`, `autoCommit`, etc.

### Java SE con el `DataSource` del driver <a href="#java-se-con-el-datasource-del-driver" id="java-se-con-el-datasource-del-driver"></a>

Ejemplo con MySQL o PostgreSQL (útil para scripts o apps pequeñitas).

```java
import com.mysql.cj.jdbc.MysqlDataSource;
import javax.sql.DataSource;
import java.sql.*;

public class SimpleDataSourceExample {
    public static DataSource mysqlDataSource() {
        MysqlDataSource ds = new MysqlDataSource();
        ds.setURL("jdbc:mysql://localhost:3306/mydb?useSSL=false");
        ds.setUser("user");
        ds.setPassword("pass");
        return ds;
    }

    public static void main(String[] args) throws Exception {
        DataSource ds = mysqlDataSource();
        try (Connection con = ds.getConnection();
             PreparedStatement ps = con.prepareStatement("SELECT 1");
             ResultSet rs = ps.executeQuery()) {
            if (rs.next()) System.out.println("OK -> " + rs.getInt(1));
        }
    }
}
```

**Cuándo usarlo:** entornos de prueba o herramientas. **En producción:** mejor un pool.

### Java SE con **pool de conexiones** (recomendado) <a href="#java-se-con-pool-de-conexiones-recomendado" id="java-se-con-pool-de-conexiones-recomendado"></a>

Un pool de conexiones es un **conjunto de conexiones a la base de datos ya abiertas y reutilizables** que una aplicación **“toma prestadas”** cuando las necesita y **devuelve** cuando termina (en lugar de abrir/cerrar una conexión nueva cada vez). Lo gestiona un componente (p. ej., un `DataSource` con HikariCP) que:

* Crea conexiones iniciales y mantiene un mínimo de ellas listas.
* Entrega una conexión libre cuando la pides.
* Si no hay libres, **espera** o **crea más** hasta un máximo configurado.
* Valida, renueva y cierra las conexiones viejas o inactivas.

> Es como una flota de taxis: no compras un coche cada vez que quieres moverte; usas uno, lo devuelves y otro cliente lo reutiliza.

#### ¿Por qué es importante? <a href="#por-que-es-importante" id="por-que-es-importante"></a>

1. **Rendimiento (latencia menor)**

* Abrir una conexión implica TCP + (TLS) + autenticación + negociación. Hacerlo por cada consulta añade decenas/centenas de ms.
* Con un pool, tomas una conexión ya lista ⇒ **tiempos de respuesta más bajos y estables (p95/p99)**.

1. **Escalabilidad y control de recursos**

* Las BBDD tienen un **límite** de conexiones concurrentes.
* El pool actúa como **válvula**: limita cuántas conexiones puede usar tu app y evita saturar la base de datos.

1. **Estabilidad y resiliencia**

* Health-checks/validación evitan usar conexiones rotas.
* **Backpressure**: si el pool está lleno, la app espera o falla rápido; mejor eso que tumbar la BBDD.
* Detección de **fugas** (conexiones no cerradas) y rotación de conexiones antiguas.

1. **Configuración centralizada y seguridad**

* URL, credenciales, timeouts y políticas en un solo sitio (JNDI/secret manager), no dispersos por el código.

<figure><img src="https://fp-informatica.gitbook.io/acceso-a-datos/~gitbook/image?url=https%3A%2F%2F2165140154-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fz960MwFGHtc3ewEBRynf%252Fuploads%252FHmTAaDo9rEsZDiNIGMvn%252Fimage.png%3Falt%3Dmedia%26token%3Dac22b4c6-dc14-4e4a-9cee-0c3beedb92f7&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=4f8be368&#x26;sv=2" alt=""><figcaption></figcaption></figure>

#### Pool de conexiones Hikari <a href="#pool-de-conexiones-hikari" id="pool-de-conexiones-hikari"></a>

**Dependencias Maven**

```xml
<dependency>
  <groupId>com.zaxxer</groupId>
  <artifactId>HikariCP</artifactId>
  <version>5.1.0</version>
</dependency>
```

**Configuraciones principales**

PropiedadDescripciónValor por defectoNotas clave

**Configuraciones principales**

Comment on block

| Propiedad                      | Descripción                                                  | Valor por defecto                          | Notas clave                                                                                     |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| `jdbcUrl`Add comment           | URL JDBC (modo DriverManager).Add comment                    | —Add comment                               | Si usas `jdbcUrl`, normalmente no necesitas `driverClassName`.Add comment                       |
| `username`Add comment          | Usuario por defecto.Add comment                              | —Add comment                               | También posible vía `dataSource.user`.Add comment                                               |
| `password`Add comment          | Password por defecto.Add comment                             | —Add comment                               | También posible vía `dataSource.password`.Add comment                                           |
| `maximumPoolSize`Add comment   | Total máx. (en uso + ociosas).Add comment                    | `10`Add comment                            | Controla la concurrencia real de tu app.Add comment                                             |
| `connectionTimeout`Add comment | Máximo a esperar una conexión libre.Add comment              | `30000`Add comment                         | Mínimo 250; al superar, lanza `SQLException`.Add comment                                        |
| `minimumIdle`Add comment       | Mínimo de conexiones ociosas.Add comment                     | = `maximumPoolSize` (implícito)Add comment | Si no lo fijas, el pool actúa como tamaño fijo.Add comment                                      |
| `idleTimeout`Add comment       | Inactividad antes de retirar una conexión ociosa.Add comment | `600000`Add comment                        | Solo aplica si `minimumIdle < maximumPoolSize`; `0` = nunca retirar por inactividad.Add comment |
| `autoCommit`Add comment        | Auto-commit al devolver la conexión.Add comment              | `true`Add comment                          | Ajusta según tu manejo de transacciones.Add comment                                             |

```java
// HikariDataSourceExample.java
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;
import javax.sql.DataSource;
import java.sql.*;

public class HikariDataSourceExample {
    static DataSource dataSource() {
        HikariConfig cfg = new HikariConfig();
        cfg.setJdbcUrl("jdbc:mysql://localhost:3306/mydb?useSSL=false");
        cfg.setUsername("user");
        cfg.setPassword("pass");

        // Ajustes típicos
        cfg.setMaximumPoolSize(10);        // tamaño del pool
        cfg.setMinimumIdle(2);
        cfg.setConnectionTimeout(10_000);  // ms para esperar una conexión libre
        cfg.setIdleTimeout(60_000);         // ms antes de cerrar inactivas
        // Hikari usa JDBC4 isValid(); no pongas connectionTestQuery salvo que el driver no lo soporte

        return new HikariDataSource(cfg);
    }

    public static void main(String[] args) throws Exception {
        try (Connection con = dataSource().getConnection();
             PreparedStatement ps = con.prepareStatement("SELECT NOW()");
             ResultSet rs = ps.executeQuery()) {
            if (rs.next()) System.out.println("DB time -> " + rs.getString(1));
        }
    }
}
```

**Buenas prácticas de pool:**

* Dimensiona `maximumPoolSize` según **concurrencia real** (p. ej. núm. de hilos de trabajo).
* Pon **timeouts** (conexión, socket).
* Usa `setReadOnly(true)` cuando proceda; gestiona `autoCommit` y `commit/rollback`.
* Mantén credenciales en **variables de entorno** o un gestor de secretos.
