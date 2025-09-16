---
cover: ../.gitbook/assets/tree.png
coverY: 94.60266666666666
---

# Ejercicios selección de colecciones

## Biblioteca

Crea un programa que maneje los datos de una biblioteca:

1. name: Nombre de la biblioteca
2. booksByIsbn: libros inexados por ISBN. Por cada libro se guardará:
   1. isbn
   2. title
   3. author
   4. genres (Set\<String>)
3. customers: socios de la biblioteca (lista). Por cada socio se guardará:
   1. nif
   2. name
   3. surname
   4. customerNumber: entero
   5. zipCode: entero
4. booklends: se almacenará un historial de préstamos (BookLend) ordenados por fecha:
   1. isbn,
   2. date,
   3. nif

## Banco

Crea una aplicación que sirva para gestionar las cuentas de los clientes de un banco. Crea una estructura de clases que permita almacenar estos datos:

1. name: Nombre del banco
2. customers: Listado de clientes. Por cada cliente:
   1. nif
   2. name
   3. surname
   4. zipCode
3. accountsByIban: cuentas indexadas por iban. Por cada cuenta
   1. iban (String)
   2. nif
   3. balance: saldo

## Tienda

Implementa una estructura de clases que permita gestionar una tienda. De la tienda se debe almacenar:

* name
* productsById: los productos deben estar indexados por id de producto. Por cada producto:
  * id: de producto (entero)
  * name
  * price: double
  * tags: conjunto no ordenado de etiquetas (cada etiqueta es un String)
* customers: Conjunto de clientes ordenados por apellidos, nombre y nif. Por cada cliente
  * nif (String)
  * name
  * surnmae
  * orders: lista de pedidos, por cada pedido:
    * id: int
    * date
    * price: double
    * items: lista de items del pedido, por cada item:
      * productId: entero
      * amount
