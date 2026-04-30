# Eventos y oyentes

### El modelo de eventos en Swing

Una interfaz gráfica es **reactiva**: no se ejecuta secuencialmente como un script, sino que **espera** a que pase algo (un clic, una tecla, un cambio de selección…) y entonces reacciona. Ese "algo" es un **evento**, y el código que reacciona es un **listener** (oyente).

El modelo es el mismo en casi todo Swing:

1. Creas un componente: `JButton b = new JButton("Aceptar");`
2. Le adjuntas un listener: `b.addXxxListener(...)`.
3. Cuando ocurre algo, el componente invoca tu listener pasándole un objeto evento con los detalles.

### ActionListener: el más común

`ActionListener` cubre la "acción principal" de un componente: pulsar un botón, dar Enter en un `JTextField`, seleccionar un ítem de menú…

#### Estilo antiguo (clase anónima)

```java
JButton boton = new JButton("Saludar");
boton.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("¡Hola!");
    }
});
```

Funciona, pero es muy verboso. Hoy se usa poco.

#### Estilo moderno (lambda)

```java
boton.addActionListener(e -> System.out.println("¡Hola!"));
```

`ActionListener` es interfaz funcional (un único método abstracto), así que aceptan lambdas. Esto es lo habitual en Java 8 en adelante, y desde luego en Java 21.

#### Varias acciones, un solo handler

```java
JButton guardar = new JButton("Guardar");
JButton abrir = new JButton("Abrir");

ActionListener handler = e -> {
    Object src = e.getSource();
    if (src == guardar) guardar();
    else if (src == abrir) abrir();
};

guardar.addActionListener(handler);
abrir.addActionListener(handler);
```

Con `e.getSource()` o `e.getActionCommand()` puedes distinguir quién disparó el evento. Aún así, suele ser más limpio un listener por botón.

### El objeto `ActionEvent`

Lo que recibe el listener:

| Método               | Devuelve                                                                  |
| -------------------- | ------------------------------------------------------------------------- |
| `getSource()`        | El objeto que disparó el evento (ej. el `JButton`).                       |
| `getActionCommand()` | Por defecto, el texto del botón. Se puede cambiar con `setActionCommand`. |
| `getModifiers()`     | Qué teclas modificadoras estaban pulsadas (Shift, Ctrl…).                 |
| `getWhen()`          | Marca de tiempo en milisegundos del evento.                               |

### Eventos de ratón: `MouseListener` y `MouseMotionListener`

`MouseListener` tiene **5 métodos**, no nos suelen interesar todos. Por eso existe `MouseAdapter`, una clase abstracta con todos los métodos vacíos para que sobrescribas solo los que uses:

```java
JLabel etiqueta = new JLabel("Pásame el ratón");
etiqueta.addMouseListener(new MouseAdapter() {
    @Override
    public void mouseEntered(MouseEvent e) {
        etiqueta.setText("¡Hola!");
    }
    @Override
    public void mouseExited(MouseEvent e) {
        etiqueta.setText("Adiós");
    }
    @Override
    public void mouseClicked(MouseEvent e) {
        if (e.getClickCount() == 2) System.out.println("Doble clic");
        if (SwingUtilities.isRightMouseButton(e)) System.out.println("Botón derecho");
    }
});
```

Métodos disponibles:

* `mouseClicked` (clic completo: presionar + soltar sin moverse).
* `mousePressed`, `mouseReleased`.
* `mouseEntered`, `mouseExited`.
* `mouseDragged`, `mouseMoved` (estos dos están en `MouseMotionListener`, también cubierto por `MouseAdapter`).

### Eventos de teclado: `KeyListener`

```java
campo.addKeyListener(new KeyAdapter() {
    @Override
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_ENTER) confirmar();
        if (e.isControlDown() && e.getKeyCode() == KeyEvent.VK_S) guardar();
    }
});
```

**Aviso**: `KeyListener` solo recibe eventos cuando el componente tiene el foco. Para atajos globales de la ventana es **mucho mejor** usar `KeyStroke` con el sistema de **Key Bindings** o asociarlo a un `Action` de menú (lo veremos en el capítulo 6).

```java
// Atajo Ctrl+S en toda la ventana, sin depender del foco
JRootPane root = ventana.getRootPane();
KeyStroke ks = KeyStroke.getKeyStroke(KeyEvent.VK_S, InputEvent.CTRL_DOWN_MASK);
root.getInputMap(JComponent.WHEN_IN_FOCUSED_WINDOW).put(ks, "guardar");
root.getActionMap().put("guardar", new AbstractAction() {
    @Override public void actionPerformed(ActionEvent e) { guardar(); }
});
```

### DocumentListener: detectar cambios en un campo de texto

`JTextField` y `JTextArea` no usan `ChangeListener`. Para reaccionar a cada cambio de contenido, se escucha el **documento** subyacente:

