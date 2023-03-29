---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Menús interactivos

Uno de los casos de uso más comunes de la estructura do-while es la implementación de menús interactivos. En este tipo de programas se muestra al usuario un menú de opciones, el usuario elige una opción, se ejecuta el código vinculado a la opción seleccionada y vuelve a mostrarse el menú de opciones hasta que se elige la opción de salida.

En este tipo de programas queremos que el menú de opciones se ejecute al menos una vez, por lo que el uso de un bucle do-while resulta muy conveniente.

```java
Scanner scanner = new Scanner(System.in);

int option;
do {
            System.out.println("1. Saluda");
            System.out.println("2. Di otra cosa");
            System.out.println("3. Salir");
            option = scanner.nextInt();
            scanner.nextLine();
            // Esta selección de opciones se puede hacer con un switch
            if(option == 1) {
                System.out.println("Hola Mundo");
            } else if(option == 2) {
                System.out.println("otra cosa");
            }
} while(option != 3);
```

