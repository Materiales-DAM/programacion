# Contenedores y paneles

Hasta ahora hemos usado `JFrame` como contenedor y `JPanel` para agrupar componentes. En este capítulo vemos otros contenedores que aparecen una y otra vez en aplicaciones reales.

### JPanel: el contenedor genérico

Es la pieza más versátil de Swing: simplemente es un rectángulo donde meter otros componentes con un layout.

```java
JPanel panel = new JPanel();              // FlowLayout por defecto
JPanel cuadrado = new JPanel(new BorderLayout());
panel.setBorder(BorderFactory.createTitledBorder("Datos personales"));
panel.setBackground(new Color(245, 245, 250));
```

Bordes habituales (factoría `BorderFactory`):

* `createEmptyBorder(t, l, b, r)`: márgenes invisibles.
* `createLineBorder(Color)`: línea de un color.
* `createTitledBorder(String)`: borde con título.
* `createEtchedBorder()` / `createBevelBorder(...)`: efecto 3D sutil.
* `createCompoundBorder(b1, b2)`: combinar dos bordes.

Una práctica recomendable: **un panel = una responsabilidad**. Si una pantalla tiene un formulario y una tabla, normalmente cada uno es un `JPanel` independiente.

### JScrollPane: barras de desplazamiento

Muchos componentes (`JTextArea`, `JTable`, `JList`, `JTree`) **no tienen scroll por sí solos**. Hay que envolverlos:

```java
JTextArea area = new JTextArea(10, 40);
JScrollPane scroll = new JScrollPane(area);
panel.add(scroll, BorderLayout.CENTER);
```

Configuración útil:

```java
scroll.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
scroll.setHorizontalScrollBarPolicy(JScrollPane.HORIZONTAL_SCROLLBAR_NEVER);
scroll.getVerticalScrollBar().setUnitIncrement(16); // velocidad de la rueda
```

Las políticas: `AS_NEEDED` (por defecto), `ALWAYS`, `NEVER`.

Si necesitas que un componente que no es nativamente scrollable (`JLabel` con un icono enorme, un panel grande…) tenga scroll, simplemente envuélvelo: `new JScrollPane(panelGrande)`.

### JTabbedPane: pestañas

```java
JTabbedPane pestanas = new JTabbedPane();
pestanas.addTab("General", new JLabel("Pestaña 1"));
pestanas.addTab("Avanzado", new JLabel("Pestaña 2"));
pestanas.addTab("Acerca de", new JLabel("Pestaña 3"));

// Con icono y tooltip:
pestanas.addTab("Datos", new ImageIcon("data.png"), panelDatos, "Información del usuario");

pestanas.setTabPlacement(JTabbedPane.TOP); // TOP, BOTTOM, LEFT, RIGHT
pestanas.setSelectedIndex(0);
```

Cada pestaña es un componente cualquiera; lo normal es que sea un `JPanel` con el contenido. Para reaccionar al cambio de pestaña:

```java
pestanas.addChangeListener(e -> {
    int idx = pestanas.getSelectedIndex();
    System.out.println("Pestaña activa: " + idx);
});
```

### JSplitPane: divisor redimensionable

Dos paneles separados por una barra que el usuario puede arrastrar:

```java
JSplitPane split = new JSplitPane(
    JSplitPane.HORIZONTAL_SPLIT,
    panelIzquierdo,
    panelDerecho
);
split.setDividerLocation(200);     // posición inicial en píxeles
split.setResizeWeight(0.3);         // al redimensionar, 30% al lado izquierdo
split.setOneTouchExpandable(true);  // botoncitos para colapsar
split.setContinuousLayout(true);    // redibujar mientras se arrastra
```

Útil para una explorador-archivos / contenido (típico IDE), o tabla / detalle.

Para un layout de tres zonas (tipo IDE) puedes anidar dos `JSplitPane`.

### JToolBar: barra de herramientas

```java
JToolBar toolbar = new JToolBar("Acciones");
toolbar.add(new JButton(new ImageIcon("new.png")));
toolbar.add(new JButton(new ImageIcon("open.png")));
toolbar.add(new JButton(new ImageIcon("save.png")));
toolbar.addSeparator();
toolbar.add(new JButton(new ImageIcon("cut.png")));
toolbar.add(new JButton(new ImageIcon("copy.png")));
toolbar.add(new JButton(new ImageIcon("paste.png")));
toolbar.setFloatable(true); // el usuario puede arrancarla en una ventana flotante
```

