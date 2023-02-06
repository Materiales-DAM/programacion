# Tipos básicos

Según Wikipedia "En [ciencias de la computación](https://es.wikipedia.org/wiki/Ciencias\_de\_la\_computaci%C3%B3n), un tipo de dato informático o simplemente tipo, es un atributo de los datos que indica al ordenador (y/o al [programador/programadora](https://es.wikipedia.org/wiki/Programador)) sobre la clase de datos que se va a manejar. Esto incluye imponer restricciones en los datos, como qué valores pueden tomar y qué operaciones se pueden realizar."​

La siguiente tabla contiene los conocidos como tipos primitivos de Java

| Tipo      | Tamaño  | Descripción                                                                                          |
| --------- | ------- | ---------------------------------------------------------------------------------------------------- |
| `byte`    | 1 byte  | Almacena enteros entre -128 y 127                                                                    |
| `short`   | 2 bytes | Almacena enteros entre -32,768 y 32,767                                                              |
| `int`     | 4 bytes | Almacena enteros entre -2,147,483,648 y 2,147,483,647                                                |
| `long`    | 8 bytes | Almacena enteros entre -9,223,372,036,854,775,808 y 9,223,372,036,854,775,807                        |
| `float`   | 4 bytes | Almacena número con decimales. Permite almacenar con precisiones mínimas de 6 a 7 digitos decimales. |
| `double`  | 8 bytes | Almacena número con decimales. Permite almacenar con precisiones mínimas de 15 digitos decimales.    |
| `boolean` | 1 bit   | Almacena valores booleanos (true o false)                                                            |
| `char`    | 2 bytes | Almacena un caracter ASCII                                                                           |

Otro tipo básico que es `String`, este tipo nos permite almacenar cadenas de caracteres. Para definir un valor de tipo String usaremos las comillas dobles (`"texto"`) alrededor del texto que se quiera crear.

```java
String sentence = "Este texto se almacena en la variable sentence";
// ¿Qué aparecerá en pantalla?
System.out.println(sentence);
```

Haz click [aquí](https://www.w3schools.com/java/exercise.asp?filename=exercise\_data\_types1) para hacer unos ejercicios de tipos.
