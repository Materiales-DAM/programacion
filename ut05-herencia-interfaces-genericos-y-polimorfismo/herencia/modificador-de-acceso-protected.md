---
cover: ../../.gitbook/assets/image (8).png
coverY: 0
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

# Modificador de acceso protected

En Java, el modificador de acceso `protected` desempeña un papel clave en el contexto de la herencia, permitiendo que los miembros de una clase sean accesibles por las clases derivadas (subclases) y por otras clases del mismo paquete. Aquí hay una explicación detallada del uso del modificador `protected` en la herencia:

## **Acceso a miembros protected**

Cuando un miembro (método o campo) de una clase tiene el modificador `protected`, ese miembro es accesible desde:

* &#x20;Las clases derivadas (subclases) independientemente del paquete.
* Desde todas clases dentro del mismo paquete, independientemente de si son subclases o no.

```java
package org.ies.ejemplo;

public class ClaseBase {
    protected int variableProtegida;

    protected void metodoProtegido() {
        // Implementación
    }
}
```

```java
package org.ies.otro_paquete;

public class SubClase extends ClaseBase {
    void otroMetodo() {
        variableProtegida = 10;  // Acceso a la variable protegida
        metodoProtegido();       // Acceso al método protegido
    }
}
```



```java
package org.ies.ejemplo;

public class OtraClase {
    void ejemplo() {
        ClaseBase subClase = new ClaseBase();
        subClase.variableProtegida = 20;  // Acceso a la variable protegida
        subClase.metodoProtegido();       // Acceso al método protegido
    }
}
```



<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

