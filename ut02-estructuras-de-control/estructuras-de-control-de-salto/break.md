---
cover: ../../.gitbook/assets/control-structures.gif
coverY: 0
---

# Break

Una sentencia `break;` sirve para teminar la ejecución de un bucle de forma inmediata.&#x20;

```java
for(int i=0; i<10;i++){
    if(i == 5){
        // Cuando el break se ejecuta se sale del bucle
        break;
    }
    System.out.println(i);
}

// Esta sentencia se ejecuta cuando ha finalizado el bucle
System.out.println("Bucle finalizado");
```

En este ejemplo deberían ocurrir 10 iteraciones, pero la presencia del `break` hace que el bucle termine antes de lo normal, en la iteración 6 (en la primera la i es 0). La salida de este programa será:

```
0
1
2
3
4
Bucle finalizado

Process finished with exit code 0
```
