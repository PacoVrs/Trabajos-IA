# Introducción a la Inteligencia Artificial - Práctica 6: El proceso de razonamiento según la lógica

## Contenido

* [Planteamiento matemático del problema de Josephus](#actividad-1-planteamiento-matemático-del-problema-de-josephus)
* [Programación de la solución](#actividad-2-programación-de-la-solución)

## Actividad 1: Planteamiento matemático del problema de Josephus

### El circulo de la muerte de Josephus

El problema plantea que hay un circulo de n personas, donde cada persona deberá matar a la que tiene a su lado, en sentido horario. Supongamos que el circulo tiene 41 personas, como originalmente se describe el problema. En este caso comienza la persona número 1, por lo cual esta eliminará a la 2, después la 3 a la 4, la 5 a la 6 y así sucesivamente, hasta que quede una sola persona. El objetivo es encontrar una manera consistente de saber quien será la ultima persona.

### Solución al problema

Para comenzar el analisis de este problema se decidió resolver el problema para los primeros 20 casos, es decir para desde 1 hasta 20 personas, lo que nos da como resultado la siguiente tabla:

|Personas en el circulo|1 |2 |3 |4 |5 |6 |7 |8 |9 |10 |11 |12 |13 |14 |15 |16 |17 |18 |19 |20 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Persona sobreviviente|1 |1 |3 |1 |3 |5 |7 |1 |3 |5 |7 |9 |11 |13 |15 |1	|3	|5 |7 |9 |

En base a estos resultados podemos concluir que para cualquier cantidad de personas que sea igual a una potencia de 2 (*2^n*), la persona que sobreviva será la que comience en el circulo. Esto se debe a que en cada ronda, se dividiran a la mitad, lo que dejará una cantidad par de personas, y esto se repetirá siempre.

Para continuar con los demás casos, los representaremos como *2^n + x*, esto debido en que en algún momento el circulo se volverá una potencia de 2, y x representará la cantidad de turnos que deben de pasar para que esto suceda.

Para explicar esto más a detalle se pondrá el ejemplo con un circulo de 6 personas, en nuestra representación matemática quedaría como *n = 2* y *x = 2*, etonces esto quiere decir que el numero que le toque tirar en el tercer turno, será el que va a sobrevivir, se supondrá que iniciará el 1, el cual elimina al 2, en ese momento se convierte en un circulo de 5, ahora el siguiente turno corresponde al 3, quien elimina al 4, justo en ese momento la cantidad de personas en el circulo corresponde a un número que es potencia de 2, el siguiente en tirar sería el 5, por lo que según los datos que se representaron en la tabla, es el que quedara vivo al final.

Ahora, si resolvemos el valor de nuestra expresión con los valores que definimos antes, quedaría como *(2^2) + 2*, esto nos da como resultado el numero de personas iniciales.

Tomando la expresión *2^n + x*, y basandonos en los valores de la tabla, la expresión *2x + 1* nos da los resultados del numero que corresponde a la persona que sobrevive, esto se puede comprobar con todos los resultados generados en la tabla.

Así, se puede definir la persona que sobrevivirá al final.

## Actividad 2: Programación de la solución

El código primeramente deberá determinar el número al cual deberá elevar la potencia, para eso tenemos el siguiente método, el cual recibirá el numero de personas que hay en el circulo, y comenzará con la potencia 0, ya que el número mínimo de personas a sobrevivir es 1, y todo número elevado a la potencia 0 es 1, a partir de ahí, entraremos en un ciclo, que incrementará la potencia siempre y cuando el resultado de esa potencia sea menor al número de personas en el círculo.

Una vez determinada la potencia, se calcula el valor faltante para llegar a la cantidad de personas, para esto se saca el valor total de la potencia, y ese valor se le resta a el total de personas.

El último paso consiste en aplicar la formula *2x + 1*, que sería el valor faltante para completar el total de personas, multiplicado por 2, más 1.

A continuación se deja el código que representa la lógica anterior.

```python
# Metodo para determinar el valor n, x y el sobreviviente en "personas = 2^n + x" y "sobreviviente = 2x + 1"
def potencia(num):
    n = 0
    while 2 ** (n + 1) <= num:
        n += 1

    potenciad2 = 2 ** n
    x = num - potenciad2
    sobreviviente = 2*x +1

    return sobreviviente

# Ejemplo con el número 41
numero = 10
sobreviviente = potencia(numero)

print(f"La última persona sobreviviente en un círculo de {numero} personas es la numero {sobreviviente}")
```