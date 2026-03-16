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

# Data Access Objects

Data Access Object (DAO) es un patrón de diseño que **aísla el acceso a datos** (SQL, archivos, APIs, etc.) del resto de la aplicación. La lógica de negocio no “sabe” cómo se persisten las cosas; solo habla con objetos DAO a través de **interfaces**.

En muchos casos, cada DAO se corresponden con una tabla de la base de datos, lo que permite una forma más directa de enviar y recuperar datos del almacenamiento y oculta las consultas engorrosas.

#### Objetivos <a href="#objetivos" id="objetivos"></a>

* **Separación de responsabilidades:** negocio ↔ persistencia.
* **Intercambiabilidad:** cambiar MySQL por PostgreSQL (o JDBC por JPA) sin tocar la capa de negocio.
* **Testeabilidad:** mockear DAOs en tests unitarios.
* **Consistencia:** centralizar SQL, mapping y manejo de errores/transacciones.

#### Componentes <a href="#componentes" id="componentes"></a>

* **Entidad**: p.ej., `Product`.
* **Interfaz DAO**: contrato, p.ej., `ProductDao`.
* **Implementación DAO**: p.ej., `JdbcProductDao`, `JpaProductDao`.

#### Ejemplo <a href="#ejemplo" id="ejemplo"></a>

**POJO**

```java
@Data
@AllArgsConstructor
public class Product {
  private Long id;
  private String name;
  private double price;

}
```

**Interface**

```java

public interface ProductDao {
  Product findById(Long id);
  List<Product> findAll();
  Long save(Product p);
  void update(Product p);
  void deleteById(Long id);
}
```

**Implementación**

```java
import javax.sql.DataSource;
import java.sql.*;
import java.util.*;

public class JdbcProductDao implements ProductDao {
  private final DataSource ds;

  public JdbcProductDao(DataSource ds) { 
    this.ds = ds; 
  }

  @Override
  public Product findById(Long id) {
    String sql = "SELECT id, name, price FROM product WHERE id = ?";
    try (Connection con = ds.getConnection();
         PreparedStatement ps = con.prepareStatement(sql)) {
      ps.setLong(1, id);
      try (ResultSet rs = ps.executeQuery()) {
        if (rs.next()) {
          Product p = mapRow(rs);
          return p;
        }
        return null;
      }
    } catch (SQLException e) {
      throw new RuntimeException("DB error in findById", e);
    }
  }

  @Override
  public List<Product> findAll() {
    String sql = "SELECT id, name, price FROM product";
    List<Product> out = new ArrayList<>();
    try (Connection con = ds.getConnection();
         PreparedStatement ps = con.prepareStatement(sql);
         ResultSet rs = ps.executeQuery()) {
      while (rs.next()) out.add(mapRow(rs));
      return out;
    } catch (SQLException e) {
      throw new RuntimeException("DB error in findAll", e);
    }
  }

  @Override
  public Long save(Product p) {
    String sql = "INSERT INTO product(name, price) VALUES(?, ?)";
    try (Connection con = ds.getConnection();
         PreparedStatement ps = con.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS)) {
      ps.setString(1, p.getName());
      ps.setDouble(2, p.getPrice());
      ps.executeUpdate();
      try (ResultSet keys = ps.getGeneratedKeys()) {
        if (keys.next()) return keys.getLong(1);
        throw new RuntimeException("No generated key returned");
      }
    } catch (SQLException e) {
      throw new RuntimeException("DB error in save", e);
    }
  }

  @Override
  public void update(Product p) {
    String sql = "UPDATE product SET name=?, price=? WHERE id=?";
    try (Connection con = ds.getConnection();
         PreparedStatement ps = con.prepareStatement(sql)) {
      ps.setString(1, p.getName());
      ps.setDouble(2, p.getPrice());
      ps.setLong(3, p.getId());
      ps.executeUpdate();
    } catch (SQLException e) {
      throw new RuntimeException("DB error in update", e);
    }
  }

  @Override
  public void deleteById(Long id) {
    String sql = "DELETE FROM product WHERE id=?";
    try (Connection con = ds.getConnection();
         PreparedStatement ps = con.prepareStatement(sql)) {
      ps.setLong(1, id);
      ps.executeUpdate();
    } catch (SQLException e) {
      throw new RuntimeException("DB error in deleteById", e);
    }
  }

  private Product mapRow(ResultSet rs) throws SQLException {
    Product p = new Product();
    p.setId(rs.getLong("id"));
    p.setName(rs.getString("name"));
    p.setPrice(rs.getDouble("price"));
    return p;
  }
}
```
