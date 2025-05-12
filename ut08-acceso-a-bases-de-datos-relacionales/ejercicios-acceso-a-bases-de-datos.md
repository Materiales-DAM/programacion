# Ejercicios acceso a bases de datos

## Instituto

Crea un programa que imprima el siguiente menú de opciones:

* Listar estudiantes: muestra todos los estudiantes en la base de datos
* Inserta estudiante: pide al usuario los datos de un estudiante y lo inserta en la base de datos.
* Elimina estudiante: pide al usuario un nif y lo elimina de la base de datos. Si el estudiante no existía, muestra el mensaje "No se ha podido encontrar el estudiante"
* Modificar estudiante: pide al usuario un nif, un nombre, apellidos y zipCode. Modifica el usuario con ese nif, actualizándole el nombre, apellidos y zipCode. Si no existe el estudiante  muestra el mensaje "No se ha podido encontrar el estudiante".

```java
package org.ies.tierno.model;

import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Student {
    private String nif;
    private String name;
    private String surname;
    private int zipCode;
}
```

