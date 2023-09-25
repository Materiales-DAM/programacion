# Soluciones

1\.



```java
import java.util.Scanner;

public class StringExamples {

    public static void main(String[] args) {

        // int
        // double
        // boolean
        // float
        // long
        // char

        // String

        Scanner scanner = new Scanner(System.in);
        System.out.println("Introduce la hora");
        int hour = scanner.nextInt();

        switch (hour) {
            case 0:
            case 1:
            case 2:
            case 3:
            case 4:
            case 5:
            case 21:
            case 22:
            case 23:
                System.out.println("Buenas noches");
                break;
            case 6:
            case 7:
            case 8:
            case 9:
            case 10:
            case 11:
            case 12:
                System.out.println("Buenos días");
                break;
            case 13:
            case 14:
            case 15:
            case 16:
            case 17:
            case 18:
            case 19:
            case 20:
                System.out.println("Buenas tardes");
                break;
            default:
                System.out.println("Hora inválidad, debe estar entre 0 y 23");
        }
    }
}

```
