Juan Eduardo Rosas Cerón - A01710168

## Proyecto

Mi proyecto consta de un predictor del mejor movimiento de ajedrez dada una posición de mate en uno en formato FEN.
El modelo recibe una posición del tablero y predice los mejores tres movimientos, uno que resulta en jaque mate y otros dos.

## Dataset

El dataset contiene posiciones de ajedrez en formato FEN junto con el movimiento que resulta en jaque mate.
Las posiciones fueron generadas a partir de partidas entre monos (agentes aleatorios),
garantizando que cada tablero tenga solo una solución válida.
Hay 5,003 registros con dos columnas: la posición en FEN y el mejor movimiento en notación algebraica.

## Proceso

### Preprocesamiento

Las posiciones fueron transformadas en representaciones numéricas aptas parael modelo.
Cada cadena fue decodificada pieza por pieza, mapeando cada tipo de pieza a un valor entero
(peón blanco = 1, caballo negro = -3, etc.) y construyendo una matriz de 8×8 que representa el tablero.
El formato FEN agrega también seis campos de metadata útil como: en passant y enrroques.

Para el escalamiento, los valores de la matriz fueron normalizados al rango [-1, 1] dividiendo entre el valor máximo absoluto asignado al rey,
de modo que todas las entradas del modelo se encuentran dentro de un rango uniforme.

El preprocesamiento del conjunto de datos es importante para que el modelo pueda trabajar adecuadamente para realizar la predicción del mejor movimiento de ajedrez.

El conjunto de datos cuanta con: el estado de la partida en nombreglatura FEN y el mejor movimiento posible en notación algebraica

**Nombreglatura FEN:**

> EJEMPLO:
>
> rnbqkbnr/ppppp2p/8/5pp1/4P3/8/PPPP1PPP/RNBQKBNR w KQkq - 0 3

Esta conformada por seis partes separadas por un espacio:
1. Posición del tablero separado por '/'
    - Mayusculas para blancas, minusculas para negras
    - K/k para el rey
    - Q/q para la reina
    - R/r para la torre
    - N/n para el caballo
    - P/p para el peón
    - B/b para el alfil
2. De quien es el turno
    - 'w' blancas
    - 'b' negras
3. Si hay enroque
    - K enroque blanco corto
    - k enroque negro corto
    - Q enroque blanco largo
    - q enroque negro largo
    - '-' ninguno disponible
4. Captura el paso con la casilla objetiva del peón que avanzó previamente en notación algebraica
    - Por ejemplo: e6
5. Semimovimientos desde el ultimo avance de peón o captura, se usa para la regla de 50 movimientos
6. Número de la jugada

##

**CNN - Convolutional Neural Network:**


CNN necesita de tensores para funcionar, estos los modelamos por medio de la nombreglatura FEN. Esto nos da como resultado un tensor de 8x8x13, doce por las piezas de ajedrez (6 negras y 6 blancas) más uno del turno y 8x8 por las casillas del tablero de ajedrez.

AlphaZero utiliza CNN con LSTM creando un modelo a la par de los mejores jugadores de ajedrez del mundo, por lo que sé que mi decisión funciona. No use también LSTM ya que solo me interesa analizar una posición de ajedrez sin importar el historial de movimientos.


## Referencias

[1] K. Samara, A. Antreassian, M. Klug y M. S. Hasan, "Enfoques de aprendizaje automático para clasificar resultados de partidas de ajedrez: un análisis comparativo de calificaciones de jugadores y dinámicas de juego," Electronics, vol. 15, núm. 1, p. 1, 2026, doi: 10.3390/electronics15010001.

[2] M. Omori y P. Tadepalli, "Estimación de calificación de ajedrez a partir de movimientos y tiempos de reloj usando una CNN-LSTM," en Computers and Games, M. Hartisch, C.-H. Hsueh y J. Schaeffer, Eds., Lecture Notes in Computer Science, vol. 15550. Cham, Suiza: Springer, 2025, doi: 10.1007/978-3-031-86585-5_1.

[3] Anthropic, Claude, asistencia mediante IA para desarrollo de interfaz gráfica de ajedrez en Google Colab, consulta del autor, 28 de abril de 2026. [En línea]. Disponible: https://claude.ai

[4] Lichess, "Base de datos abierta de Lichess — Puzzles," database.lichess.org. [En línea]. Disponible: https://database.lichess.org/#puzzles. [Consultado: 28 de abril de 2026].

[5] Bhupen, "Mate in One (Chess)," Kaggle, 2019. [En línea]. Disponible: https://www.kaggle.com/datasets/ancientaxe/mate-in-one-chess. [Consultado: 28 de abril de 2026].
