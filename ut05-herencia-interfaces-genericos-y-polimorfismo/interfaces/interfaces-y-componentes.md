---
cover: ../../.gitbook/assets/image (1) (1) (1).png
coverY: 0
---

# Interfaces y componentes

En el desarrollo de componentes en Java, las interfaces desempeñan un papel fundamental al proporcionar un medio para definir contratos estándar que deben ser implementados por los componentes. Esto facilita la creación de sistemas modulares y extensibles, ya que los componentes pueden interactuar a través de interfaces comunes sin preocuparse por la implementación interna de cada componente.

Estas son las principales utilidades de los interfaces en el desarrollo de componentes:

## **Definición de contratos**

Las interfaces permiten definir contratos claros que especifican qué métodos deben ser implementados por cualquier clase que quiera actuar como un componente. Esto proporciona una especificación clara de la funcionalidad que se espera de un componente y establece un conjunto de reglas que deben seguirse.

```java
// Con este interface definimos que toda aplicación debe definir un método run
public interface App {
    void run();
}
```

## **Interoperabilidad**

Al definir interfaces comunes, los componentes pueden interactuar entre sí de manera más fácil y eficiente. Esto permite que los componentes intercambien información y servicios de manera coherente, sin depender de la implementación interna de los demás.

```java
public class AppManager {
    // Este método recibe una lista de apps y las ejecuta
    public void runAll(App[] apps) {
        for(App app: apps){
            app.run();
        }
    }
}
```

## **Implementaciones múltiples**

Un interface puede ser implementado de múltiples maneras, dependiendo de las necesidades del programa

```java
public interface AccountReader {
    Account read();
}
```

```java
// Esta implementación de AccountReader usa el Scanner para leer los datos de una cuenta
public class ScannerAccountReader implements AccountReader {
    private Scanner scanner;

    public ScannerAccountReader(Scanner scanner) {
        this.scanner = scanner;
    }
    
    @Override
    public Account read() {
        System.out.println("Introduce los datos de la cuenta:");
        System.out.println("IBAN:");
        String iban = scanner.nextLine();
        System.out.println("Saldo:");
        double balance = scanner.nextDouble();
        scanner.nextLine();

        return new Account(iban, balance);

    }
}
```

```java
// Esta implementación de AccountReader genera cuentas aleatorias
public class RandomAccountReader implements AccountReader {
    private Random random;

    public RandomAccountReader(Random random) {
        this.random = random;
    }

    @Override
    public Account read() {
        // Genera un IBAN aleatorio
        String iban = "ES" + random.nextInt();
        // Genera un saldo aleatorio
        double balance = random.nextDouble(10000);
        return new Account(iban, balance);
    }
}
```

## **Inyección de dependencias**

Las interfaces son fundamentales en patrones de diseño como la inyección de dependencias. Permite la creación de componentes que dependen de interfaces en lugar de implementaciones concretas, facilitando la sustitución de componentes y la mejora de la flexibilidad del sistema.

```java
public class AccountApp implements App {
    // El tipo de las dependencias es el interface, no las implementaciones
    private AccountReader accountReader;

    public AccountApp(AccountReader accountReader) {
        this.accountReader = accountReader;
    }

    @Override
    public void run() {
        Account account = accountReader.read();
        int opt;
        do {
            ...
            // Implementamos el menú de opciones
        } while(opt !=5 );
    }

    // ...
}
```

```java
public class RandomMain {
    public static void main(String[] args){
        Random random = new Random();
        RandomAccountReader accountReader = new RandomAccountReader(random);
        AccountApp accountApp = new AccountApp(accountReader);
        
        accountApp.run();
    }
}
```

```java
public class ScannerMain {
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        ScannerAccountReader accountReader = new ScannerAccountReader(scanner);
        AccountApp accountApp = new AccountApp(accountReader);
        
        accountApp.run();
    }
}
```

En resumen, las interfaces en Java son esenciales en el desarrollo de componentes porque permiten definir contratos claros, promover la interoperabilidad entre componentes, facilitar la inyección de dependencias y proporcionar una forma de establecer estándares en APIs y bibliotecas. Estos aspectos contribuyen a la creación de sistemas más flexibles, extensibles y mantenibles.
