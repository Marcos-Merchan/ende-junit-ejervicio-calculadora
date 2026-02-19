# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

**1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?**

Este proyecto serviría para probar los métodos que tiene la calculadora como sumar, restar, multiplicar y dividir. En este caso las de sumar.

**2. Revisa las pruebas de la suma y comenta lo que te parezca de interés**

Una vez realizadas las pruebas el método sumarPositivosMal() da error porque el valor esperado es incorrecto.

**3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.**

Pruebas de caja negra para la división con diferentes casos:
1. División de dos números positivos (10 / 2 = 5)
1. División de un número positivo por un número negativo (10 / -2 = -5)
1. División de dos números negativos (-10 / -2 = 5)
1. División de cero por un número (0 / 10 = 0)
1. División de un número por cero (10 / 0) -> este caso llamaríaa al método dividirPorZeroException.
1. División de cero por cero (0 / 0) -> este caso tambien llamaría al método dividirPorZeroException.

Implementación de las pruebas en junit:
```java
@Test
void dividir() {
    assertAll("División",
            () -> assertEquals(5, Calculadora.dividir(10, 2), "10 / 2 = 5"),
            () -> assertEquals(-5, Calculadora.dividir(10, -2), "10 / -2 = -5"),
            () -> assertEquals(-5, Calculadora.dividir(-10, 2), "-10 / 2 = -5"),
            () -> assertEquals(5, Calculadora.dividir(-10, -2), "-10 / -2 = 5"),
            () -> assertEquals(0, Calculadora.dividir(0, 10), "0 / 10 = 0")
    );
}
@Test
void dividirPorZero() {
    var ex = assertThrows(OperacionNoValidaException.class, () -> Calculadora.dividir(10, 0), "La división por cero no está permitida");
    assertEquals(OperacionNoValidaException.MSG, ex.getMessage());
}
```




## Instrucciones

El alumno deberá hacer un fork de este proyecto, poner el repositorio como **privado**, agregar al profesor como colaborador (julparper) e implementar la solución solicitada (preguntas y código).

>Se deberá utilizar este fichero, y los artefactos de código del proyecto, para resolver el ejercicio.


**Si no se puede acceder al repositorio la evaluación del ejercicio será de 0. No se evaluarán entregas modificadas/entregadas fuera del plazo establecido en la tarea**