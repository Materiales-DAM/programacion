# Ejercicios métodos de objeto



1.  ## Instituto OOP




2.  ## Taller OOP




3.  ## Biblioteca

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
    * Comprueba si en la biblioteca está el libro  con ISBN "001", usando el método hasBook:
      * Si existe el libro:
        * Busca el libro con el método findBook
        * Muestra la información del libro
      * Si no existe,  muestra "Libro no encontrado"
    * Comprueba si hay algún libro del autor con NIF "001X" (usa el método hasAuthor):
      * Si hay libros de ese autor, cuenta los libros del autor con NIF "001X" y el mensaje "El autor 000X tiene X libros", siendo X el número de libros
      * Si no hay libros de ese autor muestra el mensaje "No se han encontrado libros del autor"
4. ## Banco
   * Bank:
     * Nombre del banco
     * Cuentas
   * Cuenta:
     * IBAN
     * Saldo: double
     * Cliente
   * Cliente:
     * NIF
     * Nombre
     * Apellidos
5. ## Edificio
   * Edificio:
     * Dirección
     * Municipio
     * Apartamentos
   * Apartamento:
     * Planta: int
     * Puerta: String
     * propietarios
   * Propietario:
     * NIF
     * Nombre
     * Apellidos
6. ## Areolínea
   * Aerolínea:
     * Nombre
     * Vuelos
   * Vuelo:
     * Número de vuelo: int
     * Origen
     * Destino
     * Puerta de embarque
     * Pasajeros
   * Pasajero:
     * NIF
     * Nombre
     * Apellidos
     * Asiento
