---
cover: ../../.gitbook/assets/quality-assurance-code-bug.jpg
coverY: 110.50526315789473
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

# Diseño de excepciones

Es posible definir excepciones propias de cada proyecto y lanzarlas cuando se considere adecuado.&#x20;

Todo programa está sujeto a las reglas y restricciones comunes del desarrollo. Estas reglas vienen definidas por: &#x20;

* Las reglas sintácticas y semánticas del lenguaje&#x20;
* Las reglas y restricciones en tiempo de ejecución  inherentes al lenguaje y librerías que se están usando (NullPointerException, InputMismatchException...)&#x20;

Además de estas reglas comunes, es posible definir nuevas restricciones que derivan de las reglas de negocio del programa que se está desarrollando. Una forma de llevar a cabo estas restricciones es a través del diseño de excepciones.

## Excepciones de negocio

Cuando se identifique un error que se quiera lanzar vinculado a una regla de negocio crearemos una nueva clase que extienda de `Exception`. Es posible añadir campos a las excepciones que mejoren la información del error que representan.

Por ejemplo, podríamos crear una excepción que represente el hecho de que no hemos encontrado un libro en una biblioteca

```java
public class BookNotFoundException extends Exception {
    // Añadimos un campo isbn para especificar el libro que no se ha encontrado
    private final String isbn;

    public BookNotFoundException(String isbn) {
        this.isbn = isbn;
    }

    public String getIsbn() {
        return isbn;
    }

    @Override
    public String toString() {
        return "BookNotFoundException{" +
                "isbn='" + isbn + '\'' +
                '}';
    }
}
```

## Lanzar excepciones

Después de definir nuestras excepciones, llega el momento de decidir cuando lanzarlas. Para lanzar una excepción usaremos la palabra reservada `throw` seguida de la creación de la excepción. Al ser estas excepciones checked exceptions, deberemos propagar la excepción el método que la lanza para que pueda ser capturada desde donde lo invocan.

Por ejemplo, podríamos tener la clase `Library` con un método para buscar un libro por ISBN

```java
import lombok.AllArgsConstructor;
import lombok.Data;

import java.util.Map;

@Data
@AllArgsConstructor
public class Library {
    private String name;
    private Map<String, Book> books;
    
    // Este método lanza y propaga la excepcióin BookNotFoundException
    public Book findBook(String isbn) throws BookNotFoundException {
        if(books.containsKey(isbn)) {
            return books.get(isbn);
        } else{
            // Lanzamos la excepción si no existe el libro
            throw new BookNotFoundException(isbn);
        }
    }
}
```

Y main sería

```java
package org.ies.tierno;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.Scanner;

public class Main {
    private final static Logger log = LoggerFactory.getLogger(Main.class);
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Reader<Library> libraryReader = new LibraryReader(scanner);
        Library library = libraryReader.read();
        log.info("Introduzca el ISBN que desea buscar");
        String isbn = scanner.nextLine();
        try {
            Book book = library.findBook(isbn);
            log.info(book.toString());
        } catch (BookNotFoundException e) {
            log.error("No se ha podido encontrar el libro con isbn " + e.getIsbn());
        }
    }
}
```

