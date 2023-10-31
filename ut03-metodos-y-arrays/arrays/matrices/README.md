---
cover: >-
  https://images.unsplash.com/photo-1488229297570-58520851e868?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw1fHxtYXRyaXh8ZW58MHx8fHwxNjk4NzUyMjE2fDA&ixlib=rb-4.0.3&q=85
coverY: 0
layout:
  cover:
    visible: true
    size: full
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

# Matrices

Es posible crear arrays de múltiples dimensiones, estos arrays de arrays se denominan matrices.

```java
public class MatrixExample {

    public static void main(String[] args) {

        String[][] tresEnRaya = {
                {null, null, null},
                {null, null, null},
                {null, null, null},
        };

        tresEnRaya[0][0] = "X";
        tresEnRaya[0][1] = "O";
        tresEnRaya[2][1] = "X";

        for (int i = 0; i < tresEnRaya.length; i++) {
            String[] columns = tresEnRaya[i];
            for (int j = 0; j < columns.length; j++) {
                String cellValue = tresEnRaya[i][j];
                System.out.print(cellValue + " ");
            }
            System.out.println();
        }
    }
}

```
