# Ejercicios acceso a bases de datos

## Instituto

Crea un programa que imprima el siguiente menú de opciones:

* Listar estudiantes: muestra todos los estudiantes en la base de datos
* Inserta estudiante: pide al usuario los datos de un estudiante y lo inserta en la base de datos.
* Elimina estudiante: pide al usuario un nif y lo elimina de la base de datos. Si el estudiante no existía, muestra el mensaje "No se ha podido encontrar el estudiante"
* Modificar estudiante: pide al usuario un nif, un nombre, apellidos y zipCode. Modifica el usuario con ese nif, actualizándole el nombre, apellidos y zipCode. Si no existe el estudiante  muestra el mensaje "No se ha podido encontrar el estudiante".
* Listar cursos: muestra todos los cursos en la base de datos
* Inserta curso: pide al usuario los datos de un curso y lo inserta en la base de datos.
* Elimina curso: pide al usuario un id de curso y lo elimina de la base de datos. Si el curso no existía, muestra el mensaje "No se ha podido encontrar el curso"
* Muestra notas de estudiante: dado un nif, muestra las notas del estudiante
* Añade nota: pide al usuario un nif, un id de curso y una nota y lo inserta en la base de datos.

```java
package org.ies.tierno.model;

import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class Student {
    private String nif;
    private String name;
    private String surname;
    private int zipCode;
}
```

El script de creación de la base de datos es

```sql
DROP DATABASE IF EXISTS highschool;
CREATE DATABASE highschool;
USE highschool;

CREATE TABLE student(
    nif VARCHAR(10) PRIMARY KEY,
    name VARCHAR(30) NOT NULL,
    surname VARCHAR(30) NOT NULL,
    zipCode INT NOT NULL
);

CREATE TABLE course(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    course_year INT
);

CREATE TABLE student_grade(
    nif VARCHAR(10) NOT NULL,
    course_id INT NOT NULL,
    grade INT NOT NULL,
    PRIMARY KEY(nif, course_id),
    CONSTRAINT fk_student_grade_student
    FOREIGN KEY (nif)
    REFERENCES student(nif),
    CONSTRAINT fk_student_grade_course
    FOREIGN KEY (course_id)
    REFERENCES course(id)
);

INSERT INTO student(nif, name, surname, zipCode)
VALUES ('1X', 'Bob', 'Esponja', 28000);

INSERT INTO student(nif, name, surname, zipCode)
VALUES ('2X', 'Peppa', 'Pig', 28001);

INSERT INTO course(name, course_year) VALUES('DAM', 2024);
INSERT INTO course(name, course_year) VALUES('DAW', 2024);

INSERT INTO student_grade(nif, course_id, grade)
VALUES('1X', 1, 7);

INSERT INTO student_grade(nif, course_id, grade)
VALUES('2X', 2, 5);
```



## Library-db

```sql
CREATE DATABASE IF NOT EXISTS library;
USE library;

-- --------------------------------------------------------
-- DDL
-- --------------------------------------------------------

CREATE TABLE author (
    nif        VARCHAR(20)  NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name  VARCHAR(150) NOT NULL,
    CONSTRAINT pk_author PRIMARY KEY (nif)
);

CREATE TABLE book (
    isbn       VARCHAR(20)  NOT NULL,
    title      VARCHAR(255) NOT NULL,
    year       INT          NOT NULL,
    author_nif VARCHAR(20)  NOT NULL,
    CONSTRAINT pk_book        PRIMARY KEY (isbn),
    CONSTRAINT fk_book_author FOREIGN KEY (author_nif) REFERENCES author(nif)
);

CREATE TABLE member (
    nif        VARCHAR(20)  NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name  VARCHAR(150) NOT NULL,
    CONSTRAINT pk_member PRIMARY KEY (nif)
);

CREATE TABLE book_lend (
    member_nif VARCHAR(20) NOT NULL,
    isbn       VARCHAR(20) NOT NULL,
    lend_date  DATE        NOT NULL,
    CONSTRAINT pk_book_lend        PRIMARY KEY (member_nif, isbn, lend_date),
    CONSTRAINT fk_book_lend_member FOREIGN KEY (member_nif) REFERENCES member(nif),
    CONSTRAINT fk_book_lend_book   FOREIGN KEY (isbn)       REFERENCES book(isbn)
);

-- --------------------------------------------------------
-- DML
-- --------------------------------------------------------

INSERT INTO author (nif, first_name, last_name) VALUES
    ('11111111A', 'George',    'Orwell'),
    ('22222222B', 'J.K.',      'Rowling'),
    ('33333333C', 'Frank',     'Herbert'),
    ('44444444D', 'Tolkien',   'J.R.R.'),
    ('55555555E', 'Agatha',    'Christie');

INSERT INTO book (isbn, title, year, author_nif) VALUES
    ('978-0451524935', 'Nineteen Eighty-Four',          1949, '11111111A'),
    ('978-0452284234', 'Animal Farm',                   1945, '11111111A'),
    ('978-0439708180', 'Harry Potter and the Sorcerer', 1997, '22222222B'),
    ('978-0441013593', 'Dune',                          1965, '33333333C'),
    ('978-0618640157', 'The Lord of the Rings',         1954, '44444444D'),
    ('978-0062073488', 'Murder on the Orient Express',  1934, '55555555E');

INSERT INTO member (nif, first_name, last_name) VALUES
    ('66666666F', 'Alice',   'Smith'),
    ('77777777G', 'Bob',     'Johnson'),
    ('88888888H', 'Carol',   'Williams'),
    ('99999999I', 'David',   'Brown'),
    ('10101010J', 'Eva',     'Jones');

INSERT INTO book_lend (member_nif, isbn, lend_date) VALUES
    ('66666666F', '978-0451524935', '2024-01-10'),
    ('66666666F', '978-0441013593', '2024-03-05'),
    ('77777777G', '978-0439708180', '2024-02-14'),
    ('77777777G', '978-0618640157', '2024-02-20'),
    ('88888888H', '978-0452284234', '2024-03-01'),
    ('99999999I', '978-0062073488', '2024-03-15'),
    ('10101010J', '978-0451524935', '2024-04-02'),
    ('10101010J', '978-0439708180', '2024-04-10');
```

