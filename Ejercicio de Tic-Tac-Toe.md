# Ejercicio de Tic-Tac-Toe (3 en linea)

## Estrategia de solución

Para la estrategia de solución se porpone lo siguiente:

Consiste en crear una amenaza doble en un espacio de 3 dimensiones, ya que resulta más sencillo crear amenazas así sin importar en que tire el jugador enemigo.

**Primer caso:** El primer tiro lo da el programa.
1. Lo primero es tomar una esquina, cualquiera en el espacio de 3x3x3 de las capa superior o inferior.
2. Se analiza el tiro del enemigo y se propone un tiro en la esquina vecina, donde si es posible, nos ayude a bloquear alguna jugada del enemigo o lo obliguemos bloquear la linea de 3.
3. El siguiente tiro se analiza y se pone en una esquina que una los dos tiros anteriores en diagonal, vertical u horizontal, donde no se encuentre ninguna ficha enemiga por lo menos en 2 caminos, ya sea en linea u horizontal, con el proposito de crear una doble amenaza.
4. Por ultimo, el enemigo solo podrá bloquear una y el siguiente tiro será en la amenaza que quede disponible.

**Segundo caso:** El primer tiro lo da el enemigo (usuario).
1. Buscamos ganar un centro en cualquier capa, preferentemente el centro de todo.
2. Analizamos los tiros del enemigo y tratamos de bloquear las lineas que vaya a completar.
3. Si se da la oportunidad buscaremos crear una v con el centro que ganamos, tratando de generar la amenaza doble.
4. Si no se puede generar la v se jugará a tratar de empatar.


## Medida de Rendimiento

La medida de rendimiento se puede basar en la cantidad de partidas ganadas en comparación con las partidas perdidas o empatadas.

- **Victoria**: +1 punto
- **Empate**: 0 puntos
- **Derrota**: -1 punto

## Secuencia de Percepción

1. **Primera percepción (Cuando la IA hace el primer movimiento):**
   - Observa el tablero vacío y decide qué esquina de la capa superior o inferior tomará como su primer movimiento.

2. **Segunda percepción (Después del primer movimiento del enemigo):**
   - Analiza el movimiento del enemigo y propone un movimiento en una esquina vecina para bloquear las jugadas del enemigo o crear una amenaza propia.
   
3. **Tercera percepción (Después del segundo movimiento del enemigo):**
   - Evalúa el segundo movimiento del enemigo y coloca su ficha en una esquina que conecta las dos jugadas anteriores en diagonal, vertical u horizontal, buscando crear una doble amenaza.
   
4. **Cuarta percepción (Después del tercer movimiento del enemigo):**
   - El enemigo bloquea una de las amenazas, y la IA coloca su ficha en la amenaza que queda disponible.

5. **Primera percepción (Cuando el enemigo hace el primer movimiento):**
   - Observa el movimiento del enemigo y busca ganar el centro en cualquier capa.
   
6. **Segunda percepción (Después del segundo movimiento del enemigo):**
   - Analiza el segundo movimiento del enemigo y bloquea las líneas que pueda completar.

7. **Tercera percepción (Después del tercer movimiento del enemigo):**
   - Si es posible, busca crear una forma de "V" con el centro ganado para generar una amenaza doble.
   
8. **Cuarta percepción (Después del cuarto movimiento del enemigo):**
   - Si no se pudo crear una "V" y la partida no está decidida, la IA juega para empatar.
