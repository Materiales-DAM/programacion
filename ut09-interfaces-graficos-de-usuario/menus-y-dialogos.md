# Menús y diálogos

### La barra de menús: `JMenuBar`, `JMenu`, `JMenuItem`

Estructura típica de tres niveles:

```java
JMenuBar barra = new JMenuBar();

JMenu menuArchivo = new JMenu("Archivo");
JMenuItem itemNuevo = new JMenuItem("Nuevo");
JMenuItem itemAbrir = new JMenuItem("Abrir...");
JMenuItem itemSalir = new JMenuItem("Salir");

menuArchivo.add(itemNuevo);
menuArchivo.add(itemAbrir);
menuArchivo.addSeparator();
menuArchivo.add(itemSalir);

barra.add(menuArchivo);
ventana.setJMenuBar(barra);  // ¡no es add()!
```

Fíjate en `setJMenuBar`, no `add`. La barra de menú es especial dentro del `JFrame`.

#### Atajos de teclado y mnemónicos

```java
// Mnemonic: la letra subrayada que se activa con Alt+letra
menuArchivo.setMnemonic('A');
itemNuevo.setMnemonic('N');

// Accelerator: combinación que ejecuta la acción directamente
itemNuevo.setAccelerator(KeyStroke.getKeyStroke(
    KeyEvent.VK_N, InputEvent.CTRL_DOWN_MASK));
itemAbrir.setAccelerator(KeyStroke.getKeyStroke(
    KeyEvent.VK_O, InputEvent.CTRL_DOWN_MASK));
itemSalir.setAccelerator(KeyStroke.getKeyStroke(
    KeyEvent.VK_Q, InputEvent.CTRL_DOWN_MASK));
```

Mnemónico es la letra subrayada en el menú (Alt+A abre Archivo). Accelerator es el atajo global (Ctrl+N para Nuevo) que funciona aunque el menú no esté abierto.

#### Submenús

Un `JMenu` puede contener otro `JMenu`:

```java
JMenu reciente = new JMenu("Abrir reciente");
reciente.add(new JMenuItem("documento1.txt"));
reciente.add(new JMenuItem("notas.md"));
menuArchivo.add(reciente);
```

#### Items especiales: checkbox y radio

```java
JCheckBoxMenuItem mostrarLineas = new JCheckBoxMenuItem("Mostrar números de línea", true);
JRadioButtonMenuItem temaClaro = new JRadioButtonMenuItem("Tema claro", true);
JRadioButtonMenuItem temaOscuro = new JRadioButtonMenuItem("Tema oscuro");
ButtonGroup tema = new ButtonGroup();
tema.add(temaClaro);
tema.add(temaOscuro);

menuVer.add(mostrarLineas);
menuVer.addSeparator();
menuVer.add(temaClaro);
menuVer.add(temaOscuro);
```

#### Usando `Action` (recomendado)

Si tienes una `Action` ya definida (capítulo 4), basta con:

```java
JMenuItem item = new JMenuItem(guardarAction);
// hereda automáticamente texto, icono, accelerator y tooltip
```

Y el mismo `Action` puede colocarse también en una `JToolBar`. **Una fuente de verdad** para texto, icono, atajo y lógica.

### Menús contextuales: `JPopupMenu`

```java
JPopupMenu popup = new JPopupMenu();
popup.add(new JMenuItem("Cortar"));
popup.add(new JMenuItem("Copiar"));
popup.add(new JMenuItem("Pegar"));

componente.setComponentPopupMenu(popup);
```

`setComponentPopupMenu` es la forma moderna y portable: muestra el popup automáticamente cuando se hace clic derecho en el componente, en cualquier sistema operativo.

### Diálogos rápidos: `JOptionPane`

`JOptionPane` resuelve el 90% de los diálogos triviales con métodos estáticos. No tienes que crear ningún `JDialog`.

#### Mensaje informativo

```java
JOptionPane.showMessageDialog(
    ventana,
    "Operación completada con éxito.",
    "Información",
    JOptionPane.INFORMATION_MESSAGE
);
```