```java
JTextField busqueda = new JTextField(20);
busqueda.getDocument().addDocumentListener(new DocumentListener() {
    @Override public void insertUpdate(DocumentEvent e) { filtrar(); }
    @Override public void removeUpdate(DocumentEvent e) { filtrar(); }
    @Override public void changedUpdate(DocumentEvent e) { /* sólo atributos */ }

    private void filtrar() {
        String texto = busqueda.getText();
        // ...lógica de búsqueda
    }
});
```

Útil para búsquedas "según escribes", validaciones en vivo, etc.

### ItemListener: cambios en checkboxes, radios, combos

```java
JCheckBox enviarCopia = new JCheckBox("Enviar copia");
enviarCopia.addItemListener(e -> {
    if (e.getStateChange() == ItemEvent.SELECTED) {
        System.out.println("Activado");
    } else {
        System.out.println("Desactivado");
    }
});
```

`JComboBox` también dispara `ItemEvent` al cambiar la selección, además de `ActionEvent`. El primero te avisa de la deselección del valor anterior **y** de la selección del nuevo; el segundo solo del nuevo.

### ChangeListener: cambios en sliders, spinners, tabbed panes

```java
JSlider volumen = new JSlider(0, 100, 50);
volumen.addChangeListener(e -> {
    if (!volumen.getValueIsAdjusting()) {
        System.out.println("Volumen final: " + volumen.getValue());
    }
});
```

`getValueIsAdjusting()` es útil para evitar disparar 50 actualizaciones mientras el usuario arrastra: solo procesas cuando suelta.

### El patrón `Action`: más limpio para acciones reutilizables

Si la misma acción ("Guardar") se invoca desde un botón, un menú y un atajo de teclado, hay una clase para encapsularla: `Action` (interfaz) con `AbstractAction` como implementación base.

```java
Action guardarAction = new AbstractAction("Guardar", new ImageIcon("save.png")) {
    @Override
    public void actionPerformed(ActionEvent e) {
        guardarDocumento();
    }
};
guardarAction.putValue(Action.SHORT_DESCRIPTION, "Guarda los cambios");
guardarAction.putValue(Action.ACCELERATOR_KEY,
    KeyStroke.getKeyStroke(KeyEvent.VK_S, InputEvent.CTRL_DOWN_MASK));

JButton boton = new JButton(guardarAction);
JMenuItem item = new JMenuItem(guardarAction);
```

Ventajas:

* Un solo objeto contiene texto, icono, atajo de teclado, tooltip y lógica.
* Si llamas a `guardarAction.setEnabled(false)`, **todos** los botones y menús asociados se deshabilitan a la vez.

Es buena práctica usar `Action` para todo lo que aparece en menús.

### Errores típicos

1. **Bloquear el EDT**: si tu listener tarda 5 segundos en ejecutarse, la ventana se congela durante esos 5 segundos. Para tareas largas, usa `SwingWorker` (capítulo 8).
2. **Olvidar el `addXxxListener`**: el componente está en pantalla pero no responde porque nadie lo escucha.
3. **Capturar un componente final que cambia**: dentro de una lambda accedes a una variable que se reasigna fuera. La lambda se queda con el valor inicial. Solución: declarar como `final` o no reasignar.
4. **Crear listeners duplicados**: si llamas dos veces a `addActionListener` con la misma lambda, el botón ejecutará la acción dos veces por clic. Cuidado al construir interfaces dinámicas.

### Ejemplo integrador: contador

```java
import javax.swing.*;
import java.awt.*;

public class Contador extends JFrame {

    private int valor = 0;
    private final JLabel etiqueta = new JLabel("0", JLabel.CENTER);

    public Contador() {
        super("Contador");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(new BorderLayout(10, 10));

        etiqueta.setFont(new Font("SansSerif", Font.BOLD, 48));
        add(etiqueta, BorderLayout.CENTER);

        var botones = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        var menos = new JButton("−");
        var mas = new JButton("+");
        var reset = new JButton("Reset");

        menos.addActionListener(e -> actualizar(valor - 1));
        mas.addActionListener(e -> actualizar(valor + 1));
        reset.addActionListener(e -> actualizar(0));

        botones.add(menos);
        botones.add(reset);
        botones.add(mas);
        add(botones, BorderLayout.SOUTH);

        setSize(300, 200);
        setLocationRelativeTo(null);
    }

    private void actualizar(int nuevoValor) {
        valor = nuevoValor;
        etiqueta.setText(String.valueOf(valor));
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new Contador().setVisible(true));
    }
}
```

### Ejercicio

Coge la calculadora (estructura) del capítulo anterior y dale vida:

* Cada botón numérico añade su dígito a la `JTextField` superior.
* Los botones de operación (+, −, ×, ÷) recuerdan el operador y el valor anterior.
* "=" calcula y muestra el resultado.
* "C" limpia.

Pista: usa una variable `double acumulador` y otra `String operador`. No te preocupes por el manejo perfecto de errores aún.
