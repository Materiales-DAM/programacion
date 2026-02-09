---
cover: ../../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Ejercicios Map\<K, V>

## User

```java
import lombok.Data;
import lombok.AllArgsConstructor;

@Data
@AllArgsConstructor
public class User {
    private String nif;
    private String name;
    private String surname;
    private String phoneNumber;
    private String email;
    private int age;

}

```

1. Escribe un programa que almacene los datos de los usuarios. Indexa los usuarios por el nif del usuario.
   1. put
2. Crea un método que dado un mapa de usuarios indexados por nif y un nif, devuelva el teléfono. (public static String getPhoneByNif(Map\<String, User> usersByNif, String nif))
   1. containsKey
   2. get
3. Crea un método que dado un mapa de usuarios indexados por nif, devuelva todos los teléfonos almacenados (List\<String> con los valores). (public static List\<String> getPhones(Map\<String, User> usersByNif))
   1. values()
   2. foreach
4. Crea un método que dado un mapa de usuarios indexados por nif y un nif, elimina el usuario asociado al nif.
   1. containsKey
   2. remove
5. Crea un método que dado un mapa de usuarios indexados por nif, devuelva una lista con los nif
   1. keySet() foreach
6. Crea un método que dado un mapa de usuarios indexados por nif, un nif y un teléfono, modifica el teléfono de un usuario.
   1. containsKey
   2. get
   3. put
