---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Switch

Es otra estructura de control condicional. Sirve para establecer condiciones basadas en el valor de una expresión fija.&#x20;

* La expresión usada en el `switch` debe ser del tipo `int`, `byte`, `short`, `char` o `String`.​
* Los valores de los case deben ser del mismo tipo que la expresión del `switch`.​
* Cuando el valor es igual que el case en el que se está se ejecutan todas las sentencias hay hasta que se llega a un `break` o acaba la estructura `switch`.​
* No todos los casos deben contener un `break`.​
* Al final puede haber un caso por defecto (`default`) que se seleccionará si ninguno de los casos definidos coincide con la expresión del `switch`.

```java
switch (expression) {
    case value1:
        // Se ejecuta si expression es igual a value1
        
        // Cada case acaba con un break
        break;
    case value2:
        // Se ejecuta si expression es igual a value2
        
        // Cada case acaba con un break
        break;
    default:
        // Se ejecuta si expression no es ninguno de los casos definidos antes
        
}
```

Por ejemplo, si queremos decir el día de la semana a partir de un número

<pre class="language-java"><code class="lang-java">Scanner scanner = new Scanner(System.in);

int day = scanner.nextInt();
scanner.nextLine();

<strong>switch (day) {
</strong>    case 1:
        System.out.println("Lunes");
        break;
    case 2:
        System.out.println("Martes");
        break;
    case 3:
        System.out.println("Miércoles");
        break;
    case 4:
        System.out.println("Jueves");
        break;
    case 5:
        System.out.println("Viernes");
        break;
    case 6:
        System.out.println("Sábado");
        break;
    case 7:
        System.out.println("Domingo");
        break;
    default:
        System.out.println("No es un día de la semana");
}
</code></pre>
