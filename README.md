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