Tipos de mensaje (cambian el icono):

* `INFORMATION_MESSAGE`
* `WARNING_MESSAGE`
* `ERROR_MESSAGE`
* `QUESTION_MESSAGE`
* `PLAIN_MESSAGE` (sin icono)

#### Confirmación

```java
int respuesta = JOptionPane.showConfirmDialog(
    ventana,
    "¿Desea guardar los cambios antes de salir?",
    "Confirmar",
    JOptionPane.YES_NO_CANCEL_OPTION
);

switch (respuesta) {
    case JOptionPane.YES_OPTION    -> guardar();
    case JOptionPane.NO_OPTION     -> { /* salir sin guardar */ }
    case JOptionPane.CANCEL_OPTION -> { /* no hacer nada */ }
}
```

(Aprovecho para enseñar el `switch expression` de Java 21: más limpio que el clásico.)

#### Pedir un valor con `showInputDialog`

```java
String nombre = JOptionPane.showInputDialog(
    ventana,
    "¿Cómo te llamas?",
    "Pregunta",
    JOptionPane.QUESTION_MESSAGE
);
if (nombre != null) {
    System.out.println("Hola, " + nombre);
}
```

Si el usuario pulsa Cancelar, devuelve `null`. **Siempre comprueba**.

Variante con opciones predefinidas:

```java
String[] opciones = {"Pequeño", "Mediano", "Grande"};
String elegido = (String) JOptionPane.showInputDialog(
    ventana,
    "Selecciona el tamaño:",
    "Tamaño",
    JOptionPane.QUESTION_MESSAGE,
    null,           // icono
    opciones,
    opciones[1]     // valor por defecto
);
```

### Selector de archivos: `JFileChooser`

```java
JFileChooser fc = new JFileChooser();
fc.setCurrentDirectory(new File(System.getProperty("user.home")));
fc.setFileFilter(new FileNameExtensionFilter("Archivos de texto (*.txt)", "txt"));
fc.setMultiSelectionEnabled(false);

int resultado = fc.showOpenDialog(ventana);
if (resultado == JFileChooser.APPROVE_OPTION) {
    File archivo = fc.getSelectedFile();
    System.out.println("Seleccionado: " + archivo.getAbsolutePath());
}
```

Para guardar:

```java
int res = fc.showSaveDialog(ventana);
if (res == JFileChooser.APPROVE_OPTION) {
    File destino = fc.getSelectedFile();
    // si quieres añadir extensión por defecto:
    if (!destino.getName().endsWith(".txt")) {
        destino = new File(destino.getAbsolutePath() + ".txt");
    }
    Files.writeString(destino.toPath(), contenido);
}
```

Modos disponibles: `FILES_ONLY` (por defecto), `DIRECTORIES_ONLY`, `FILES_AND_DIRECTORIES`.

### Selector de color: `JColorChooser`

```java
Color elegido = JColorChooser.showDialog(
    ventana,
    "Color del texto",
    Color.BLACK
);
if (elegido != null) {
    area.setForeground(elegido);
}
```

### `JDialog`: diálogos personalizados

Cuando `JOptionPane` se queda corto (necesitas varios campos, una tabla dentro del diálogo…), creas un `JDialog`:

```java
public class DialogoLogin extends JDialog {

    private final JTextField usuario = new JTextField(15);
    private final JPasswordField clave = new JPasswordField(15);
    private boolean aceptado = false;

    public DialogoLogin(Frame padre) {
        super(padre, "Iniciar sesión", true);  // true = modal

        var panel = new JPanel(new GridLayout(2, 2, 5, 5));
        panel.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));
        panel.add(new JLabel("Usuario:"));
        panel.add(usuario);
        panel.add(new JLabel("Contraseña:"));
        panel.add(clave);

        var botonera = new JPanel();
        var ok = new JButton("Aceptar");
        var cancelar = new JButton("Cancelar");
        ok.addActionListener(e -> { aceptado = true; dispose(); });
        cancelar.addActionListener(e -> dispose());
        botonera.add(ok);
        botonera.add(cancelar);

        getRootPane().setDefaultButton(ok); // Enter activa "Aceptar"

        setLayout(new BorderLayout());
        add(panel, BorderLayout.CENTER);
        add(botonera, BorderLayout.SOUTH);

        pack();
        setLocationRelativeTo(padre);
    }

    public boolean isAceptado() { return aceptado; }
    public String getUsuario() { return usuario.getText(); }
    public char[] getClave() { return clave.getPassword(); }
}
```

