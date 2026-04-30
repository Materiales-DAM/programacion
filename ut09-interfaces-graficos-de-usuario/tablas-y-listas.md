# Tablas y listas

`JList`, `JTable` y `JTree` son los componentes "pesados" de Swing: muestran colecciones de datos. Todos siguen el patrón **MVC**: hay una **vista** (el componente) y un **modelo** (los datos), separados.

Si actualizas el modelo, la vista se redibuja automáticamente. Si manipulas el componente directamente, normalmente lo estás haciendo mal.

### JList: lista de elementos

#### Versión rápida (modelo inmutable)

```java
String[] nombres = {"Ana", "Luis", "Carlos", "María"};
JList<String> lista = new JList<>(nombres);
JScrollPane scroll = new JScrollPane(lista);
```

Esto crea automáticamente un modelo interno. Sirve para listas estáticas. Si necesitas añadir o quitar elementos en tiempo de ejecución, usa `DefaultListModel`.

#### Versión recomendada (`DefaultListModel`)

```java
DefaultListModel<String> modelo = new DefaultListModel<>();
modelo.addElement("Ana");
modelo.addElement("Luis");

JList<String> lista = new JList<>(modelo);
lista.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

// Más adelante:
modelo.addElement("Carlos");           // añade al final
modelo.remove(0);                       // borra el primero
modelo.set(1, "Luis Manuel");           // reemplaza
```

#### Modos de selección

```java
lista.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
lista.setSelectionMode(ListSelectionModel.SINGLE_INTERVAL_SELECTION);
lista.setSelectionMode(ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);
```

#### Reaccionar a la selección

```java
lista.addListSelectionListener(e -> {
    if (!e.getValueIsAdjusting()) {  // ignorar eventos intermedios
        String seleccionado = lista.getSelectedValue();
        System.out.println("Elegido: " + seleccionado);
    }
});
```

#### Detalles útiles

```java
lista.setVisibleRowCount(8);              // filas visibles (afecta al tamaño preferido)
lista.setLayoutOrientation(JList.HORIZONTAL_WRAP); // mosaico horizontal
lista.setFixedCellHeight(24);             // optimización si todas las filas son iguales
```

### JTable: tabla con columnas

#### Versión rápida con arrays

```java
String[] columnas = {"Nombre", "Edad", "Ciudad"};
Object[][] datos = {
    {"Ana",    29, "Madrid"},
    {"Luis",   35, "Zaragoza"},
    {"Carlos", 41, "Sevilla"}
};
JTable tabla = new JTable(datos, columnas);
JScrollPane scroll = new JScrollPane(tabla);
```

Igual que `JList`, esto está bien para datos fijos. Para algo dinámico, mejor usar `DefaultTableModel`.

#### Con `DefaultTableModel`

```java
DefaultTableModel modelo = new DefaultTableModel(
    new Object[]{"Nombre", "Edad", "Ciudad"}, 0
);
modelo.addRow(new Object[]{"Ana",    29, "Madrid"});
modelo.addRow(new Object[]{"Luis",   35, "Zaragoza"});
modelo.addRow(new Object[]{"Carlos", 41, "Sevilla"});

JTable tabla = new JTable(modelo);

// Manipulación posterior:
modelo.addRow(new Object[]{"María", 26, "Bilbao"});
modelo.removeRow(0);
modelo.setValueAt("Madrid Centro", 1, 2);  // valor, fila, columna
```

#### Configuración habitual

```java
tabla.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
tabla.setAutoCreateRowSorter(true);       // hace clickables los headers para ordenar
tabla.setFillsViewportHeight(true);        // ocupa todo el alto del scroll, aun con pocas filas
tabla.getTableHeader().setReorderingAllowed(false); // si no quieres que el usuario mueva columnas
tabla.getColumnModel().getColumn(0).setPreferredWidth(150);
```

#### Tipos de celda

`DefaultTableModel` por defecto trata todo como `Object`. Si quieres que la columna "Edad" se muestre y ordene como número (alineada a la derecha) o que aparezca un checkbox para `Boolean`, hay que sobrescribir `getColumnClass`:

