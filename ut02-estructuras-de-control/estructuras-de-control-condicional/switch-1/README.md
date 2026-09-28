---
cover: ../../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Operador ternario

El operador ternario (`? :`) es la única operación de Java que trabaja con **tres operandos**. Sirve para elegir entre dos valores según una condición, y todo ello en una sola **expresión**.

```java
condicion ? valorSiTrue : valorSiFalse
```

* `condicion`: tiene que ser una expresión `boolean`.
* `valorSiTrue`: es lo que devuelve la expresión si la condición es `true`.
* `valorSiFalse`: es lo que devuelve si es `false`.

Veamos el siguiente ejemplo:

```java
int edad = 20;
String estado = (edad >= 18) ? "mayor de edad" : "menor de edad";
System.out.println(estado); // mayor de edad
```

Los paréntesis alrededor de la condición no son obligatorios, pero ayudan a leer el código.

### Equivalencia con `if-else`

El ejemplo anterior hace lo mismo que esto:

```java
String estado;
if (edad >= 18) {
    estado = "mayor de edad";
} else {
    estado = "menor de edad";
}
```

La diferencia es importante. El `if` es una **sentencia**: ejecuta acciones. El ternario es una **expresión**: produce un valor. Por eso el ternario puede ir dentro de una asignación, de un `return` o de la llamada a un método.

```java
return (a > b) ? a : b;

System.out.println("Tienes " + n + (n == 1 ? " mensaje" : " mensajes"));
```

### Lo que NO se puede hacer

#### No es una sentencia

```java
edad >= 18 ? System.out.println("Mayor") : System.out.println("Menor"); // ❌ No compila
```

El ternario tiene que producir un valor que se use en algún sitio, y los métodos `void` no devuelven nada. Si lo que quieres es ejecutar acciones distintas, usa un `if`.

#### Los dos valores tienen que ser compatibles

```java
int x = cond ? 5 : "cinco"; // ❌ No compila: un int y un String no encajan en un int
```

### ¿Cuándo usarlo?

✅ **Úsalo** cuando elijas entre dos valores simples y la línea se lea de un vistazo.

❌ **Evítalo** en estos casos:

* Cuando haya que ejecutar acciones y no elegir valores.
* Cuando la condición o los valores sean largos.
* Cuando haga falta anidar más de un nivel.

La regla de oro: si tienes que pararte a pensar qué hace la línea, es mejor escribir un `if`.

