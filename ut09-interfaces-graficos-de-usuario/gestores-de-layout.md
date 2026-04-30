# Gestores de layout

### ¿Por qué necesito un layout?

En otros frameworks (HTML, Qt Designer…) puedes posicionar elementos por coordenadas absolutas. En Swing **es mala idea**. Los motivos:

* Las ventanas se redimensionan: si tu botón está en `(100, 50)`, qué pasa si la ventana mide 200 píxeles de ancho.
* Las fuentes y métricas cambian entre sistemas operativos: lo que en Linux ocupa 80 px en macOS puede ser 95.
* La accesibilidad (zoom, alto DPI, idiomas con texto más largo) rompe los layouts fijos.

Por eso Swing usa **gestores de layout (`LayoutManager`)**: objetos que se encargan de calcular la posición y el tamaño de cada componente cuando algo cambia.

Cada contenedor (`JFrame`, `JPanel`…) tiene un layout. Cuando llamas a `panel.add(componente)`, el layout decide dónde colocarlo. Vamos a ver los más útiles.

### FlowLayout — en fila, como las palabras de un texto

```java
JPanel p = new JPanel(new FlowLayout(FlowLayout.LEFT, 10, 5));
p.add(new JButton("Uno"));
p.add(new JButton("Dos"));
p.add(new JButton("Tres"));
```

Pone los componentes uno detrás de otro, de izquierda a derecha. Cuando no caben, salta a la siguiente fila. Argumentos:

* Alineación: `LEFT`, `CENTER` (por defecto), `RIGHT`, `LEADING`, `TRAILING`.
* `hgap, vgap`: separación horizontal y vertical.

Es el layout por defecto de `JPanel`. Útil para barras de botones, pero queda raro en formularios grandes.

### BorderLayout — cinco zonas: norte, sur, este, oeste, centro

```java
JPanel p = new JPanel(new BorderLayout(5, 5));
p.add(new JLabel("Cabecera"), BorderLayout.NORTH);
p.add(new JLabel("Pie"), BorderLayout.SOUTH);
p.add(new JLabel("Izquierda"), BorderLayout.WEST);
p.add(new JLabel("Derecha"), BorderLayout.EAST);
p.add(new JLabel("Contenido principal"), BorderLayout.CENTER);
```

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Características:

* Es el layout por defecto de `JFrame` (en su content pane).
* El componente **CENTER** se queda con todo el espacio sobrante.
* Cada zona admite **un solo componente**. Si necesitas más, mete un `JPanel` con su propio layout.
* Las zonas N y S respetan la altura preferida del componente; E y W respetan su anchura preferida.

Es el "armazón" típico de una ventana: barra de herramientas arriba, barra de estado abajo, panel principal en el centro.

### GridLayout — rejilla de celdas idénticas

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

```java
JPanel p = new JPanel(new GridLayout(3, 4, 5, 5));
// 3 filas, 4 columnas, separaciones de 5 px
for (int i = 1; i <= 12; i++) {
    p.add(new JButton(String.valueOf(i)));
}
```

* Todas las celdas son del **mismo tamaño**.
* Si pones 0 en una dimensión, esa se calcula sola: `new GridLayout(0, 2)` significa "2 columnas, las filas que hagan falta".
* Útil para teclados, calculadoras, paneles de iconos uniformes.

### BoxLayout — caja de componentes en una sola dimensión

```java
JPanel p = new JPanel();
p.setLayout(new BoxLayout(p, BoxLayout.Y_AXIS)); // Y_AXIS = vertical, X_AXIS = horizontal
p.add(new JLabel("Línea 1"));
p.add(Box.createVerticalStrut(10));   // espaciador fijo
p.add(new JLabel("Línea 2"));
p.add(Box.createVerticalGlue());      // empuja lo que viene después al final
p.add(new JButton("Abajo del todo"));
```

Las "cajas vacías" útiles:

* `Box.createHorizontalStrut(n)` / `createVerticalStrut(n)`: separador rígido de n píxeles.
* `Box.createHorizontalGlue()` / `createVerticalGlue()`: separador elástico (se estira al máximo).
* `Box.createRigidArea(new Dimension(w, h))`: separador rígido en ambas dimensiones.

Cada componente respeta su tamaño preferido, pero hay que vigilar `setAlignmentX(...)` y `setMaximumSize(...)` para que no haya saltos raros.

### GridBagLayout — el más potente y el más complejo

`GridBagLayout` es como `GridLayout`, pero las celdas pueden tener tamaños distintos, ocupar varias filas/columnas y crecer de forma diferenciada. Es lo que necesitas para formularios serios.