```java
DefaultTableModel modelo = new DefaultTableModel(
    new Object[]{"Producto", "Precio", "Disponible"}, 0
) {
    @Override
    public Class<?> getColumnClass(int columnIndex) {
        return switch (columnIndex) {
            case 1 -> Double.class;
            case 2 -> Boolean.class;
            default -> String.class;
        };
    }
};
modelo.addRow(new Object[]{"Manzanas", 1.99, true});
modelo.addRow(new Object[]{"Peras",    2.49, false});
```

Ahora la columna 1 se alinea a la derecha y se ordena numéricamente, y la 2 muestra checkboxes.

#### Modelo de tabla personalizado

Para listas de objetos del dominio (no genéricos `Object[]`), lo limpio es extender `AbstractTableModel`:

```java
public record Persona(String nombre, int edad, String ciudad) {}

public class PersonaTableModel extends AbstractTableModel {

    private final List<Persona> personas = new ArrayList<>();
    private final String[] columnas = {"Nombre", "Edad", "Ciudad"};

    public void add(Persona p) {
        personas.add(p);
        fireTableRowsInserted(personas.size() - 1, personas.size() - 1);
    }

    public Persona get(int fila) {
        return personas.get(fila);
    }

    @Override public int getRowCount()    { return personas.size(); }
    @Override public int getColumnCount() { return columnas.length; }
    @Override public String getColumnName(int c) { return columnas[c]; }

    @Override
    public Class<?> getColumnClass(int c) {
        return c == 1 ? Integer.class : String.class;
    }

    @Override
    public Object getValueAt(int fila, int col) {
        Persona p = personas.get(fila);
        return switch (col) {
            case 0 -> p.nombre();
            case 1 -> p.edad();
            case 2 -> p.ciudad();
            default -> null;
        };
    }
}
```

Aquí aparecen dos cosas modernas de Java: `record` para datos inmutables y `switch expression`. La llamada `fireTableRowsInserted` notifica a la vista que hay una fila nueva.

Uso:

```java
var modelo = new PersonaTableModel();
var tabla = new JTable(modelo);
modelo.add(new Persona("Ana", 29, "Madrid"));
modelo.add(new Persona("Luis", 35, "Zaragoza"));
```

#### Reaccionar a la selección

```java
tabla.getSelectionModel().addListSelectionListener(e -> {
    if (!e.getValueIsAdjusting()) {
        int fila = tabla.getSelectedRow();
        if (fila >= 0) {
            int filaModelo = tabla.convertRowIndexToModel(fila);
            Persona p = modelo.get(filaModelo);
            System.out.println("Selección: " + p);
        }
    }
});
```

**Atención**: si tienes activado el sorter (`setAutoCreateRowSorter(true)`), el índice visual no es el del modelo. Hay que convertirlo con `convertRowIndexToModel`. Es el error más común con `JTable`.

#### Renderers personalizados

Cómo se dibuja una celda lo decide un `TableCellRenderer`. Por defecto Swing usa renderers razonables, pero puedes pintar celdas con colores condicionales, iconos, etc.:

```java
tabla.setDefaultRenderer(Integer.class, new DefaultTableCellRenderer() {
    @Override
    public Component getTableCellRendererComponent(JTable table, Object value,
            boolean isSelected, boolean hasFocus, int row, int column) {
        var c = super.getTableCellRendererComponent(
            table, value, isSelected, hasFocus, row, column);
        if (value instanceof Integer n && n > 30) {
            c.setForeground(Color.RED);
        } else {
            c.setForeground(Color.BLACK);
        }
        setHorizontalAlignment(SwingConstants.RIGHT);
        return c;
    }
});
```

### JTree: estructura jerárquica

