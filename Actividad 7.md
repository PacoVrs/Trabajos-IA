# Introducción a la Inteligencia Artificial - Práctica 7: El papel de la heurística

## Contenido
* [Definicion de la herística y su papel en la resolución de problemas](#actividad-1-definir-qué-es-la-heurística-y-cual-es-su-papel-en-la-resolucón-de-probelmas)
* [Desarrollo de algoritmo de solución](#actividad-2-desarrollo-de-algoritmo-de-solución-usando-recursividad)
* [Programación de la solución](#actividad-3-programación-y-explicación-del-algoritmo-de-solución-mediante-recursividad)

## Actividad 1: Definir qué es la Heurística y cual es su papel en la resolucón de probelmas

La heurística es una técnica o estrategia para resolver problemas, tomar decisiones o descubrir soluciones, especialmente en situaciones complejas o donde la información es limitada. Se basa en reglas prácticas o métodos empíricos que, aunque no garantizan una solución óptima, tienden a ser efectivos y a producir resultados satisfactorios en un tiempo razonable.

En la resolución de problemas, la heurística desempeña un papel fundamental al permitir el desarrollo de métodos aproximados, prácticos y eficientes para encontrar soluciones cuando los enfoques exactos pueden ser computacionalmente costosos o incluso imposibles de aplicar. Estas estrategias se centran en simplificar la búsqueda de soluciones a través de la reducción del espacio de búsqueda, la identificación de patrones o la aplicación de reglas generales.

La heurística permite:

* **Reducir la complejidad:** Al emplear atajos o reglas simplificadas, limita la cantidad de opciones a considerar, haciendo más manejable la búsqueda de soluciones.

* **Encontrar soluciones aceptables:** Aunque no asegura la mejor solución, proporciona resultados satisfactorios o cercanos a la solución óptima en un tiempo razonable.

* **Tomar decisiones en situaciones inciertas:** En contextos donde la información es incompleta o costosa de obtener, la heurística ofrece un marco para tomar decisiones basadas en la experiencia o reglas empíricas.

* **Agilizar la resolución de problemas complejos:** En problemas computacionalmente costosos, la heurística puede acelerar el proceso de búsqueda de soluciones razonables, evitando un agotamiento de recursos.

Es importante tener en cuenta que si bien la heurística es valiosa para encontrar soluciones rápidas, no garantiza la optimización ni siempre conduce a la mejor respuesta posible. En ocasiones, puede llevar a soluciones subóptimas debido a las simplificaciones que emplea. Sin embargo, su capacidad para ofrecer soluciones aceptables en tiempo razonable la hace crucial en muchos contextos de resolución de problemas.

## Actividad 2: Desarrollo de algoritmo de solución usando recursividad

Para este problema se busca encontrar la ruta más corta desde un nodo inicial hata un nodo objetivo dentro de una matriz, en donde se tendrá en cuenta el costo acumulado además de una estmación heurística del costo restante.

### Algoritmo

En esta sección se detalla el algoritmo que se utilizará para resolver este problema.

*Notas:*
* *Se utilizarán 2 listas, cerrada y abierta. En la lista abierta están todos los nodos que se han explorado, incluyendo los que no se han visitado, mientras que en la lista cerrada están los nodos por los que ya se ha pasado.*
* *Cada uno de los nodos deberá hacer referencia hacia su nodo padre, el cual corresponde al nodo por el cual se llegó al nodo actual. Esta referencia solo cambiará cuando hay una actualización de valores y nos da una estimación total menor que el padre actual.*
* *No se puede visitar un nodo que ya esté en la lista cerrada.*
* *Para conocer el camino final, se deberá seguir el camino de los nodos padre iniciando en el nodo objetivo.*

Aquí comienza la descripción general del algoritmo que se utilizará.

1. **Comienzo del algoritmo.**
   * Se comienza en el nodo inicial con un valor de costo inicial de 0.
   * Se calcula la heurística desde el nodo actual hasta el nodo objetivo.

2. **Exploración de vecinos.**
    * Se analizan los vecinos del nodo actual.
    * Se calcula el costo acumulado desde el nodo inicial hasta cada vecino.
    * Se calcula la heurística desde cada nodo vecino hasta el nodo objetivo.
  
3. **Actualizar datos.**
    * Se actualiza el costo acumulado y la heurística para cada vecino.
    * Se ordena la lista abierta de nodos en base al costo acumulado y la heurística.

4. **Se selecciona el nodo con menor valor en el costo acumulado.**

5. **Repetir desde el paso 2 hasta que se llegue al nodo objetivo.**

## Actividad 3: Programación y explicación del algoritmo de solución mediante recursividad.

Como primer paso definiremos los laberintos, a continuación se muestran los laberintos que se utilizaron.

```python
laberinto = [
    [1,1,1,1,1,1,1,0,1],
    [0,0,0,0,0,0,1,0,1],
    [1,1,1,0,1,1,1,0,1],
    [1,0,0,0,1,0,1,0,1],
    [1,0,1,1,1,0,1,0,1],
    [1,0,0,0,0,0,0,0,1],
    [1,0,1,1,1,0,1,0,1],
    [1,0,1,0,0,0,1,0,1],
    [1,1,1,1,1,1,1,1,1]
]

laberinto2 = [
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
    [0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,1,0,1],
    [1,1,1,0,1,1,1,0,1,1,1,1,0,1,1,1,0,1],
    [1,0,0,0,1,0,1,0,1,0,0,0,0,1,0,1,0,1],
    [1,0,1,1,1,0,1,0,0,0,0,1,1,1,0,1,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,1],
    [1,0,1,1,1,0,1,0,1,1,0,1,1,1,0,1,0,1],
    [1,0,1,0,0,0,1,0,1,0,0,1,1,1,0,1,0,1],
    [1,0,0,0,0,0,1,0,0,0,0,0,0,0,0,1,0,1],
    [1,1,1,0,1,1,1,0,1,1,1,1,0,1,1,1,0,1],
    [1,0,0,0,1,0,1,0,1,1,0,0,0,1,0,1,0,1],
    [1,0,1,1,1,0,1,0,0,1,0,1,1,1,0,1,0,1],
    [1,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,1],
    [1,0,1,1,1,0,1,0,1,1,0,1,1,1,0,1,0,1],
    [1,0,1,0,0,0,1,0,1,0,0,1,1,1,0,1,0,1],
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1]
]
```

Ahora declararemos las listas que se utilizaran

* **Lista abierta:** Vecinos explorados.
* **Lista cerrada:** Nodos visitados.
* **Lista meta:** Contiene los metadatos de las casillas, tales como el id, las coordenadas del padre y los valores G, H y F.
* **Lista aux:** Lista auxiliar.
* **Camino:** Camino mas corto encontrado.

```python
lista_abierta = []
lista_cerrada = []
lista_meta=[]
lista_aux = []
camino = []
n=0

coordenada_inicio = [1,0]
coordenada_final = [0,7]
```

Ahora iniciaremos un ciclo que llenará la lista de metadatos con valores iniciales.

```python
filas = len(laberinto2)
columnas = len(laberinto2[0])

for row in laberinto:
    for column in row:
        # metadata = [id, padrex, padrey, G, H, F]
        metadata = [n, None, None, 0, 0, 0]
        lista_aux.append(metadata)
        n = n + 1
    lista_meta.append(lista_aux)
    lista_aux = []
```

Se tiene también la siguiente función, que nos ayuda a determinar si un vecino es válido para realizar una exploración o no.

```python
def isValid(coord):
    return 0 <= coord[0] < len(laberinto) and 0 <= coord[1] < len(laberinto[coord[0]]) and laberinto[coord[0]][coord[1]] == 0 and (coord[0] != coordenada_inicio[0] or coord[1] != coordenada_inicio[1])
```

La siguiente función nos permite identificar si dos coordenadas con vecinos en diagonal o no.

```python
def isdiagonal(coord, dad):
    for x,y in [(1,1), (-1,1), (-1,-1), (1,-1)]:
        if dad[0] == (coord[0]+x) and dad[1] == (coord[1]+y):
            return True
    return False
```

La siguiente función nos regresa el valor de la heurística (valor de la variable H) desde una coordenada dada.

```python
def getH(coord):
    xux = coord[0]
    yux = coord[1]
    cont = 0
    while xux != coordenada_final[0]:
        if xux > coordenada_final[0]:
            xux = xux - 1
            cont = cont + 1
        else:
            xux = xux + 1
            cont = cont + 1

    while yux != coordenada_final[1]:
        if yux > coordenada_final[1]:
            yux = yux - 1
            cont = cont + 1
        else:
            yux = yux + 1
            cont = cont + 1
    
    return cont * 10
```

La siguiente función nos permite obtener los vecinos de una coordenada dada.

```python
def getneigh(coord):
    lista = [(0,1), (0,-1), (1,0), (-1,0), (1,1), (-1,1), (-1,-1), (1,-1)]
    neigh = []
    for x,y in lista:
        neighcoord = [(coord[0] + x), (coord[1] + y)]
        if isValid(neighcoord):
            neigh.append((neighcoord[0], neighcoord[1]))
            lista_abierta.append(neighcoord)
    return neigh
```

La siguiente función es la función principal de la búsqueda, se encarga de ejecutar el algoritmo que creamos.

```python
def findtheway(coord):
    if coord[0] != coordenada_final[0] or coord[1] != coordenada_final[1]:
        lista_cerrada.append(coord)
    
        # Se obtiene la lista de vecinos
        neighlist = getneigh(coord)
        
        for x,y in neighlist:
            # Obtener el nuevo calculo de G
            tempG = lista_meta[coord[0]][coord[1]][3]
            
            if isdiagonal([x,y], coord):
                tempG = tempG + 14
            else:
                tempG = tempG + 10
    
            # Obtener el nuevo valor de H
            tempH = getH([x,y])
        
            # Calculamos la nueva F
            tempF = tempG + tempH
            
            # Comprobamos si el vecino ya tenia padre
            if lista_meta[x][y][1] is None:
                lista_meta[x][y][1] = coord[0]
                lista_meta[x][y][2] = coord[1]
                lista_meta[x][y][3] = tempG
                lista_meta[x][y][4] = tempH
                lista_meta[x][y][5] = tempF
            elif lista_meta[x][y][5] > tempF:
                lista_meta[x][y][1] = coord[0]
                lista_meta[x][y][2] = coord[1]
                lista_meta[x][y][3] = tempG
                lista_meta[x][y][4] = tempH
                lista_meta[x][y][5] = tempF
    
        # Nodos a los que nos podemos mover
        aviablenodos = [elemento for elemento in lista_abierta if elemento not in lista_cerrada]
    
        # Obtendremos los valores de F de los nodos disponibles
        fvalues = []
        for nodo in aviablenodos:
            fvalues.append(lista_meta[nodo[0]][nodo[1]][5])
    
        fminvalue = min(fvalues)
    
        aux = 0
        while fvalues[aux] != fminvalue:
            aux = aux + 1
        # Esta variable almacenara las coordenadas del nodo al que nos moveremos
        nextnodo = aviablenodos[aux]
        findtheway(nextnodo)
```

La última función nos permite enlistar el camino más corto gracias a los metadatos que se generaron en la función anterior, para iniciar la extracción del camino deberemos mandarlo llamar con las coordenadas del nodo objetivo.

```python
def getbestpath(coord):
    camino.insert(0, lista_meta[coord[0]][coord[1]][0])
    dad = [lista_meta[coord[0]][coord[1]][1], lista_meta[coord[0]][coord[1]][2]]
    if dad[0] is not None:
        getbestpath(dad)
    else:
        return

```

Una vez ya definidos todos las funciones que se utilizarán, se agrega a la lista abierta el nodo inicial y comenzamos la ejecución del algoritmo principal, y cuando termine, extraemos el camino más corto y lo imprimimos.

```python
lista_abierta.append(coordenada_inicio)
findtheway(coordenada_inicio)
getbestpath(coordenada_final)

print(f'La ruta mas corta fue {camino}')
```