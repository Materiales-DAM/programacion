---
cover: ../../.gitbook/assets/testing.jpg
coverY: 0
---

# JUnit 5

JUnit es una librería de Java que sirve para la realización de pruebas unitarias. Proporciona un entorno para escribir, organizar y ejecutar pruebas de forma automática, lo que facilita la detección de errores en el código de manera rápida y eficiente.

## Configuración

Para poder usar JUnit 5, debemos añadir la siguiente dependencia al `pom.xml`

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.13.0-M2</version>
    <scope>test</scope>
</dependency>
```

## Pruebas con JUnit

El código de las pruebas debe estar en la carpeta `src/test/java`

Todas las pruebas sobre métodos de una misma clase se suelen colocar en una misma clase de pruebas con el nombre NombreClaseAProbarTests

Por ejemplo, si vamos a probar una clase llamada `Calculator`, crearemos una clase `CalculatorTests` para realizar sus tests. Anotaremos cada método de test con la anotación `@Test`&#x20;

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Assertions;

public class CalculatorTests {

    @Test
    public void testAddition() {
        // Preparación
        Calculator calc = new Calculator();
        
        // Ejecución
        int res = calc.add(2, 2);
        
        // Aserciones
        Assertions.assertEquals(4, res);
    }

    @Test
    public void testSubtraction() {
        // Preparación
        Calculator calc = new Calculator();
        
        // Ejecución
        int res = calc.substract(4, 2);
        
        // Aserciones
        Assertions.assertEquals(2, res);
    }
}
```

Cada método con la anotación @Test se denomina escenario de test.

## Escenarios de test

Un escenario de prueba (o test scenario en inglés) es una descripción detallada de un conjunto de condiciones y acciones que deben llevarse a cabo para probar una funcionalidad específica de un sistema, aplicación o componente. Cada escenario de prueba está diseñado para validar un aspecto particular del software bajo prueba.

Cada escenario divide su ejecución en tres fases: preparación, ejecución y aserciones.

### Preparación (Setup)

En esta fase, se prepara el entorno necesario para la ejecución de la prueba. Esto puede incluir la creación de objetos, la configuración de variables, la inicialización de objetos simulados (mocks) y la configuración de cualquier estado inicial requerido para la prueba.

Ejemplos de acciones durante la fase de preparación:

* Crear instancias de las clases que se van a probar.
* Configurar el estado inicial de los objetos.
* Inicializar cualquier recurso necesario para la prueba, como bases de datos en memoria o simuladas.
* Configurar objetos simulados o mocks para simular el comportamiento de dependencias externas.

### Ejecución

Durante esta fase, se invoca el código que se está probando con los datos de entrada adecuados. Aquí es donde ocurre la acción principal que queremos probar.

### Aserciones

En esta fase, se verifica que el comportamiento o resultado de la ejecución del código coincida con lo que se espera. Se utilizan aserciones para comparar el resultado real con el resultado esperado y determinar si la prueba ha pasado o fallado.

Ejemplos de acciones durante la fase de aserciones:

* Asserts sobre el valor devuelto
* Comprobaciones de excepciones

## Tests que producen excepciones

En ocasiones, vamos a querer probar métodos cuya invocación puede resultar en que se lance una excepción. En este caso, necesitamos especificar en el test que la excepción es el comportamieno deseado.

```java
@Test
public void testZeroDividedByZero() {
    Assertions.assertThrows(
            ArithmeticException.class,
            () -> {
                int number1 = 0;
                int number2 = 0;

                int res = number1 / number2;
            }
    );
}
```
