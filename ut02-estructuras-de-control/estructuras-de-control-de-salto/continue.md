---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Continue

Una sentencia `continue;` sirve para teminar la ejecución de una iteración de forma inmediata.&#x20;

```java
for(int i=0; i<10;i++){
    if(i == 5){
        // Cuando el continua se pasa a la siguiente iteración
        continue;
    }
    System.out.println(i);
}

// Esta sentencia se ejecuta cuando ha finalizado el bucle
System.out.println("Bucle finalizado");
```

En este ejemplo deberían ocurrir 10 iteraciones, en la iteración 6 (en la primera la i es 0) la sentencia de `System.out.println(i)` no se ejecuta debido a que el `continue` ocurre antes. La salida de este programa será:

```
0
1
2
3
4
6
7
8
9
Bucle finalizado

Process finished with exit code 0
```
