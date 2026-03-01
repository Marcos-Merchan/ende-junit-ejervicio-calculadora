# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

**1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?**

Sentido del proyecto:

Sirve comprobar que el código funciona bien en todos los casos posibles, evitando errores en producción.

Se podría usar para:

- Detectar errores automáticamente ahorrando tiempo.
- Asegurar que cambios futuros en el código no rompan funcionalidades existentes.
- Garantizar que el programa funciona correctamente.

**2. Revisa las pruebas de la suma y comenta lo que te parezca de interés**

- sumarPositivos(): Prueba que valida que 2+3=5
- sumarPositivosMal(): Prueba que falla a propósito por una suma incorrecta: 2+3=4
- sumar(): Usa `assertAll()` para hacer probar varios casos en una sola prueba.


**3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.**

Tenemos 2 entradas: dividendo y divisor. 
El resultado esperado es el cociente de la división.

Valores límites:

|Variable|Clase|Descripción|
|-|-|-|
|`dividendo`|= 0|dividendo cero|
||> 0|positivo|
||< 0|negativo|
|`divisor`|= 0|ERROR|
||> 0|positivo|
||< 0|negativo|

Producto cartesiano:

|dividendo \ divisor|0|2|-2|5|
|-|-|-|-|-|
|**0**|ERROR|0|0|0|
|**1**|ERROR|0|0|0|
|**5**|ERROR|2|-2|1|
|**6**|ERROR|3|-3|1|
|**10**|ERROR|5|-5|2|
|**-10**|ERROR|-5|5|-2|

Casos de prueba:

|Caso de Prueba|dividendo|divisor|Resultado esperado (Salida)|
|-|-|-|-|
|CP1|10|2|5|
|CP2|6|2|3|
|CP3|1|2|0|
|CP4|0|5|0|
|CP5|-10|2|-5|
|CP6|10|-2|-5|
|CP7|-10|-2|5|
|CP8|5|0|ERROR|
|CP9|0|0|ERROR|

Implementación en JUnit:

```java
@Test
void dividirPositivos() {
    assertAll("División de positivos",
            () -> assertEquals(5, Calculadora.dividir(10, 2)),
            () -> assertEquals(3, Calculadora.dividir(6, 2)),
            () -> assertEquals(0, Calculadora.dividir(1, 2)),
            () -> assertEquals(0, Calculadora.dividir(0, 5)),
            () -> assertEquals(1000, Calculadora.dividir(1000000, 1000)));
}

@Test
void dividirConNegativos() {
    assertAll("División con negativos",
            () -> assertEquals(-5, Calculadora.dividir(-10, 2)),
            () -> assertEquals(-5, Calculadora.dividir(10, -2)),
            () -> assertEquals(5, Calculadora.dividir(-10, -2)));
}

@Test
@DisplayName("Probar la división por cero")
void dividirPorZeroException() {
    var ex = assertThrows(OperacionNoValidaException.class, () -> Calculadora.dividir(10, 0),
            "La división por cero no está permitida");
    assertEquals(OperacionNoValidaException.MSG, ex.getMessage());
}
```

## Instrucciones

El alumno deberá hacer un fork de este proyecto, poner el repositorio como **privado**, agregar al profesor como colaborador (julparper) e implementar la solución solicitada (preguntas y código).

>Se deberá utilizar este fichero, y los artefactos de código del proyecto, para resolver el ejercicio.


**Si no se puede acceder al repositorio la evaluación del ejercicio será de 0. No se evaluarán entregas modificadas/entregadas fuera del plazo establecido en la tarea**