```java
DefaultMutableTreeNode raiz = new DefaultMutableTreeNode("Proyectos");

DefaultMutableTreeNode java = new DefaultMutableTreeNode("Java");
java.add(new DefaultMutableTreeNode("App de gestión"));
java.add(new DefaultMutableTreeNode("Servidor REST"));

DefaultMutableTreeNode web = new DefaultMutableTreeNode("Web");
web.add(new DefaultMutableTreeNode("Tienda online"));
web.add(new DefaultMutableTreeNode("Blog corporativo"));

raiz.add(java);
raiz.add(web);

JTree arbol = new JTree(raiz);
arbol.addTreeSelectionListener(e -> {
    DefaultMutableTreeNode nodo =
        (DefaultMutableTreeNode) arbol.getLastSelectedPathComponent();
    if (nodo != null) {
        System.out.println("Seleccionado: " + nodo.getUserObject());
    }
});
```

`DefaultMutableTreeNode` envuelve cualquier `Object` (`getUserObject()`). Para árboles muy grandes o con datos del dominio, conviene implementar `TreeModel` en condiciones.

### Ejemplo: tabla con buscador y botones

```java
import javax.swing.*;
import javax.swing.table.*;
import java.awt.*;

public class TablaConFiltro extends JFrame {

    public TablaConFiltro() {
        super("Tabla con filtro");
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        var modelo = new DefaultTableModel(
            new Object[]{"Producto", "Precio", "Stock"}, 0
        ) {
            @Override public Class<?> getColumnClass(int c) {
                return switch (c) {
                    case 1 -> Double.class;
                    case 2 -> Integer.class;
                    default -> String.class;
                };
            }
            @Override public boolean isCellEditable(int r, int c) { return false; }
        };
        modelo.addRow(new Object[]{"Manzanas", 1.99, 120});
        modelo.addRow(new Object[]{"Peras",    2.49, 80});
        modelo.addRow(new Object[]{"Naranjas", 1.79, 200});
        modelo.addRow(new Object[]{"Plátanos", 1.49, 150});

        var tabla = new JTable(modelo);
        var sorter = new TableRowSorter<>(modelo);
        tabla.setRowSorter(sorter);

        var filtro = new JTextField();
        filtro.getDocument().addDocumentListener(new javax.swing.event.DocumentListener() {
            @Override public void insertUpdate(javax.swing.event.DocumentEvent e)  { aplicar(); }
            @Override public void removeUpdate(javax.swing.event.DocumentEvent e)  { aplicar(); }
            @Override public void changedUpdate(javax.swing.event.DocumentEvent e) { aplicar(); }
            private void aplicar() {
                String texto = filtro.getText();
                sorter.setRowFilter(texto.isBlank()
                    ? null
                    : RowFilter.regexFilter("(?i)" + java.util.regex.Pattern.quote(texto), 0));
            }
        });

        var top = new JPanel(new BorderLayout(5, 5));
        top.setBorder(BorderFactory.createEmptyBorder(8, 8, 0, 8));
        top.add(new JLabel("Buscar:"), BorderLayout.WEST);
        top.add(filtro, BorderLayout.CENTER);

        setLayout(new BorderLayout());
        add(top, BorderLayout.NORTH);
        add(new JScrollPane(tabla), BorderLayout.CENTER);

        setSize(500, 350);
        setLocationRelativeTo(null);
    }

    public static void main(String[] args) {
        try { UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName()); }
        catch (Exception ignored) {}
        SwingUtilities.invokeLater(() -> new TablaConFiltro().setVisible(true));
    }
}
```

Aquí ves dos cosas importantes:

1. **`TableRowSorter`** permite filtrar y ordenar. `RowFilter.regexFilter("(?i)texto", 0)` filtra la columna 0 sin distinguir mayúsculas.
2. El método `isCellEditable` se sobrescribe para hacer toda la tabla de solo lectura.

### Ejercicio

Crea una tabla de "alumnos" con columnas Nombre, Curso y Nota. Bajo la tabla, un botón "Añadir" que abra un diálogo (`JDialog` o `JOptionPane.showInputDialog` repetido) para introducir los datos y los añada al modelo. Otro botón "Eliminar seleccionado" debe quitar la fila seleccionada (recuerda convertir el índice si tienes sorter).

