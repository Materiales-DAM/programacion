---
cover: ../.gitbook/assets/tree.png
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

# Ejercicios colecciones

## Biblioteca

Implementar los métodos en Biblioteca :

* Dado un género, devuelve todos los libros que tengan ese género (List\<Book>).
  * Add
  * foreach
  * Contains
* Dado un código postal, devuelve los socios que viven ahí (List\<Customer>)
  * Add
  * foreach
* Dado un nif y un ISBN, crea un préstamo para un socio. Crea un BookLend con la fecha actual.
  * Add
* Dado un ISBN y un género, elimina el género del libro
  * containsKey
  * get
  * remove
* Dado un ISBN y un número de socio (no NIF), devuelve si el socio ha tomado prestado el libro o no (boolean).
  * Foreach
* Dado un ISBN, devuelve los géneros del libro. Si no existe el libro, devuelve null.
* Dado un ISBN, devuelve todos los préstamos de ese libro. Si no existe el libro, devuelve null.

## Banco

El banco debe permitir realizar las siguientes operaciones:

* Dado un iban y una cantidad, ingresar la cantidad en la cuenta. Si no existe la cuenta muestra en la consola el mensaje "No existe la cuenta".
* Dado un nif, devolver todas las cuentas de ese cliente. Si el cliente no existe devuelve null.
* Dado un iban y una cantidad, saca la cantidad en la cuenta, si no hay suficiente saldo muestra el mensaje "No hay saldo suficiente". Si no existe la cuenta muestra en la consola el mensaje "No existe la cuenta".&#x20;
* Realizar una transferencia entre dos cuentas de dos clientes. Para realizar la transferencia será necesario proporcionar la cantidad, el iban de cuenta de origen y de destino. Si no existe la cuenta origen muestra "No existe la cuenta origen", si no existe la cuenta destino "No existe la cuenta destino", si no hay saldo suficiente en la cuenta de origen muestra "No hay saldo suficiente en origen".
* Dado un código postal, devuelve todas las cuentas cuyo propietario vive en ese código postal

## Tienda

Implementa los siguientes métodos en la clase Shop:

* Dado un nif, devuelve el cliente con ese NIF.
* Dado un nif y un id de pedido, devuelve el pedido del cliente.
* Dado un nif y un id de pedido, devuelve una lista con los productos que se han pedido.
* Dado una etiqueta (String), devuelve una lista de productos que tienen esa etiqueta.
* Dado un nif, devuelve cuánto se ha gastado el cliente en la tienda.
