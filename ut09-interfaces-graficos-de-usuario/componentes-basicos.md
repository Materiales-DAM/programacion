# Componentes básicos

Aquí cubrimos los componentes más usados de Swing. Cada uno con un ejemplo mínimo y los métodos que más vas a tocar. Más adelante (capítulos 3 y 4) veremos cómo organizarlos en pantalla y cómo reaccionar a sus eventos.

### JLabel — texto y/o icono no editable

```java
JLabel saludo = new JLabel("Bienvenido");
JLabel conIcono = new JLabel("Imprimir", new ImageIcon("printer.png"), JLabel.LEFT);
saludo.setFont(new Font("SansSerif", Font.BOLD, 18));
saludo.setForeground(Color.DARK_GRAY);
```

* `setText(String)` y `setIcon(Icon)`: cambian el contenido.
* `setHorizontalAlignment(int)`: `LEFT`, `CENTER`, `RIGHT`.
* Acepta HTML básico: `new JLabel("<html><b>Negrita</b><br>y salto de línea</html>")`.

### JButton — botón pulsable

```java
JButton boton = new JButton("Aceptar");
boton.setMnemonic('A'); // Alt+A lo activa
boton.setToolTipText("Confirma la operación");
boton.addActionListener(e -> System.out.println("Pulsado"));
```

* `addActionListener` dispara código al pulsar (lo veremos a fondo en el capítulo 4).
* `setEnabled(false)` lo deja en gris y lo desactiva.
* También soporta iconos: `new JButton("Guardar", new ImageIcon("save.png"))`.

### JTextField — entrada de texto en una línea

```java
JTextField nombre = new JTextField(20); // 20 columnas (no caracteres exactos)
nombre.setText("Valor por defecto");
String texto = nombre.getText();
```

* El parámetro del constructor son "columnas" en unidades del ancho de fuente.
* `setEditable(false)` lo convierte en solo lectura sin cambiar su aspecto a deshabilitado.
* Genera `ActionEvent` cuando el usuario pulsa Enter dentro.

### JPasswordField — entrada con caracteres ocultos

```java
JPasswordField clave = new JPasswordField(15);
char[] chars = clave.getPassword(); // ¡no usar getText()!
clave.setEchoChar('●');
```

Importante: usa `getPassword()` que devuelve `char[]`, no `getText()`. Así puedes sobrescribir el array con ceros tras usarlo, en vez de dejar la contraseña como `String` inmutable en memoria.

### JTextArea — texto multilinea

```java
JTextArea area = new JTextArea(10, 40); // 10 filas, 40 columnas
area.setLineWrap(true);
area.setWrapStyleWord(true);
JScrollPane scroll = new JScrollPane(area);
```

`JTextArea` **no** lleva scroll por sí solo: hay que envolverlo en un `JScrollPane`. Es un error muy común olvidarlo y luego no entender por qué no aparece la barra de desplazamiento.

### JCheckBox — casilla marcable

```java
JCheckBox acepto = new JCheckBox("Acepto los términos");
acepto.setSelected(true);
boolean valor = acepto.isSelected();
```

Útil para opciones independientes (cada checkbox es autónomo).

### JRadioButton + ButtonGroup — opción exclusiva

```java
JRadioButton r1 = new JRadioButton("Pequeño");
JRadioButton r2 = new JRadioButton("Mediano", true); // seleccionado por defecto
JRadioButton r3 = new JRadioButton("Grande");

ButtonGroup grupo = new ButtonGroup();
grupo.add(r1);
grupo.add(r2);
grupo.add(r3);
```

El `ButtonGroup` no es un componente visual: solo se encarga de garantizar que como mucho uno esté seleccionado. Tienes que añadir cada radio al `ButtonGroup` **y** al panel correspondiente.

### JComboBox — desplegable

```java
String[] paises = {"España", "Portugal", "Francia", "Italia"};
JComboBox<String> combo = new JComboBox<>(paises);
combo.setSelectedIndex(0);
combo.setEditable(false); // true permite escribir un valor que no esté en la lista

String seleccionado = (String) combo.getSelectedItem();
```

Como ves, `JComboBox` es **genérico**: indica el tipo de los elementos para evitar casts. Si tu lista cambia en tiempo de ejecución, mejor usa un `DefaultComboBoxModel<T>`.

### JSpinner — valor numérico (o de lista) con flechas

```java
JSpinner edad = new JSpinner(new SpinnerNumberModel(18, 0, 120, 1));
// (valor inicial, mínimo, máximo, incremento)
int valor = (int) edad.getValue();
```

También sirve para fechas (`SpinnerDateModel`) o listas (`SpinnerListModel`).

### JSlider — selector deslizable

```java
JSlider volumen = new JSlider(0, 100, 50);
volumen.setMajorTickSpacing(25);
volumen.setMinorTickSpacing(5);
volumen.setPaintTicks(true);
volumen.setPaintLabels(true);
```

Genera `ChangeEvent` mientras el usuario lo mueve. Si solo quieres la decisión final, comprueba `slider.getValueIsAdjusting()`.

### JProgressBar — barra de progreso

```java
JProgressBar barra = new JProgressBar(0, 100);
barra.setValue(35);
barra.setStringPainted(true); // muestra "35%" encima
```

Si no conoces la duración, llama a `setIndeterminate(true)` para tener una barra "rebotando".

### Ejemplo completo: formulario con todo lo anterior

```java
import javax.swing.*;
import java.awt.*;

public class Formulario extends JFrame {

    public Formulario() {
        super("Formulario de ejemplo");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        var panel = new JPanel(new GridLayout(0, 2, 10, 10));
        panel.setBorder(BorderFactory.createEmptyBorder(15, 15, 15, 15));

        panel.add(new JLabel("Nombre:"));
        panel.add(new JTextField(20));

        panel.add(new JLabel("Contraseña:"));
        panel.add(new JPasswordField(20));

        panel.add(new JLabel("Edad:"));
        panel.add(new JSpinner(new SpinnerNumberModel(18, 0, 120, 1)));

        panel.add(new JLabel("País:"));
        panel.add(new JComboBox<>(new String[]{"España", "Portugal", "Francia"}));

        panel.add(new JCheckBox("Suscribirse al boletín"));
        panel.add(new JCheckBox("Aceptar términos"));

        var enviar = new JButton("Enviar");
        enviar.addActionListener(e -> JOptionPane.showMessageDialog(this, "Enviado"));
        panel.add(enviar);
        panel.add(new JButton("Cancelar"));

        add(panel);
        pack();
        setLocationRelativeTo(null);
    }

    public static void main(String[] args) {
        try { UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName()); }
        catch (Exception ignored) {}
        SwingUtilities.invokeLater(() -> new Formulario().setVisible(true));
    }
}
```

Fíjate en `GridLayout(0, 2, 10, 10)`: 0 filas (= "las que hagan falta") y 2 columnas, con 10 px de separación. Lo veremos a fondo en el siguiente capítulo.

### Ejercicio

Crea un formulario de matrícula con:

* Nombre y apellidos (`JTextField`).
* Curso: 1º DAM, 2º DAM, 1º DAW, 2º DAW (`JComboBox`).
* Modalidad: Presencial / Online (`JRadioButton` agrupados).
* Asignaturas optativas (varios `JCheckBox`).
* Botón "Matricular" que muestre por consola lo seleccionado.
