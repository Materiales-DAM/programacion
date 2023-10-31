# Solucinoes

1\.



```java
public class Ej1 {

    public static int max(int[] numbers) {
        int max = numbers[0];
        for (int i = 0; i < numbers.length; i++) {
            if(numbers[i] > max) {
                max = numbers[i];
            }
        }

        return max;
    }

    public static void printMax(int value) {
        System.out.println("El máximo es " + value);
    }

    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 0};
        int max = max(numbers);
        printMax(max);
    }
}

```
