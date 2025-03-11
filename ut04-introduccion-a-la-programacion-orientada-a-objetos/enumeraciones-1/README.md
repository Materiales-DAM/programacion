---
cover: ../../.gitbook/assets/oop.png
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

# Fechas

`LocalDate` es una clase introducida en Java 8 dentro del paquete `java.time`. Se utiliza para representar fechas sin información de zona horaria, es decir, solo el año, mes y día. Esta clase es inmutable y segura para el uso en múltiples hilos.

### **1. Creación de un `LocalDate`**

Puedes crear una instancia de `LocalDate` de varias maneras:

#### **a) Obtener la fecha actual del sistema**

```java
LocalDate fechaActual = LocalDate.now();
System.out.println("Fecha actual: " + fechaActual);
```

#### **b) Crear una fecha específica**

```java
LocalDate fechaEspecifica = LocalDate.of(2025, 3, 11);
System.out.println("Fecha específica: " + fechaEspecifica);
```

#### **c) Crear un `LocalDate` a partir de una cadena en formato ISO-8601 (`YYYY-MM-DD`)**

```java
LocalDate fechaDesdeCadena = LocalDate.parse("2025-03-11");
System.out.println("Fecha desde cadena: " + fechaDesdeCadena);
```

***

### **2. Obtener Información de una Fecha**

Puedes extraer partes específicas de una fecha con los siguientes métodos:

```java
int año = fechaEspecifica.getYear();
int numeroMes = fechaEspecifica.getMonthValue(); // 1 para enero, 12 para diciembre
Month mes = fechaEspecifica.getMonth(); // Devuelve un enum Month
int diaMes = fechaEspecifica.getDayOfMonth();
DayOfWeek diaSemana = fechaEspecifica.getDayOfWeek(); // Devuelve un enum DayOfWeek

System.out.println("Año: " + año);
System.out.println("Número de mes: " + numeroMes);
System.out.println("Mes: " + mes);
System.out.println("Día del mes: " + diaMes);
System.out.println("Día de la semana: " + diaSemana);
```

***

### **3. Modificar Fechas**

Dado que `LocalDate` es inmutable, cualquier modificación devuelve una nueva instancia:

```java
LocalDate masCincoDias = fechaEspecifica.plusDays(5);
LocalDate menosDosMeses = fechaEspecifica.minusMonths(2);
LocalDate masUnAño = fechaEspecifica.plusYears(1);

System.out.println("Fecha +5 días: " + masCincoDias);
System.out.println("Fecha -2 meses: " + menosDosMeses);
System.out.println("Fecha +1 año: " + masUnAño);
```

***

### **4. Comparación de Fechas**

Puedes comparar fechas con estos métodos:

```java
LocalDate otraFecha = LocalDate.of(2025, 5, 15);

boolean esAntes = fechaEspecifica.isBefore(otraFecha);  // true si fechaEspecifica es anterior
boolean esDespues = fechaEspecifica.isAfter(otraFecha); // true si fechaEspecifica es posterior
boolean esIgual = fechaEspecifica.isEqual(otraFecha);   // true si son iguales

System.out.println("Es antes de otraFecha: " + esAntes);
System.out.println("Es después de otraFecha: " + esDespues);
System.out.println("Es igual a otraFecha: " + esIgual);
```

***

### **5. Formateo y Parseo de Fechas**

#### **a) Convertir un `LocalDate` a String con formato personalizado**

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
String fechaFormateada = fechaEspecifica.format(formatter);
System.out.println("Fecha formateada: " + fechaFormateada);
```

#### **b) Convertir una String a `LocalDate` con un formato personalizado**

```java
LocalDate fechaAnalizada = LocalDate.parse("11/03/2025", formatter);
System.out.println("Fecha analizada desde cadena: " + fechaAnalizada);
```

***

### **6. Ejemplo Completo**

```java
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class EjemploLocalDate {
    public static void main(String[] args) {
        // Crear una fecha específica
        LocalDate fecha = LocalDate.of(2025, 3, 11);
        System.out.println("Fecha original: " + fecha);

        // Sumar 10 días
        LocalDate nuevaFecha = fecha.plusDays(10);
        System.out.println("Fecha después de sumar 10 días: " + nuevaFecha);

        // Formatear la nueva fecha
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        String fechaFormateada = nuevaFecha.format(formatter);
        System.out.println("Fecha formateada: " + fechaFormateada);
    }
}
```

#### **Salida esperada:**

```yaml
Fecha original: 2025-03-11  
Fecha después de sumar 10 días: 2025-03-21  
Fecha formateada: 21/03/2025  
```

***

### **Conclusión**

La clase `LocalDate` de Java proporciona una forma eficiente y fácil de manejar fechas sin zona horaria. Con métodos para manipulación, comparación y formateo, facilita el trabajo con fechas en aplicaciones Java.
