# Primer programa en Swing

### El "Hola Mundo" de Swing

Crea un fichero `HolaSwing.java` con el siguiente contenido:

```java
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.SwingUtilities;

public class HolaSwing {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            JFrame ventana = new JFrame("Hola Swing");
            ventana.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            ventana.setSize(400, 200);
            ventana.add(new JLabel("¡Hola, mundo!", JLabel.CENTER));
            ventana.setLocationRelativeTo(null); // centrar en pantalla
            ventana.setVisible(true);
        });
    }
}
```

Compílalo y ejecútalo:

```bash
javac HolaSwing.java
java HolaSwing
```

O directamente, sin compilar (Java 11+):

```bash
java HolaSwing.java
```

Deberías ver una ventana de 400×200 con el texto centrado.

### Análisis línea por línea

#### Los `import`

```java
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.SwingUtilities;
```

Las clases de Swing viven en `javax.swing.*` (con `x` de "extension", herencia histórica). Las de utilería para gráficos básicos están en `java.awt.*`.

#### `SwingUtilities.invokeLater`

```java
SwingUtilities.invokeLater(() -> { ... });
```

Esto delega la creación de la ventana al **EDT** (Event Dispatch Thread). El método `main` se ejecuta en el hilo principal, pero los componentes Swing se deben crear y modificar **únicamente** en el EDT. Es el patrón estándar y tienes que escribirlo siempre, aunque al principio lo veas como ceremonia inútil.

`invokeLater` recibe un `Runnable`, y como `Runnable` es una interfaz funcional (un único método `run()`), podemos pasarle una **expresión lambda**.

#### `JFrame`: la ventana

```java
JFrame ventana = new JFrame("Hola Swing");
```

`JFrame` es la ventana principal de una aplicación Swing. El argumento del constructor es el título que aparece en la barra superior. Una `JFrame` es ya un contenedor: puedes añadirle componentes con `add(...)`.

#### `setDefaultCloseOperation`

```java
ventana.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```

Indica qué hacer cuando el usuario pulsa la "X". Las opciones son:

| Constante                        | Comportamiento                                            |
| -------------------------------- | --------------------------------------------------------- |
| `JFrame.EXIT_ON_CLOSE`           | Termina toda la JVM. Útil para apps con una sola ventana. |
| `JFrame.DISPOSE_ON_CLOSE`        | Cierra solo esta ventana, libera sus recursos.            |
| `JFrame.HIDE_ON_CLOSE` (default) | La oculta pero la deja en memoria.                        |
| `JFrame.DO_NOTHING_ON_CLOSE`     | No hace nada (útil si quieres mostrar un "¿Seguro?").     |

**Aviso**: si te olvidas de poner `EXIT_ON_CLOSE` en una app pequeña, al cerrar la ventana el proceso Java sigue vivo y tendrás que matarlo desde la consola.

#### `setSize` y `setLocationRelativeTo`

```java
ventana.setSize(400, 200);
ventana.setLocationRelativeTo(null);
```

`setSize(ancho, alto)` define el tamaño en píxeles. `setLocationRelativeTo(null)` centra la ventana en la pantalla. Si pasas otro componente como argumento, se centra respecto a él (útil para diálogos modales).

#### `add` y `setVisible`

```java
ventana.add(new JLabel("¡Hola, mundo!", JLabel.CENTER));
ventana.setVisible(true);
```

Añadimos un `JLabel` (texto estático) al área de contenido del frame. La constante `JLabel.CENTER` alinea el texto horizontalmente.

`setVisible(true)` debe ser **lo último** que hagas en la construcción de la ventana, una vez que ya están todos los componentes añadidos. Si lo llamas antes, los componentes que añadas después puede que no se vean hasta que ocurra un repintado.

### Variante: clase que extiende `JFrame`

Otra forma común es heredar de `JFrame`. Es opcional, pero ordena el código cuando crece:

```java
import javax.swing.*;

public class VentanaPrincipal extends JFrame {

    public VentanaPrincipal() {
        super("Hola Swing (versión OOP)");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setSize(400, 200);
        add(new JLabel("¡Hola desde una subclase!", JLabel.CENTER));
        setLocationRelativeTo(null);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new VentanaPrincipal().setVisible(true));
    }
}
```

Ventajas:

* El código de construcción queda dentro del constructor, no en `main`.
* Puedes sobrescribir métodos de `JFrame` si lo necesitas.
* Más natural para añadir métodos auxiliares (`crearMenu()`, `cargarDatos()`…).

A partir de aquí usaremos este estilo en muchos ejemplos.

### Look and Feel: que no parezca de los 90

Por defecto Swing usa el "Metal Look and Feel", que se ve bastante datado. Puedes cambiarlo al aspecto del sistema operativo con una línea:

```java
public static void main(String[] args) {
    try {
        UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
    } catch (Exception ignored) { }
    SwingUtilities.invokeLater(() -> new VentanaPrincipal().setVisible(true));
}
```

Esto hará que en Windows tenga aspecto Windows, en macOS aspecto macOS y en Linux GTK. Si quieres algo más moderno, mira **FlatLaf** (es un `.jar` externo, pero con resultados muy elegantes).

### Errores frecuentes en el primer programa

1. **Olvidar `setVisible(true)`**: la ventana existe pero no se muestra.
2. **`setVisible(true)` antes de añadir componentes**: aparecen tarde o no se ven.
3. **No usar `invokeLater`**: funciona "casi siempre" pero da bugs raros con ratón o repintados.
4. **`setSize` no funciona**: si la ventana usa `pack()` o un layout que ignora el tamaño preferido.

### Ejercicio

1. Modifica el "Hola Mundo" para que el texto del `JLabel` muestre la fecha actual usando `LocalDate.now()`.
2. Cambia el tamaño a 500×300.
3. Aplica el Look and Feel del sistema.
4. Sustituye `setSize` por `pack()` y observa qué cambia (la ventana se ajusta al tamaño preferido del contenido).