```java
import javax.swing.*;
import java.awt.*;

public class FormularioGridBag extends JFrame {

    public FormularioGridBag() {
        super("Formulario con GridBagLayout");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        var panel = new JPanel(new GridBagLayout());
        var c = new GridBagConstraints();
        c.insets = new Insets(5, 5, 5, 5);
        c.anchor = GridBagConstraints.WEST;

        // Fila 0
        c.gridx = 0; c.gridy = 0; c.weightx = 0;
        panel.add(new JLabel("Nombre:"), c);

        c.gridx = 1; c.weightx = 1; c.fill = GridBagConstraints.HORIZONTAL;
        panel.add(new JTextField(20), c);

        // Fila 1
        c.gridx = 0; c.gridy = 1; c.weightx = 0; c.fill = GridBagConstraints.NONE;
        panel.add(new JLabel("Comentarios:"), c);

        c.gridx = 1; c.weightx = 1; c.weighty = 1;
        c.fill = GridBagConstraints.BOTH;
        panel.add(new JScrollPane(new JTextArea(5, 20)), c);

        // Fila 2: botón centrado, ocupa 2 columnas
        c.gridx = 0; c.gridy = 2; c.gridwidth = 2;
        c.weightx = 0; c.weighty = 0;
        c.fill = GridBagConstraints.NONE;
        c.anchor = GridBagConstraints.CENTER;
        panel.add(new JButton("Enviar"), c);

        add(panel);
        pack();
        setLocationRelativeTo(null);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new FormularioGridBag().setVisible(true));
    }
}
```

Las propiedades clave de `GridBagConstraints`:

| Propiedad          | Significado                                                                   |
| ------------------ | ----------------------------------------------------------------------------- |
| `gridx, gridy`     | Coordenada de la celda (columna, fila).                                       |
| `gridwidth`        | Cuántas columnas ocupa el componente.                                         |
| `gridheight`       | Cuántas filas ocupa.                                                          |
| `weightx, weighty` | Cómo se reparte el espacio extra (0 = no crece, 1 = máximo crecimiento).      |
| `fill`             | Si crece o no para llenar la celda: `NONE`, `HORIZONTAL`, `VERTICAL`, `BOTH`. |
| `anchor`           | Alineación dentro de la celda: `WEST`, `CENTER`, `NORTHEAST`…                 |
| `insets`           | Márgenes externos al componente (`Insets(top, left, bottom, right)`).         |

`GridBagLayout` es verboso pero predecible una vez le coges el truco. Para formularios complejos no hay alternativa estándar mejor en Swing.

### CardLayout — varias "tarjetas", una visible

```java
var cards = new JPanel(new CardLayout());
cards.add(new JLabel("Pantalla 1"), "uno");
cards.add(new JLabel("Pantalla 2"), "dos");
cards.add(new JLabel("Pantalla 3"), "tres");

CardLayout cl = (CardLayout) cards.getLayout();
cl.show(cards, "dos"); // pasar a la tarjeta "dos"
```

Útil para wizards, asistentes paso a paso, vistas con botones "Siguiente/Anterior". Solo una tarjeta es visible cada vez.

### El "no-layout" (`null`)

```java
panel.setLayout(null);
boton.setBounds(10, 20, 100, 30);
panel.add(boton);
```

Posicionas componentes por coordenadas absolutas. **Evítalo.** Aunque IDE como NetBeans lo usan internamente con su diseñador visual, mantenerlo a mano te dará problemas con redimensionado, fuentes y plataformas.

### Reglas prácticas para combinar layouts

En la vida real **anidas paneles**: un layout por panel. Por ejemplo, una ventana típica:

```
JFrame (BorderLayout)
├── NORTH:   JPanel (FlowLayout)         ← barra de botones
├── CENTER:  JPanel (BorderLayout)
│            ├── CENTER: JScrollPane(JTable)
│            └── EAST:   JPanel (BoxLayout vertical)  ← panel lateral
└── SOUTH:   JPanel (BorderLayout)        ← barra de estado
             ├── WEST: JLabel("Listo")
             └── EAST: JLabel("v1.0")
```

Cada panel resuelve un problema local y simple. Si te ves usando `GridBagLayout` con 30 componentes, probablemente puedes dividirlo en 3 paneles más simples.

### Recomendación general

| Situación                                          | Layout recomendado                   |
| -------------------------------------------------- | ------------------------------------ |
| Esqueleto de ventana (cabecera/pie/contenido)      | `BorderLayout`                       |
| Barra de botones                                   | `FlowLayout`                         |
| Botones de calculadora, teclado…                   | `GridLayout`                         |
| Formulario etiqueta-campo                          | `GridBagLayout`                      |
| Lista vertical de elementos con espaciado variable | `BoxLayout`                          |
| Wizard / asistente paso a paso                     | `CardLayout`                         |
| Necesitas algo aún más flexible                    | **MigLayout** (externo, muy popular) |

### Ejercicio

Diseña con paneles y layouts anidados una "calculadora": en la zona NORTH una `JTextField` para mostrar el resultado, y en la zona CENTER un `GridLayout(5, 4)` con teclas 0–9, +, –, ×, ÷, =, C, ., ±. No tienes que implementar la lógica todavía: solo el layout.