Uso:

```java
var dlg = new DialogoLogin(this);
dlg.setVisible(true);  // bloquea hasta que se cierre (modal)
if (dlg.isAceptado()) {
    autenticar(dlg.getUsuario(), dlg.getClave());
}
```

Notas:

* El tercer argumento de `JDialog(...)` es el flag de modalidad: `true` bloquea la ventana padre hasta cerrar.
* `dispose()` cierra el diálogo y libera recursos.
* `getRootPane().setDefaultButton(boton)` asocia Enter al botón principal.

### Ejemplo: ventana con menú completo

```java
import javax.swing.*;
import java.awt.event.*;

public class VentanaConMenu extends JFrame {

    private final JTextArea editor = new JTextArea();

    public VentanaConMenu() {
        super("Editor con menú");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setSize(700, 500);
        setLocationRelativeTo(null);
        add(new JScrollPane(editor));

        setJMenuBar(crearMenu());
    }

    private JMenuBar crearMenu() {
        var barra = new JMenuBar();

        var archivo = new JMenu("Archivo");
        archivo.setMnemonic('A');
        archivo.add(item("Nuevo", KeyEvent.VK_N, e -> editor.setText("")));
        archivo.add(item("Abrir...", KeyEvent.VK_O, e -> abrir()));
        archivo.add(item("Guardar...", KeyEvent.VK_S, e -> guardar()));
        archivo.addSeparator();
        archivo.add(item("Salir", KeyEvent.VK_Q, e -> dispose()));

        var ayuda = new JMenu("Ayuda");
        ayuda.add(item("Acerca de...", 0, e -> JOptionPane.showMessageDialog(this,
            "Editor de ejemplo v1.0", "Acerca de", JOptionPane.INFORMATION_MESSAGE)));

        barra.add(archivo);
        barra.add(ayuda);
        return barra;
    }

    private JMenuItem item(String texto, int keyCode, ActionListener handler) {
        var i = new JMenuItem(texto);
        if (keyCode != 0) {
            i.setAccelerator(KeyStroke.getKeyStroke(keyCode, InputEvent.CTRL_DOWN_MASK));
        }
        i.addActionListener(handler);
        return i;
    }

    private void abrir() {
        var fc = new JFileChooser();
        if (fc.showOpenDialog(this) == JFileChooser.APPROVE_OPTION) {
            try {
                editor.setText(java.nio.file.Files.readString(fc.getSelectedFile().toPath()));
            } catch (Exception ex) {
                JOptionPane.showMessageDialog(this, "Error: " + ex.getMessage(),
                    "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    private void guardar() {
        var fc = new JFileChooser();
        if (fc.showSaveDialog(this) == JFileChooser.APPROVE_OPTION) {
            try {
                java.nio.file.Files.writeString(
                    fc.getSelectedFile().toPath(), editor.getText());
            } catch (Exception ex) {
                JOptionPane.showMessageDialog(this, "Error: " + ex.getMessage(),
                    "Error", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    public static void main(String[] args) {
        try { UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName()); }
        catch (Exception ignored) {}
        SwingUtilities.invokeLater(() -> new VentanaConMenu().setVisible(true));
    }
}
```

### Ejercicio

Amplía el editor anterior:

* Añade un menú "Edición" con Cortar, Copiar, Pegar (las acciones ya las tiene `JTextArea` por defecto a través de `editor.getActions()` o atajos estándar).
* Añade un menú "Ver" con un `JCheckBoxMenuItem` "Ajustar líneas" que active/desactive `editor.setLineWrap(...)`.
* Añade un diálogo personalizado "Buscar..." con un `JTextField` y un botón que resalte la siguiente aparición.