### POJOs

#### Book

* ISBN: String
* Titulo: String
* Año: int
* AutorNif: String

#### Autor

* Nif
* Nombre
* Apellidos

#### Member

* Nif
* Nombre
* Apellidos

BookLend

* MemberNif
* isbn
* lendDate: Date

### Componentes

#### BookDAO

* Insertar, listar, eliminar

#### AuthorDAO

* Insertar, listar, eliminar

#### MemberDAO

* Insertar, listar, eliminar

#### BookLendDAO

* Insertar, listar, eliminar

#### LibraryApp

Debe implementar un bucle con las siguientes opciones:

* Listar libros
* Insertar libro
* Ver autores
* Insertar autor
* Ver autor de libro
* Ver libros de autor
* Ver socios
* Insertar socio
* Ver préstamos socio
* Ver prestamos libro
* Añadir nuevo préstamo

## Airline

```sql
-- Crear la base de datos
CREATE DATABASE airline CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE airline;

-- Crear la tabla Flight
CREATE TABLE Flight (
    number INT PRIMARY KEY,
    origin VARCHAR(100) NOT NULL,
    destination VARCHAR(100) NOT NULL,
    date DATE NOT NULL,
    airline VARCHAR(100) NOT NULL
);

-- Crear la tabla Passenger
CREATE TABLE Passenger (
    ticketNumber VARCHAR(20) PRIMARY KEY,
    nif VARCHAR(20) NOT NULL,
    flightNumber INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    surname VARCHAR(100) NOT NULL,
    seatNumber INT NOT NULL,
    CONSTRAINT fk_flight FOREIGN KEY (flightNumber) REFERENCES Flight(number)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Crear la tabla Luggage
CREATE TABLE Luggage (
    id INT AUTO_INCREMENT PRIMARY KEY,
    ticketNumber VARCHAR(20) NOT NULL,
    description TEXT,
    CONSTRAINT fk_passenger FOREIGN KEY (ticketNumber) REFERENCES Passenger(ticketNumber)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

```

### POJOs

#### Flight

* number: Integer
* origin: String
* destination: String
* date: LocalDate
* airline: String

#### Passenger

* ticketNumber: String
* nif
* flightNumber: Integer
* name
* surname
* seatNumber: Integer

#### Luggage (equipaje)

* id
* ticketNumber
* description

### Componentes

#### FlightDAO

* Insertar, listar, eliminar

#### PassengerDAO

* Insertar, listar, eliminar

#### LuggageDAO

* Insertar, listar, eliminar

#### AirlineApp

Debe implementar un bucle con las siguientes opciones:

* Listar vuelos
* Listar vuelos origen
* Listar vuelos destino
* Insertar vuelo
* Ver pasejeros vuelo
* Insertar pasajero
* Eliminar pasajero
* Ver equipaje de pasajero
* Añadir equipaje
* Eliminar equipaje

Script SQL
