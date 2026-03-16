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

# API JDBC

La forma más básica (que no la más simple) para acceder a bases de datos relacionales es a través del uso de al API incluida en el JDK.

### Componentes <a href="#componentes" id="componentes"></a>

* **DriverManager**: Encargado de cargar el driver de la base de datos.
* **DataSource**: representa una fuente de datos concreta, por ejemplo la base de datos MySQL, disponible en la url jdbc:mysql://192.168.1.10:3306/mydatabase, y con unas credenciales dadas.
* **Connection**: Representa una conexión a un DataSource, las conexiones permiten ejecutar sentencias SQL sobre la base de datos. Cada hilo que acceda a la base de datos debe usar su propia conexión.
* **Statement**: Permite ejecutar sentencias SQL en la base de datos.
* **PreparedStatement**: Permite ejecutar sentencia precompiladas.
* **ResultSet**: son iteradores que permiten extraer la información resultante de una consulta SQL.

### Ejemplo de acceso a datos de una tienda <a href="#ejemplo-de-acceso-a-datos-de-una-tienda" id="ejemplo-de-acceso-a-datos-de-una-tienda"></a>

#### Crear el contenedor en Docker <a href="#crear-el-contenedor-en-docker" id="crear-el-contenedor-en-docker"></a>

```bash
docker container rm -f diurno-mysql
docker volume prune
docker run --name diurno-mysql -e MYSQL_ROOT_PASSWORD=Sandia4you -p 3306:3306 -d proxy-docker.tierno.es:5000/library/mysql:8.1 mysqld --default-authentication-plugin=mysql_native_password --bind-address=0.0.0.0
```

#### Crear base de datos MySQL <a href="#crear-base-de-datos-mysql" id="crear-base-de-datos-mysql"></a>

Lo primero sería definir una base de datos

```sql
DROP DATABASE IF EXISTS shop;
CREATE DATABASE shop CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
USE shop;

CREATE TABLE product (
  id         BIGINT UNSIGNED NOT NULL AUTO_INCREMENT,
  name       VARCHAR(200)    NOT NULL,
  price      DECIMAL(10,2)   NOT NULL,
  active     TINYINT(1)      NOT NULL DEFAULT 1,

  PRIMARY KEY (id),
  INDEX idx_product_active_price (active, price),
  INDEX idx_product_name (name),
  CHECK (price >= 0)
) ENGINE=InnoDB;

INSERT INTO product (name, price, active) VALUES
  ('USB-C Cable 1m',              9.90,   1),
  ('Wireless Mouse',             19.99,   1),
  ('Mechanical Keyboard',        79.00,   1),
  ('27-inch Monitor',           189.00,   1),
  ('Laptop Stand',               25.50,   1),
  ('Noise-Cancelling Headset',  129.99,   0),
  ('Webcam 1080p',               39.95,   1),
  ('Desk Lamp LED',              15.00,   1),
  ('HDMI 2.1 Cable 2m',          12.49,   1),
  ('Portable SSD 1TB',          109.00,   0);
```

Para poder conectarnos a MySQL necesitamos cargar el driver como dependencia del proyecto

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

Después creamos el modelo en Java (POJO)

```java
package org.ies.tierno.jdbc.model;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    private Long id;
    private String name;
    private double price;
    private Boolean active;
}
```

#### Leyendo productos <a href="#leyendo-productos" id="leyendo-productos"></a>

Ahora ya podemos ejecutar consultas SELECT y cargar los datos de la tabla en la memoria del programa:

```java
package org.ies.tierno.jdbc;

import lombok.extern.log4j.Log4j;
import org.ies.tierno.jdbc.model.Product;

import java.math.BigDecimal;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

@Log4j
public class JdbcSelectDemo {

    private static final String URL  = "jdbc:mysql://localhost:3306/shop";
    private static final String USER = "root";
    private static final String PASS = "Sandia4you";

    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection(URL, USER, PASS)) {

            String sql = "SELECT id, name, price, active FROM product WHERE active = ? AND price >= ?";
            List<Product> products = new ArrayList<>();

            try (PreparedStatement ps = conn.prepareStatement(sql)) {
                ps.setBoolean(1, true);
                ps.setBigDecimal(2, new BigDecimal("10.00"));

                try (ResultSet rs = ps.executeQuery()) {
                    while (rs.next()) {
                        // Map each row to Product (no builder)
                        Product p = new Product(
                                rs.getLong("id"),
                                rs.getString("name"),
                                rs.getDouble("price"),
                                rs.getBoolean("active")
                        );
                        products.add(p);
                    }
                }
            }

            for(var product: products) {
                log.info(product);
            }
        } catch (SQLException e) {
            log.error("Error el ejecutar la query", e);
        }
    }
}

```

#### Insertar un producto <a href="#insertar-un-producto" id="insertar-un-producto"></a>

Ahora vamos a ver cómo insertar un producto en la base de datos a partir de los datos que nos da el usuario.

```java
package org.ies.tierno.jdbc;

import lombok.extern.log4j.Log4j;
import org.ies.tierno.jdbc.model.Product;

import java.sql.*;
import java.util.Scanner;

@Log4j
public class JdbcInsertDemo {

    private static final String URL = "jdbc:mysql://localhost:3306/shop?useSSL=false";
    private static final String USER = "root";
    private static final String PASS = "Sandia4you";

    public static void main(String[] args) {
        try (
                Scanner sc = new Scanner(System.in);
                Connection conn = DriverManager.getConnection(URL, USER, PASS)
        ) {

            log.info("=== Insert a new product ===");

            log.info("Name: ");
            String name = sc.nextLine().trim();

            double price = readPrice(sc);
            Boolean active = readActive(sc);

            Product p = new Product(null, name, price, active);
            long newId = insertProduct(conn, p);

            log.info("Product inserted with ID: " + newId);

        } catch (SQLException e) {
            log.error("SQL error: " + e.getMessage(), e);
        }
    }

    private static double readPrice(Scanner sc) {
        double price = -1;
        do {
            log.info("Price: ");
            try {
                price = sc.nextDouble();
            } catch (NumberFormatException ex) {
                log.info("Invalid number. Try again.");
            } finally {
                sc.nextLine();
            }
        } while (price <= 0);
        return price;
    }

    private static Boolean readActive(Scanner sc) {
        Boolean active = null;
        do {
            log.info("Active? (y/n): ");
            String raw = sc.nextLine().trim().toLowerCase();
            if (raw.equals("y") || raw.equals("yes"))
                active = true;

            if (raw.equals("n") || raw.equals("no"))
                active = false;
            log.info("Please answer y/n.");
        } while (active == null);
        return active;
    }

    private static long insertProduct(Connection conn, Product p) throws SQLException {
        String sql = "INSERT INTO product(name, price, active) VALUES (?, ?, ?)";
        try (PreparedStatement ps = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS)) {
            ps.setString(1, p.getName());
            ps.setDouble(2, p.getPrice());
            ps.setBoolean(3, p.getActive());

            int updated = ps.executeUpdate();
            if (updated != 1) {
                throw new SQLException("Unexpected affected rows: " + updated);
            }

            try (ResultSet keys = ps.getGeneratedKeys()) {
                keys.next();
                return keys.getLong(1);
            }
        }
    }
}
```

[<br>](https://fp-informatica.gitbook.io/acceso-a-datos/ut02-jdbc/modelo-de-datos)
