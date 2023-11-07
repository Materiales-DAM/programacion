---
cover: ../../.gitbook/assets/arrays.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Recorrer un array

En ocasiones, el tamaño de un array no se va a saber en tiempo de compilación. Por ejemplo, si es el usuario quien mete el tamaño del array y luego lo rellenamos con valores.

Por esto, para recorrer todos los valores de un array vamos a utilizar un bucle for.

Por ejemplo si tenemos el siguiente array



<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>



## Fori

Vamos a querer recorrerlo en un bucle for, dicho bucle for deberá hacer tantas iteraciones como el tamaño del array. Para obtener el tamaño del array haremos `array.length`

```java
// Este bucle realiza el mismo número de iteraciones que el tamaño de numbers
for(int i = 0; i < numbers.length; i++){
    // En cada iteración i se corresponde con la posición del array en la que estamos mirando
    
    // Creamos number para almacenar el valor que hay en la posición i del array
    int number = numbers[i];
    System.out.println("El valor en la posición " + i + " es " + number); 
}
```

Si se ejecuta el código anterior aparecerá lo siguiente en la consola

```log
El valor en la posición 0 es 5
El valor en la posición 1 es 1
El valor en la posición 2 es 7
El valor en la posición 3 es 9

Process finished with exit code 0
```

## For each

En ocasiones no nos interesa el valor de la i más que para sacar valores del array.

```java
int sum=0;
for(int number: numbers){
    sum= sum + number;
}
```
