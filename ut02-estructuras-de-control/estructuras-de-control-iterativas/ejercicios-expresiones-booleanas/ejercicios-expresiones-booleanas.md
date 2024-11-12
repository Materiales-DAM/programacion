# Soluciones expresiones booleanas

1. Si tengo dos números: number1 y number2 escribe las siguientes expresiones booleanas:
   1. number1 es mayor o igual que number2\
      `number1 >= number2`
   2. number1 es divisible entre dos y number2 es mayor que cero\
      `number1 % 2 == 0 && number2 > 0`
   3. number2 es 100 veces mayor que number1\
      `number2 > number1 * 100`
   4. number1 es positivo o number2 es menor que number1\
      `number1 >= 0 || number2 < number1`
2. Si tengo dos variables number (int) y answer (String), escribe las siguientes expresiones booleanas:
   1. answer es "Hola" y number es mayor que cero\
      answer.equals("Hola") && number > 0
   2. number es negativo o answer es distinto de "N"\
      `number < 0 || !answer.equals("N")`
   3. number es distinto de cero y answer es "S"\
      `number != 0 && answer.equals("S")`
