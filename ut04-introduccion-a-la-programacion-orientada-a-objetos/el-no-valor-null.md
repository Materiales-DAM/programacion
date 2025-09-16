---
cover: ../.gitbook/assets/oop.png
coverY: 0
---

# Métodos de objeto

Los métodos de un objeto definen las operaciones que podemos realizar con las entidades de este tipo. Hasta ahora hemos visto métodos estáticos, también conocidos como métodos de clase, esos métodos se podían invocar sin necesidad de instanciar un objeto de la clase en la que están definidos.

Sin embargo, los métodos de objeto (no estáticos) solo se pueden invocar cuando existe un objeto de la clase en la que están definidos.

Por ejemplo, en la clase `Student` tenemos el método `sayHello`, para poder ejecutar ese método necesitamos una instancia de `Student`.

```java
// Esta sentencia no compila
Student.sayHello()

Student st = new Student();
// Esta sentencia compila
st.sayHello();
```

Algunas características de los métodos de objeto son:

* **Pueden acceder a los valores almacenados en los campos del objeto**.
* Implementan **funcionalidades vinculadas con el tipo** en el que están definidos.
* Por lo demás, la definición de métodos de objeto sigue las mismas reglas que los métodos de clase.
