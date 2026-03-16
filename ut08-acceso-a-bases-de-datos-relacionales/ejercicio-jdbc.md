---
cover: ../.gitbook/assets/jdbc.jpeg
coverY: 0
layout:
  width: default
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
  metadata:
    visible: true
  tags:
    visible: true
---

# Ejercicio JDBC

### Proyectos <a href="#proyectos" id="proyectos"></a>

<p align="center"><img src="https://fp-informatica.gitbook.io/acceso-a-datos/~gitbook/image?url=https%3A%2F%2F2165140154-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fz960MwFGHtc3ewEBRynf%252Fuploads%252Fm1Rw9OMknkzGVxy46goD%252Fimage.png%3Falt%3Dmedia%26token%3D482d3d05-02b0-45c2-9982-c0f1c966dc03&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=2ce7ca14&#x26;sv=2" alt=""></p>

```sql
DROP SCHEMA IF EXISTS Proyectos;
CREATE DATABASE Proyectos ;
USE Proyectos;
CREATE TABLE Empleado(
	Id INT PRIMARY KEY AUTO_INCREMENT,
	Nombre VARCHAR(30) NOT NULL,
	Apellidos VARCHAR(30) NOT NULL,
	Rol VARCHAR(10) NOT NULL
);
CREATE TABLE Proyecto(
	Id INT PRIMARY KEY AUTO_INCREMENT,
	Nombre VARCHAR(30) NOT NULL
);
CREATE TABLE Tarea(
	Id INT PRIMARY KEY AUTO_INCREMENT,
	Nombre VARCHAR(30) NOT NULL,
	Id_Empleado INT NOT NULL,
	Id_Proyecto INT NOT NULL,
	CONSTRAINT fk_Tarea_Empleado
	FOREIGN KEY (Id_Empleado)
	REFERENCES Empleado(Id)
	ON DELETE RESTRICT
    ON UPDATE CASCADE,
    CONSTRAINT fk_Tarea_Proyecto
	FOREIGN KEY (Id_Proyecto) 
	REFERENCES Proyecto(Id)
	ON DELETE CASCADE
    ON UPDATE CASCADE
); 
```

1. Haz un programa con los siguientes componentes:
   1. EmployeeReader: define un método Employee read(), que pide al usuario los datos de un empleado usando el Scanner y lo devuelve
   2. EmployeeDao: esta clase va a definir métodos para leer/modificar empleados
      1. void insert(Employee employee): inserta el empleado en la base de datos
      2. List\<Employee> list(): lista todos los empleados de la base de datos
      3. void delete(int employeeId): elimina el empleado con el id del parámetro
   3. ProjectDao:
      1. void insert(Project project): inserta el proyecto en la base de datos
      2. List\<Project> list(): lista todos los proyectos de la base de datos
   4. TaskDao:
      1. void insert(Task task): inserta la tarea en la base de datos
      2. List\<Task> listEmployeeTasks(int employeeId): lista las tareas del empleado con el id proporcionado
