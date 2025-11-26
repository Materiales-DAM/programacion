# Ejercicios métodos de objeto

## Biblioteca

Crea los siguientes métodos de objeto:

* Book:
  * hasAuthor(nif): Dado un nif devuelve si el libro tiene ese autor
* Autor:
  * showInfo(): Muestra la información del autor
* Biblioteca:
  * hasBook(isbn): dado un ISBN devuelve si el libro existe en la biblioteca
  * hasAuthor(authorNif): dado un NIF devuelve si hay algún libro de ese autor
  * countBooks(authroNif): dado un NIF devuelve el número de libros del autor
  * countYearBooks(year): dado un año, devuelve el número de libros de ese año.
  * findBook(isbn): dado un ISBN, devuelve el libro con ese ISBN. Si no lo encuentra, devuelve null

Modifica el Main para que realice lo siguiente:

* Crea los reader:
* Lee una biblioteca con el LibraryReader
* Comprueba si en la biblioteca está el libro  con ISBN 1001, usando el método hasBook:
  * Si existe el libro:
    * Busca el libro con el método findBook
    * Muestra la información del libro
  * Si no existe,  muestra "Libro no encontrado"
* Comprueba si hay algún libro del autor con NIF "001X" (usa el método hasAuthor):
  * Si hay libros de ese autor, cuenta los libros del autor con NIF "001X" y el mensaje "El autor 000X tiene X libros", siendo X el número de libros
  * Si no hay libros de ese autor muestra el mensaje "No se han encontrado libros del autor"

## Banco

* Cliente
  * showInfo()
* Cuenta:
  * showInfo()
  * deposit(amount): dado una cantidad ingresa esa cantidad en la a cuenta
  * withdraw(amount): dado una cantidad saca el dinero de la cuenta. Si no hay suficiente saldo muestra un mensaje de error y no modifica el saldo.
* Bank:
  * Mostrar todas las cuentas del banco (IBAN, saldo y NIF del cliente)
  * Dado un IBAN, mostrar la información de la cuenta con ese IBAN.
  * Dado un IBAN, devuelve la cuenta con ese IBAN.
  * Dado un NIF, mostrar todas las cuentas del cliente con ese NIF
  * Dado un IBAN y una cantidad de dinero, ingresar esa cantidad en la cuenta con ese IBAN. Si no se encuentra la cuenta con ese IBAN muestra el mensaje "No se encuentra la cuenta"
  * Dado un NIF, devuelve el numero de cuentas de ese cliente
  * Dado un IBAN, devuelve los datos del cliente al que pertenece la cuenta. Si no existe la cuenta, devuelve null
  * Dados dos IBAN y una cantidad de dinero, realiza una transferencia desde la cuenta con el primer IBAN a la cuenta con el segundo IBAN. Si una de las cuentas no existo o no hay suficiente saldo en la cuenta de origen no se realiza la trasnferencia y se muestra un error explicando el problema

#### BankApp1

Tendrá un método run() que realice lo siguiente:

* Pide un banco usando BankReader
* Busca la cuenta con IBAN "ES0001".
  * Si no existe muestra "La cuenta no existe"
  * Si existe, hace un deposito en la misma de 500
* Busca otra cuenta con IBAN "ES0002"
  * Si no existe muestra "La cuenta no existe"
  * Si existe, saca 30 euros
* Haz una trasnferencia de 500 euros desde "ES0001" a "ES0002"
* Muestra en pantalla la información de la cuenta "ES0001"
* Muestra en pantalla la información de la cuenta "ES0002"

#### BankApp2

Tendrá un método run() que realice lo siguiente:

* Pide un banco usando BankReader
* Muestra todas las cuentas del banco
* Saca 50 de la cuenta ES0003
* Muestra las cuentas del cliente con NIF 000X
* Mete 300 en la cuenta ES004
* Muestra los datos del titular de la cuenta ES0001

#### BankApp3

Tendrá un método run() que realice lo siguiente:

* Pide un banco usando BankReader
* Busca la cuenta con IBAN ES0001
  * Si no existe la cuenta muestra un mensaje de error
  * Si existe:
    * Muestra los datos de la cuenta
    * Haz una transferencia de todo el dinero de la cuenta ES0001 a la cuenta ES0002
    * Muestra la información del banco

## Edificio

* Edificio:
  * showInfo()
  * findApartment(int floor, String door): Dado una planta y una puerta, devuelve el apartamento en esa planta y puerta. Si no existe dicho apartamento devuelve null.
  * countApartmentOwners(int floor, String door): Dado una planta y una puerta, devuelve el número de propietarios del departamento. Si no existe el departamento, devuelve null
  * showFloorApartments(int floor): Dado un número de planta, muestra los apartamentos de esa planta
  * findOwners(int floor, String door): Dado una planta y una puerta, devuelve los propietarios del apartamento de esa puerta y planta. Si no existe dicho apartamento devuelve null.
* Apartamento:
  * showInfo()
* Propietario:
  * showInfo()

#### BuildingApp1

Tendrá un método run() que realice lo siguiente:

* Lee un edificio&#x20;
* Pide al usuario una planta y una puerta
* Busca el apartamento de en el planta y puerta que ha pasado el usuario
  * Si existe, muestra su información
  * Si no existe muestra el mensaje "No se ha encontrado el apartamento"
* Después, muestra la información de los apartamentos de la segunda planta

## Aerolínea

* Pasajero:
  * showInfo()
* Vuelo:
  * showInfo()
  * hasPassenger(String nif): devuelve true si el pasajero está en el vuelo y false si no lo está
  * findPassenger(String nif): busca el pasajero en el vuelo y lo devuelve, si no existe devuelve null
* Aerolínea:
  * showFlights()
  * showFlightsFromOrigin(String origin)
  * findFlight(int flightNumber): busca el vuelo y lo devuelve, si no existe devuelve null
  * showPassengerFlights(String nif): muestra todos los vuelos donde haya un pasajero con el nif del parámetro
  * getPassengerSeat(int flightNumber, String nif): Devuelve el asiento del pasajero en el vuelo, si no existe el vuelo o el pasajero, devuelve null
  * updateSeatNumber(int flightNumber, String nif, int seatNumber): busca el pasajero en el vuelo, si existe le cambia el asiento. Si no existe el vuelo o el pasajero muestra mensajes de error.

#### AirlineApp1

Tendrá un método run() que realice los siguiente:

* Pide los datos de la aerolínea
* Pide al usuario un número de vuelo
* Busca el vuelo con ese número de vuelo
  * Si no existe muestra por pantalla un error
  * Si existe:
    * Pide al usuario el nif de un pasajero.
    * Busca a ese pasajero dentro del vuelo:
      * Si existe:
        * Muestra los datos del pasajero
        * Pide un número de asiento
        * Cambia el asiento del pasajeor
      * Si no existe muestra un mensaje de error
