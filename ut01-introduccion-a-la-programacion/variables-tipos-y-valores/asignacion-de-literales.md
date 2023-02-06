# Asignación de literales

Como su nombre indica, el valor de una variable puede cambiar a lo largo del programa. Cuando se quiere cambiar el valor de una variable se debe ejecutar una sentencia de asignación.

Es posible asignarle un **valor literal** a la variable en la misma sentencia en la que se declara. Esto se denomina inline initialization. Los valores literales aparecen explicitamente en el código.

```java
// En esta sentencia se declara la variable myNumber y se le asigna el 
// valor literal 3
int myNumber = 3;
```

También es posible separar lo anterior en dos sentencias:

```java
// Se declara la variable myNumber
int myNumber;
// Se le asigna el valor literal 3 a la variable myNumber
myNumber = 3;
```

El valor de una variable se puede modificar tantas veces como se desee a lo largo del programa, simplemente se deben realizar nuevas asignaciones de valores.

```java
// Se declara la variable myNumber
int myNumber;
// Se le asigna el valor literal 3 a la variable myNumber
myNumber = 3;

System.out.println(myNumber);

// Se le asigna el valor literal 5 a la variable myNumber
myNumber = 5;

System.out.println(myNumber);

// ¿Qué saldrá impreso en pantalla al ejecutar estas sentencias?
```
