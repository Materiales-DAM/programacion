---
coverY: 0
---

# Introducción

### ¿Qué es Swing?

Swing es la biblioteca estándar de Java para construir **interfaces gráficas de usuario (GUI)** de escritorio. Forma parte de Java SE desde la versión 1.2 (1998) y vive en los paquetes `javax.swing.*`. Con Swing puedes crear ventanas, botones, menús, tablas, formularios… todo lo que esperas de una aplicación de escritorio clásica.

Aunque hoy existen alternativas más modernas (JavaFX, web, Electron…), Swing sigue siendo:

* **Estable y maduro**: lleva más de 25 años en producción y sus bugs principales están resueltos.
* **Incluido en el JDK**: no añade dependencias externas.
* **Multiplataforma**: el mismo `.jar` funciona en Windows, Linux y macOS.
* **Suficiente para muchas herramientas internas**: editores, paneles de administración, utilidades…

Sigue siendo una opción razonable para aplicaciones internas, herramientas administrativas, y desde luego para **enseñar los fundamentos de programación gráfica orientada a eventos**.

### Un poco de historia

| Año  | Hito                                                                                       |
| ---- | ------------------------------------------------------------------------------------------ |
| 1995 | **AWT** (Abstract Window Toolkit). Componentes "pesados", delegan en el sistema operativo. |
| 1998 | **Swing** (Java 1.2). Componentes "ligeros", dibujados por Java.                           |
| 2008 | **JavaFX** aparece como sucesor moderno de Swing.                                          |
| 2014 | JavaFX se incluye en el JDK (Java 8).                                                      |
| 2018 | JavaFX se separa del JDK (Java 11) y pasa a OpenJFX.                                       |
| 2026 | Swing **sigue** en el JDK estándar y se mantiene activamente.                              |

Aunque Oracle posicionó JavaFX como "sucesor", Swing nunca ha sido marcado como obsoleto y recibe pequeñas mejoras en cada versión del JDK.

### Swing vs AWT vs JavaFX

* **AWT** (`java.awt.*`): la biblioteca original. Sus componentes son "pesados": cada `Button` de AWT es realmente un botón nativo del sistema operativo. Hoy se usa principalmente como base de Swing (`java.awt.Color`, `java.awt.Font`, layouts…).
* **Swing** (`javax.swing.*`): construido encima de AWT, pero sus componentes son "ligeros" (lightweight): los dibuja Java pixel a pixel. Esto da uniformidad entre plataformas y un control total sobre el aspecto.
* **JavaFX** (`javafx.*`): API más moderna, con un grafo de escena, CSS, animaciones nativas y soporte multimedia. Más potente pero también más compleja, y desde Java 11 hay que añadirla aparte.

Para este curso usamos **Swing**, porque es lo que viene en el JDK y porque sus conceptos (jerarquía de contenedores, modelo de eventos, EDT) son fundamentos que se trasladan a casi cualquier framework de UI.

### Arquitectura: contenedores, componentes y MVC

Una aplicación Swing es esencialmente un **árbol de componentes**:

```
JFrame (la ventana)
└── JPanel (contenedor general)
    ├── JLabel ("Nombre:")
    ├── JTextField (campo de texto)
    └── JButton ("Aceptar")
```

Cada nodo del árbol es un objeto Java, y todos los componentes Swing heredan de `JComponent`, que a su vez hereda de `java.awt.Container`. Conviene tener clara esta jerarquía:

```
Object
└── Component (AWT)
    └── Container (AWT)
        └── JComponent (Swing)
            ├── JLabel, JButton, JTextField…
            └── JPanel, JScrollPane, JTabbedPane…
```

Los componentes Swing aplican el patrón **MVC** (Modelo-Vista-Controlador) de forma simplificada: cada componente complejo (`JList`, `JTable`, `JTree`…) tiene un **modelo** que guarda los datos, una **UI delegate** que lo dibuja y oyentes que reaccionan a la interacción.

### El Event Dispatch Thread (EDT)

Esto es lo más importante de toda la introducción, así que subráyalo:

> **Toda interacción con componentes Swing debe hacerse en un único hilo: el Event Dispatch Thread (EDT).**

Si actualizas un `JLabel` desde otro hilo, tarde o temprano la aplicación se comportará de forma errática. En el capítulo 8 veremos `SwingUtilities.invokeLater`, `SwingWorker` y `javax.swing.Timer`, las herramientas para trabajar correctamente con concurrencia.

### ¿Por qué aprender Swing en 2026?

1. **Es Java puro**, sin dependencias externas. Ideal para enseñanza.
2. **Los conceptos son universales**: árbol de componentes, layouts, eventos y bucle de eventos están en cualquier UI moderna (Android, iOS, web, Qt…).
3. **Sigue funcionando**: hay millones de líneas de Swing en producción (IntelliJ IDEA, jEdit, NetBeans, herramientas científicas, ERPs…).
4. **Es ligero**: una app Swing arranca en milisegundos, sin necesidad de Chromium incrustado.

### Lo que vas a aprender

Al terminar este tutorial sabrás:

* Crear ventanas y organizar componentes con layouts.
* Escuchar y responder a eventos del usuario.
* Usar tablas, listas, menús y diálogos.
* Manejar concurrencia con `SwingWorker` sin congelar la interfaz.
* Estructurar una aplicación pequeña separando modelo, vista y lógica.

