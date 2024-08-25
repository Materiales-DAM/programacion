---
hidden: true
cover: ../../../.gitbook/assets/java.jpeg
coverY: 0
---

# String

Este tipo se utiliza para almacenar cadenas de texto. A diferencia de los tipos primitivos, los String son objetos por lo que algunas operaciones se deben realizar de una manera diferente.

### Comparar String

Para ver si dos String son iguales debemos usar el método equals

```java
// Some code
String myString = "Some value";

// Esto funciona bien
boolean areSameString = myString.equals("Some other value");

// Esto no funciona bien
boolean areSameString2 = myString == "Some other value";
```

### Otros métodos

| Method                                                                                 | Description                                                                            | Return Type |
| -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ----------- |
| [charAt()](https://www.w3schools.com/java/ref\_string\_charat.asp)                     | Returns the character at the specified index (position)                                | char        |
| [concat()](https://www.w3schools.com/java/ref\_string\_concat.asp)                     | Appends a string to the end of another string                                          | String      |
| [contains()](https://www.w3schools.com/java/ref\_string\_contains.asp)                 | Checks whether a string contains a sequence of characters                              | boolean     |
| [endsWith()](https://www.w3schools.com/java/ref\_string\_endswith.asp)                 | Checks whether a string ends with the specified character(s)                           | boolean     |
| [equals()](https://www.w3schools.com/java/ref\_string\_equals.asp)                     | Compares two strings. Returns true if the strings are equal, and false if not          | boolean     |
| [equalsIgnoreCase()](https://www.w3schools.com/java/ref\_string\_equalsignorecase.asp) | Compares two strings, ignoring case considerations                                     | boolean     |
| [indexOf()](https://www.w3schools.com/java/ref\_string\_indexof.asp)                   | Returns the position of the first found occurrence of specified characters in a string | int         |
| [isEmpty()](https://www.w3schools.com/java/ref\_string\_isempty.asp)                   | Checks whether a string is empty or not                                                | boolean     |
|                                                                                        |                                                                                        |             |

| [lastIndexOf()](https://www.w3schools.com/java/ref\_string\_lastindexof.asp) | Returns the position of the last found occurrence of specified characters in a string                             | int       |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------- |
| [length()](https://www.w3schools.com/java/ref\_string\_length.asp)           | Returns the length of a specified string                                                                          | int       |
| [replace()](https://www.w3schools.com/java/ref\_string\_replace.asp)         | Searches a string for a specified value, and returns a new string where the specified values are replaced         | String    |
| replaceFirst()                                                               | Replaces the first occurrence of a substring that matches the given regular expression with the given replacement | String    |
| replaceAll()                                                                 | Replaces each substring of this string that matches the given regular expression with the given replacement       | String    |
| split()                                                                      | Splits a string into an array of substrings                                                                       | String\[] |
| [startsWith()](https://www.w3schools.com/java/ref\_string\_startswith.asp)   | Checks whether a string starts with specified characters                                                          | boolean   |

| Method                                                                       | Description                                                                                                                   | Return Type |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------- |
| substring()                                                                  | Extracts the characters from a string, beginning at a specified start position, and through the specified number of character | String      |
| [toLowerCase()](https://www.w3schools.com/java/ref\_string\_tolowercase.asp) | Converts a string to lower case letters                                                                                       | String      |
| [toUpperCase()](https://www.w3schools.com/java/ref\_string\_touppercase.asp) | Converts a string to upper case letters                                                                                       | String      |
| [trim()](https://www.w3schools.com/java/ref\_string\_trim.asp)               | Removes whitespace from both ends of a string                                                                                 | String      |
