# Ejercicios con menú interactivo

## Biblioteca



## Banco

#### BankMenuApp

Tendrá un método run() que realice los siguiente:

* Pide los datos de un banco
* Inicia un bucle de menú con las siguientes opciones
  1. Mostrar las cuentas del banco
  2. Mostrar datos de una cuenta
     * Se pide un IBAN
     * Se busca la cuenta con ese IBAN.
     * Si no existe se muestra el mensaje "No existe la cuenta", si existe se muestra todo en pantall
  3. Mostrar los datos de las cuentas de un cliente
     * Se pide un nif
     * Se recorren las cuentas comprobando si son del cliente con ese nif. Se muestran en pantalla
  4. Ingresar dinero en cuenta
     * Se pide un IBAN
     * Se pide una cantidad de dinero
     * Se busca la cuenta con el IBAN.
       * Si no existe se muestra el mensaje "No existe la cuenta"
       * Si existe se modifica el saldo, añadiendo la cantidad.
       * Se muestra la cuenta
  5. Sacar diner de una cuenta
     * Se pide un IBAN
     * Se pide una cantidad de dinero
     * Se busca la cuenta con el IBAN.
       * Si no existe se muestra el mensaje "No existe la cuenta"
       * Si hay suficiente saldo, se reduce el saldo. Si no hay suficiente saldo se muestra "Saldo insuficiente"
       * Se muestra la cuenta
  6. Contar cuentas de cliente
  7. Mostrar cliente de cuenta
  8. Realizar transferencia

## Edificio

#### BuildingMenuApp

Debe tener un método run() que haga:

* Pide los datos del edificio
* Inicia un bucle de menú con las siguientes opciones:
  * Muestra toda la información del edificio
  * Dado una planta y una puerto, devuelve el apartamento en esa planta y puerta. Si no existe dicho apartamento devuelve null.
  * Dado un número de planta, muestra los apartamentos de esa planta
  * Dado una planta y una puerto, devuelve los propietarios del apartamento de esa puerta y planta. Si no existe dicho apartamento devuelve null.
  * Muestra los datos del apartamento situado en una puerta y planta dados. Si no se encuentra muestra el mensaje "No existe el apartamento"
  * Muestra los propietarios de un apartamento situado en una planta y puerta dados. Si no se encuentra muestra el mensaje "No existe el apartamento"

## Areolínea

#### AirlineAppMenu

Tendrá un método run() que realice los siguiente:

* Pide los datos de la aerolínea
* Inicia un bucle de menú con las siguientes opciones
  1. Muestra todos los vuelos
  2. Mostrar vuelos origen:
     * Pide un origen al usuario y muestra todos los vuelos que tengan ese origen
  3. Muestra los vuelos de un pasajero:
     * Se pide un nif
     * Se recorren los vuelos comprobando si alguno de sus pasajeros tiene el NIF.
  4. Muestra asiento de pasajero
     * Se pide un flightNumber
     * Se pide un NIF
     * Se busca el vuelo y el pasajero:
       * Si no existe el vuelo se muestra "El vuelo no existe"
       * Si no se encuentra el pasajero en el vuelo se muestra "El pasajero no está registrado en el vuelo"
       * Si se encuentra el pasajero se muestra "El asiento asignado es "
  5. Cambiar asiento de pasajero
     * Se pide un flightNumber
     * Se pide un NIF
     * Se pide un seatNumber (Integer)
     * Se busca el vuelo y el pasajero:
       * Si no existe el vuelo se muestra "El vuelo no existe"
       * Si no se encuentra el pasajero en el vuelo se muestra "El pasajero no está registrado en el vuelo"
       * Si se encuentra el pasajero se le cambia el asiento y se muestra el mensaje "Asiento asignado"
