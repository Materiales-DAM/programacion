---
cover: ../../.gitbook/assets/lambda.jpeg
coverY: 0
---

# Lambdas (λ)

Las **expresiones lambda** en Java permiten escribir código más conciso y funcional al trabajar con funciones anónimas. Son útiles para implementar interfaces funcionales de manera más sencilla y clara.

## Sintaxis

La sintaxis básica de una expresión lambda es la siguiente

```java
(parametros) -> expresion
```

O, si tiene múltiples líneas:

```java
(parametros) -> {
    // Cuerpo de la función
}
```

* `(parámetros)`: Lista de parámetros que toma la lambda. Puede ser vacía si no hay parámetros, un parámetro sin paréntesis si hay exactamente uno, o múltiples parámetros separados por comas dentro de paréntesis si hay más de uno.
* `->`: Operador de flecha que separa los parámetros de la expresión.
* `expresion`: Código que se ejecutará cuando la lambda sea invocada.

Veamos algunos ejemplos básicos

1.  Lambda sin parámetros

    ```java
    () -> System.out.println("Hola, mundo")
    ```
2.  Lambda con un parámetro:

    ```java
    (nombre) -> System.out.println("Hola, " + nombre)
    ```
3.  Lambda con múltiples parámetros:

    ```java
    (x, y) -> x + y
    ```

## Notación del tipo de lambda

Para expresar el tipo de lambda que necesitamos en cada lugar vamos a usar la siguiente notación:

* Primero ponemos entre paréntesis y separados por comas los tipos de los parámetros de la lambda
* Después de los paréntesis ponemos el símbolo ->
* Por último, ponemos el tipo de retorno

Ejemplos:

* () -> String: no tiene parámetros y devuelve un String
* (Integer) -> String: tiene un parámetro de tipo Integer y devuelve un String
* (String) -> Void: tiene un parámetro de tipo String y no devuelve nada ( es void)
* (Integer, String) -> Integer: tiene dos parámetros: el primero es de tipo Integer y el segundo de tipo String. Además, devuelve un Integer.

## Uso de Lambdas con Streams

Las expresiones lambda se utilizan comúnmente con streams para realizar operaciones sobre colecciones de manera más concisa. Por ejemplo, para imprimir todos los elementos de una lista:

```java
List<String> nombres = List.of("Juan", "María", "Carlos");

// Esta lambda es de tipo (String) -> Void
nombres.forEach(nombre -> System.out.println(nombre));
```

## **Beneficios de las Lambdas**

* Código más compacto y legible.
* Facilitan la programación funcional en Java.
* Se utilizan junto con Streams y APIs funcionales.
