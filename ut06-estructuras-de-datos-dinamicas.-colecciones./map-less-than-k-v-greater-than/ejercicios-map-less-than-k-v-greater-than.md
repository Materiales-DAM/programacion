---
cover: ../../.gitbook/assets/tree.png
coverY: 94.60266666666666
layout:
  cover:
    visible: true
    size: hero
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

# Ejercicios Map\<K, V>

## User

```java
import java.util.Objects;

public class User {
    private String nif;

    private String name;
    private String surname;
    private String phoneNumber;
    private String email;
    private int age;

    public User(String nif, String name, String surname, String phoneNumber, String email, int age) {
        this.nif = nif;
        this.name = name;
        this.surname = surname;
        this.phoneNumber = phoneNumber;
        this.email = email;
        this.age = age;
    }

    public String getNif() {
        return nif;
    }

    public void setNif(String nif) {
        this.nif = nif;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSurname() {
        return surname;
    }

    public void setSurname(String surname) {
        this.surname = surname;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        User user = (User) o;

        if (age != user.age) return false;
        if (!Objects.equals(nif, user.nif)) return false;
        if (!Objects.equals(name, user.name)) return false;
        if (!Objects.equals(surname, user.surname)) return false;
        if (!Objects.equals(phoneNumber, user.phoneNumber)) return false;
        return Objects.equals(email, user.email);
    }

    @Override
    public int hashCode() {
        int result = nif != null ? nif.hashCode() : 0;
        result = 31 * result + (name != null ? name.hashCode() : 0);
        result = 31 * result + (surname != null ? surname.hashCode() : 0);
        result = 31 * result + (phoneNumber != null ? phoneNumber.hashCode() : 0);
        result = 31 * result + (email != null ? email.hashCode() : 0);
        result = 31 * result + age;
        return result;
    }

    @Override
    public String toString() {
        return "User{" +
                "nif='" + nif + '\'' +
                ", name='" + name + '\'' +
                ", surname='" + surname + '\'' +
                ", phoneNumber='" + phoneNumber + '\'' +
                ", email='" + email + '\'' +
                ", age=" + age +
                '}';
    }
}

```

1. Escribe un programa que almacene los datos de los estudiantes. Indexa los usuarios por el nif del usuario. Inserta varios usuarios con sus teléfonos.
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
   1. KeySet() foreach
6. Crea un método que dado un mapa de usuarios indexados por nif, un nif y un teléfono, modifica el teléfono de un usuario.
   1. containsKey
   2. get
   3. Put
