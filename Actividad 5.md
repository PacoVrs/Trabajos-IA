# Introducción a la Inteligencia Artificial - Práctica 5: Identificación de colores

## Contenido
* [Ensayo sobre el proceso de solución del problema](#actividad-1-ensayo-sobre-el-proceso-de-solución-del-problema)
* [Programación del problema](#actividad-2-progamación-del-problema)

## Actividad 1: Ensayo sobre el proceso de solución del problema

### "El proceso de reflexión previo a la resolución de problemas algorítmicos"
#### Presentado por Francisco Javier Villegas Reyes

El diseño y desarrollo de algoritmos son elementos cruciales en la informática y la resolución de problemas computacionales. Sin embargo, en la prisa por encontrar respuestas rápidas, es común pasar por alto la importancia de detenerse y reflexionar sobre el problema antes de buscar una solución.

Esta reflexión inicial es fundamental, ya que sienta las bases para un diseño más eficiente. Al enfrentarnos a un problema algorítmico, comprender su naturaleza, identificar sus características y limitaciones, así como considerar diferentes enfoques de solución, resulta esencial.

Esta pausa reflexiva permite anticipar desafíos, evaluar la complejidad del problema y considerar estrategias diversas antes de decidir una solución específica. Un análisis riguroso en esta etapa inicial ahorra tiempo y previene errores, mejorando la eficiencia y escalabilidad del algoritmo final.

Esta reflexión profunda fomenta la innovación al explorar enfoques creativos y soluciones novedosas. Considerar distintas perspectivas y abordajes puede conducir a alternativas más elegantes, eficientes e incluso revolucionarias, impulsando el avance en la ciencia de la computación.

Por tanto, reflexionar y analizar un problema antes de abordar su solución es esencial en el desarrollo de algoritmos. Esta práctica no solo mejora la eficiencia en la resolución de problemas, sino que también estimula la innovación y el descubrimiento de soluciones más avanzadas y creativas. Definir el problema de manera clara y precisa es el primer paso para iniciar este proceso de resolución.

Para esta práctica, se pidió un programa capaz de contar el número de elementos del mismo color, para lograr esto necesitamos profundizar más en en el contexto del problema.

El problema se basa en la busqueda dentro de imagenes, interpretadas en forma de matriz, en donde utilizamos el término isla para definir un conjunto de pixeles, en este caso también nombrados como coordenadas. Para la búsqueda se tendrá que ir recorriendo cada punto de la matriz, y cuando se detecte el color que se está buscando iniciará un algoritmo que será capaz de recorrer la isla y contar cuantos elementos existen de ese color.

La complejidad de este problema viene en la interpretación de los colores, ya que no tendrá unicamente 1 canal para el color, sino que ahora tendremos 3 canales, eso si se está trabajando con el formato RGB. Si quisieramos hacer el código para manejarlo así la cantidad de comparaciones resultaría excesiva, por lo que se propone el uso de el formato HSV, que aunque también maneja 3 canales, se maneja diferente la clasificación del color, dejando como resultado que es más sencilla su forma de clasificar los colores, y nos permitirá hacer más con menos código.

El color rojo en este formato de color se encuentra en ambos extremos de los valores, por lo que para poder aplicar filtros debemos de utilizar dos umbrales, lo que nos permitirá ubicar todos los pixeles que se encuentren en ese rango de colores, y después podremos aplicar un filtro de blanco y negro y buscar la cantidad de islas.

**Algoritmo de resolución del problema**

A continuación se muestra el algoritmo que se seguirá para resolver el problema:

* Se recorrera la matriz de izquierda a derecha y de arriba a abajo.
* Cuando se encuentre un elemento de un color especifico o diferente al del fondo, se compara con una lista que almacena las coordenadas que ya han sido registradas para una isla.
  * Si no ha sido registrada, se almacena las coordenadas iniciales en una variable que llamaremos coordenadas limites y se entrara en el método de registro de islas.
  * Si ya fue registrada, ignorará ese pixel y continuará con el recorrido.
* Las coordenadas que entran en el método de registro de islas entrara en una pila.
* Se iniciará un ciclo que durará mientras la pila siga teniendo datos.
* Se obtendrán los datos que se encuentren en la parte superior de la pila.
* Se agregan las coordenadas a la lista.
* Se comparan las coordenadas de la variable coordenadas limite, y si es mayor o menor ya sea en 'x' o 'y' superior o inferior se actualizarán los limites.
* Se verifica que su vecino de la derecha sea de un color diferente al del fondo, ademas que se encuentre dentro de los rangos de la matriz, y que las nuevas coordenadas no estén ya en la lista, si se cumple con las condiciones se agrega a la pila.
* Se verifica que su vecino de la izquierda sea de un color diferente al del fondo, ademas que se encuentre dentro de los rangos de la matriz, y que las nuevas coordenadas no estén ya en la lista, si se cumple con las condiciones se agrega a la pila.
* Se verifica que su vecino de arriba sea de un color diferente al del fondo, ademas que se encuentre dentro de los rangos de la matriz, y que las nuevas coordenadas no estén ya en la lista, si se cumple con las condiciones se agrega a la pila.
* Se verifica que su vecino de abajo sea de un color diferente al del fondo, ademas que se encuentre dentro de los rangos de la matriz, y que las nuevas coordenadas no estén ya en la lista, si se cumple con las condiciones se agrega a la pila.
* Se verifica si la pila sigue teniendo elementos, si contienen más elementos, se repite el ciclo, en caso contrario termina el ciclo.
* Se aumenta el contador de islas encontradas.
* Se continua con el recorrido de la matriz.
* Una vez termina el recorrido de la matriz se les coloca un recuadro a cada isla detectada, y se muestran la cantidad de islas encontradas así como la imagen con los recuadros de donde se ubicaron las islas.

## Actividad 2: Progamación del problema

Se importan las librerias a utilizar.
```python
import cv2 as cv
```

Se definen los métodos que se utilizaran en el programa.

```python
# Método de busqueda de islas
def startSearch(mascara):
    
    def regIsland(i, j):
        stack = [(i, j)]
        while stack:
            x, y = stack.pop()
            lista.add((x, y))
            if (x > coord[2]):
                coord[2] = x
            elif (x < coord[0]):
                coord[0] = x
            elif (y > coord[3]):
                coord[3] = y
            elif (y < coord[1]):
                coord[1] = y
            for dx, dy in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
                nx, ny = x + dx, y + dy
                if 0 <= nx < w and 0 <= ny < h and mascara[nx, ny] != 0 and (nx, ny) not in lista:
                    stack.append((nx, ny))
                        
    w, h = mascara.shape
    lista = set()
    listacoord = []
    for i in range(w):
        for j in range(h):
            if (mascara[i,j] != 0) and (i, j) not in lista:
                    coord = [i, j, i, j]
                    regIsland(i, j)
                    listacoord.append(coord)
                
    return listacoord

# Método para colocar rectángulos a las islas encontradas
def setRect(aux, coords):
    for coord in coords:
        cv.rectangle(aux, (coord[1]-1, coord[0]-1), (coord[3]+1, coord[2]+1), (255, 0, 0), 1)
```

Se carga la imagen que se utilizará en este análisis y se le colocan los filtros para utilizarla con el formato HSV.

```python
img = cv.imread('D:/Imagenes/objetos.png', 1)
img2 = cv.cvtColor(img, cv.COLOR_BGR2RGB)
img3 = cv.cvtColor(img2, cv.COLOR_RGB2HSV)
```

Para este ejercicio se definirá un umbral de color para detectar el color rojo de la siguiente imagen.

![Imagen de objetos](images/objetos.png)

*Nota: Como el umbral del color rojo abarca los extremos se utilizarán dos umbrales que se unirán en uno solo.*

Se definen los umbrales y se unen para formar uno solo.

```python
# Definición de umbrales
umbralbajo = (0, 80, 80)
umbralalto = (10, 255, 255)
umbralbajob = (175, 80, 80)
umbralaltob = (180, 255, 255)

# Se aplican las mascaras
mascara1 = cv.inRange(img3, umbralbajo, umbralalto)
mascara2 = cv.inRange(img3, umbralbajob, umbralaltob)

# Se unen las mascaras par cubrir todos los rojos
mascararoja = mascara1 + mascara2
```

Ejecutamos la búsqueda de islas para esa mascara, le aplicamos el filtro a la imagen y le colocamos los rectangulos a las islas encontradas.

```python
# Incia busqueda de islas
coordrojas = startSearch(mascararoja)

# Aplicar filtro a la imagen para color rojo
resultadorojo = cv.bitwise_and(img, img, mask=mascararoja)

# Se colocan los rectangulos a las islas
setRect(filtrado, coordrojas)
```

Por último se muestra el conteo de islas y se muestra la imagen con las islas.

```python
# Se cuentan y muestran la cantidad de islas
cantidadislas = len(coordrojas)
print(f'Se encontraron {cantidadislas} islas.')

# Se muestra la imagen con filtro
cv.imshow('resultado rojo', resultadorojo)
```