Lo más limpio es asociar cada botón de la `JToolBar` a un objeto `Action` (como vimos en el capítulo anterior), porque así la misma acción aparece en menú y en barra sin duplicar código.

```java
Action guardarAction = ...;
toolbar.add(guardarAction);  // crea el botón con icono y tooltip automáticamente
```

### Box: contenedor con BoxLayout integrado

`Box` es atajo para crear paneles con `BoxLayout`:

```java
Box vertical = Box.createVerticalBox();
vertical.add(new JLabel("Línea 1"));
vertical.add(Box.createVerticalStrut(10));
vertical.add(new JLabel("Línea 2"));

Box horizontal = Box.createHorizontalBox();
horizontal.add(new JButton("Aceptar"));
horizontal.add(Box.createHorizontalGlue());
horizontal.add(new JButton("Cancelar"));
```

Lo último (con el "glue" en medio) deja "Aceptar" pegado a la izquierda y "Cancelar" pegado a la derecha. Patrón habitual para botoneras de diálogo.

### JLayeredPane: capas superpuestas

Para superponer componentes (overlays, badges, dialogos no modales internos):

```java
JLayeredPane capas = new JLayeredPane();
capas.setPreferredSize(new Dimension(400, 300));

JLabel fondo = new JLabel(new ImageIcon("bg.png"));
fondo.setBounds(0, 0, 400, 300);

JButton encima = new JButton("OK");
encima.setBounds(150, 130, 100, 30);

capas.add(fondo, JLayeredPane.DEFAULT_LAYER);
capas.add(encima, JLayeredPane.PALETTE_LAYER);
```

En este contenedor sí se posiciona por coordenadas absolutas (es la excepción a la regla del capítulo 3).

### JDesktopPane y JInternalFrame: MDI

Permiten tener "ventanas dentro de la ventana" (estilo aplicaciones de los 90 con muchos documentos abiertos).

```java
JDesktopPane escritorio = new JDesktopPane();
JInternalFrame interna = new JInternalFrame("Documento 1", true, true, true, true);
interna.setSize(300, 200);
interna.setVisible(true);
escritorio.add(interna);
```

Está algo en desuso (los IDE modernos prefieren pestañas a MDI), pero saber que existe está bien.

### Ejemplo integrador: ventana con cabecera, lateral y contenido

```java
import javax.swing.*;
import java.awt.*;

public class VentanaIDE extends JFrame {

    public VentanaIDE() {
        super("Ejemplo de layout tipo IDE");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        // Toolbar
        var toolbar = new JToolBar();
        toolbar.add(new JButton("Nuevo"));
        toolbar.add(new JButton("Abrir"));
        toolbar.add(new JButton("Guardar"));

        // Lateral izquierdo
        var lista = new JList<>(new String[]{"Inicio.java", "Util.java", "Config.java"});
        var scrollLista = new JScrollPane(lista);
        scrollLista.setBorder(BorderFactory.createTitledBorder("Archivos"));

        // Centro: pestañas con editores
        var pestanas = new JTabbedPane();
        pestanas.addTab("Inicio.java", new JScrollPane(new JTextArea()));
        pestanas.addTab("Util.java", new JScrollPane(new JTextArea()));

        // Splits
        var splitCentral = new JSplitPane(JSplitPane.HORIZONTAL_SPLIT, scrollLista, pestanas);
        splitCentral.setDividerLocation(180);

        // Barra de estado
        var estado = new JLabel(" Listo");
        estado.setBorder(BorderFactory.createLoweredBevelBorder());

        setLayout(new BorderLayout());
        add(toolbar, BorderLayout.NORTH);
        add(splitCentral, BorderLayout.CENTER);
        add(estado, BorderLayout.SOUTH);

        setSize(900, 600);
        setLocationRelativeTo(null);
    }

    public static void main(String[] args) {
        try { UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName()); }
        catch (Exception ignored) {}
        SwingUtilities.invokeLater(() -> new VentanaIDE().setVisible(true));
    }
}
```

Con menos de 50 líneas tienes un esqueleto bastante decente. A partir de aquí solo es ir rellenando.

### Ejercicio

Diseña la ventana principal de un cliente de correo:

* Toolbar arriba con: Nuevo, Responder, Reenviar, Borrar.
* Tres zonas con dos `JSplitPane` anidados:
  * Izquierda: lista de carpetas (Inbox, Enviados, Borradores…).
  * Centro: lista de mensajes de la carpeta.
  * Derecha: contenido del mensaje seleccionado.
* Barra de estado abajo.

No tienes que implementar la lógica: solo dejarlo bien dispuesto.
