# Introducción

Vamos a estudiar cómo acceder a una base de datos relacional (MySQL) desde Java. La librería que vamos a usar para ello se denomina JDBC (Java Database Connectivity) y está integrada en el JDK de Java.

## **Configuración  Maven**

Para **MySQL** (similar para PostgreSQL):

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

## **Abrir una conexión**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseConnection {
    private static final String URL = "jdbc:mysql://localhost:3306/your_database";
    private static final String USER = "your_user";
    private static final String PASSWORD = "your_password";

    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}
```

## **Leer datos de la base de datos**

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

public class SelectExample {
    public static void main(String[] args) {
        try (Connection conn = DatabaseConnection.getConnection()) {
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT id, name FROM users")
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                System.out.println(id + " - " + name);
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## **Insertar datos en una tabla**

```java
import java.sql.Connection;
import java.sql.PreparedStatement;

public class InsertExample {
    public static void main(String[] args) {
        String sql = "INSERT INTO users (name, email) VALUES (?, ?)";

        try (Connection conn = DatabaseConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setString(1, "John Doe");
            pstmt.setString(2, "john@example.com");

            int rows = pstmt.executeUpdate();
            System.out.println("Inserted " + rows + " row(s)");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## **Actualizar datos de una tabla**

```java
import java.sql.Connection;
import java.sql.PreparedStatement;

public class UpdateExample {
    public static void main(String[] args) {
        String sql = "UPDATE users SET email = ? WHERE id = ?";

        try (Connection conn = DatabaseConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setString(1, "newemail@example.com");
            pstmt.setInt(2, 1);

            int rows = pstmt.executeUpdate();
            System.out.println("Updated " + rows + " row(s)");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## **Eliminar filas de una tabla**

```java
import java.sql.Connection;
import java.sql.PreparedStatement;

public class DeleteExample {
    public static void main(String[] args) {
        String sql = "DELETE FROM users WHERE id = ?";

        try (Connection conn = DatabaseConnection.getConnection();
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setInt(1, 1);

            int rows = pstmt.executeUpdate();
            System.out.println("Deleted " + rows + " row(s)");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## **Buenas Prácticas**

✅ Siempre usa **PreparedStatement** (evita SQL Injection).\
✅ Usa **try-with-resources** para cerrar conexiones.\
✅ Considera un **pool de conexiones** (HikariCP) en aplicaciones reales.\
✅ Para aplicaciones complejas: evalúa usar **JPA (Hibernate, Spring Data JPA)**.
