# Proyecto 3 -Phaser 3 proyectiles

## Objetivo:

Editar el Juego Phaser para que esquive proyectiles 

- Horizontal 
- Vertical 
- Diagonal 

Diseña una red neuronal para que el juego sea capaz de aprender patrones de movimeinto y pueda jugarse de forma automatica.

## Descripción de Funciones

- **Variables Globales**
  - `w` y `h`: Ancho y alto del fondo del juego.
  - `jugador`: Variable que representa al jugador.
  - `fondo`: Variable que representa el fondo del juego.
  - `bala`, `disp`, `nave`: Variables para la nave y su bala en movimiento horizontal.
  - `bala2`, `disp2`, `nave2`: Variables para la nave y su bala en movimiento vertical.
  - `bala3`, `disp3`, `nave3`: Variables para la nave y su bala en movimiento diagonal.
  - `velocidadBala`, `despBala`, `velocidadBala2`, `despBala2`, `velocidadBala3`, `despBalaHorizontal3`, `despBalaVertical3`, `despBala3`: Variables relacionadas con la velocidad y desplazamiento de las balas.
  - `salto`, `avanzar`, `menu`: Acciones del juego.
  - `arriba`, `abajo`, `derecha`, `izquierda`: Estados del jugador.
  - `nnNetwork`, `nnEntrenamiento`, `nnSalida`, `datosEntrenamiento`: Variables relacionadas con la red neuronal.
  - `modoAuto`, `eCompleto`: Modos de juego y estado del entrenamiento.

- **Funciones Principales**

  ### `preload()`
  Carga los recursos del juego.
  - `fondo`: Carga la imagen de fondo.
  - `mono`: Carga el sprite del jugador.
  - `nave`: Carga la imagen de la nave.
  - `bala`: Carga la imagen de la bala.
  - `menu`: Carga la imagen del menú.

  ### `create()`
  Inicializa los elementos del juego.
  - Inicia el sistema de física y establece la gravedad.
  - Crea y posiciona los sprites del fondo, las naves, las balas y el jugador.
  - Habilita la física para los elementos.
  - Configura la animación del jugador.
  - Configura el texto y eventos de pausa.
  - Configura las teclas de entrada (`SPACEBAR` y `RIGHT`).
  - Inicializa la red neuronal (`nnNetwork`) y el entrenador (`nnEntrenamiento`).

  ### `enRedNeural()`
  Entrena la red neuronal con los datos de entrenamiento.
  - Parámetros: Tasa de aprendizaje (`rate`), número de iteraciones (`iterations`) y si se deben mezclar los datos (`shuffle`).

  ### `datosDeEntrenamiento(param_entrada)`
  Procesa los datos de entrada y activa la red neuronal.
  - `param_entrada`: Array con los datos de entrada (desplazamiento y velocidad de las balas).
  - Activa la red neuronal con los datos de entrada y obtiene las salidas.
  - Calcula y muestra los porcentajes de movimiento hacia arriba, abajo, derecha e izquierda.
  - Retorna `true` si el valor de la salida para la derecha es mayor o igual al de la izquierda.

  ## Descripción de Funciones Adicionales

### `EntrenamientoSalto(param_entrada)`
Procesa los datos de entrada para determinar si el jugador debe saltar.
- **Parámetros**:
  - `param_entrada`: Array con los datos de entrada (desplazamiento y velocidad de las balas).
- **Función**:
  - Activa la red neuronal con los datos de entrada y obtiene las salidas.
  - Calcula y muestra los porcentajes de movimiento hacia arriba (`aire`) y hacia abajo (`piso`).
  - Retorna `true` si el valor de la salida para arriba es mayor o igual al de abajo.

### `pausa()`
Pausa el juego y muestra el menú de pausa.
- **Función**:
  - Pausa el juego.
  - Añade un sprite de menú en el centro de la pantalla.
  - Establece el anclaje del menú al centro.

### `mPausa(event)`
Maneja los eventos de pausa y reanuda el juego basándose en las interacciones del usuario con el menú de pausa.
- **Parámetros**:
  - `event`: El evento del ratón que contiene las coordenadas del clic.
- **Función**:
  - Comprueba si el juego está pausado.
  - Determina si el clic del ratón está dentro de los límites del menú.
  - Si el clic está en la parte superior del menú, reinicia el entrenamiento y desactiva el modo automático.
  - Si el clic está en la parte inferior del menú, inicia el entrenamiento si no se ha completado y activa el modo automático.
  - Restablece las variables y el estado del jugador.
  - Reanuda el juego y destruye el menú.

## Descripción de la Función `update()`

### `update()`
Esta función se ejecuta continuamente durante el juego y maneja la lógica principal de actualización del estado del juego.

- **Actualización del Fondo**:
  - Desplaza el fondo del juego para crear un efecto de movimiento continuo.

- **Colisiones**:
  - Detecta colisiones entre el jugador y las naves o balas.

- **Estatus Iniciales**:
  - Inicializa los estados de las variables `arriba`, `abajo`, `derecha` e `izquierda`.

- **Detección de Movimiento del Jugador**:
  - Si el jugador está en el aire o moviéndose verticalmente, se actualizan los estados `arriba` y `abajo`.
  - Si el jugador se está moviendo horizontalmente a cierta velocidad, se actualizan los estados `derecha` e `izquierda`.

- **Cálculo de Desplazamientos**:
  - Calcula la diferencia horizontal y vertical entre la posición del jugador y las posiciones de las balas.

- **Restricción de Movimiento del Jugador**:
  - Evita que el jugador avance más allá de 200px.

- **Control Manual del Jugador**:
  - Permite que el jugador salte y se mueva hacia la derecha o izquierda si se presionan las teclas correspondientes y se cumplen ciertas condiciones.

- **Control Automático del Jugador**:
  - Si el modo automático está activado, utiliza la red neuronal para determinar si el jugador debe saltar o correr basándose en las posiciones y velocidades de las balas.

- **Disparo de Balas**:
  - Controla el disparo y reseteo de las balas.

- **Entrenamiento de la Red Neuronal**:
  - Si el modo automático está desactivado y hay balas en el juego, se recopilan datos de entrenamiento incluyendo las entradas (desplazamientos y velocidades de las balas) y las salidas (estados `arriba`, `abajo`, `derecha`, `izquierda`).

## Descripción de Funciones

### `disparo()`
Inicializa la velocidad y dirección de la primera bala.
- **Función**:
  - Genera una velocidad aleatoria para la bala dentro del rango de 300 a 700.
  - Establece la velocidad de la bala en el eje `x`.
  - Marca la bala como disparada (`disp=true`).

### `disparo2()`
Inicializa la velocidad y dirección de la segunda bala.
- **Función**:
  - Genera una velocidad aleatoria para la bala dentro del rango de 300 a 800.
  - Establece la velocidad de la bala en el eje `y`.
  - Marca la bala como disparada (`disp2=true`).

### `disparo3()`
Inicializa la velocidad y dirección de la tercera bala.
- **Función**:
  - Genera una velocidad aleatoria para la bala dentro del rango de 400 a 500.
  - Establece la velocidad de la bala en los ejes `x` e `y`.
  - Marca la bala como disparada (`disp3=true`).

### Acciones del Jugador

#### `correr()`
Hace que el jugador corra.
- **Función**:
  - Establece la velocidad horizontal del jugador a 150.

#### `saltar()`
Hace que el jugador salte.
- **Función**:
  - Si el jugador está en la posición `x` mayor o igual a 200, lo mueve hacia atrás.
  - Si no, establece la velocidad vertical del jugador a -270 para permitir el salto.

#### `atras()`
Hace que el jugador retroceda.
- **Función**:
  - Establece la velocidad horizontal del jugador a -150.

#### `Retrceder()`
Detiene el movimiento horizontal del jugador.
- **Función**:
  - Establece la velocidad horizontal del jugador a 0.

### Colisiones

#### `colisionH()`
Pausa el juego cuando ocurre una colisión.
- **Función**:
  - Llama a la función `pausa()` para pausar el juego.

### Restablecimiento de Variables

#### `resetVariables()`
Restablece las propiedades de la primera bala.
- **Función**:
  - Detiene la bala y la reposiciona.
  - Marca la bala como no disparada (`disp=false`).

#### `resetVariables2()`
Restablece las propiedades de la segunda bala.
- **Función**:
  - Detiene la bala y la reposiciona.
  - Marca la bala como no disparada (`disp2=false`).

#### `resetVariables3()`
Restablece las propiedades de la tercera bala.
- **Función**:
  - Detiene la bala y la reposiciona.
  - Marca la bala como no disparada (`disp3=false`).

#### `resetPlayer()`
Reposiciona el jugador a su posición inicial.
- **Función**:
  - Establece la posición `x` del jugador a 50.

### Utilidades

#### `velocidadRandom(min, max)`
Genera un número aleatorio dentro de un rango.
- **Parámetros**:
  - `min`: El valor mínimo del rango.
  - `max`: El valor máximo del rango.
- **Función**:
  - Retorna un número aleatorio entre `min` y `max`.

#### `render()`
Función de renderización, actualmente vacía.
- **Función**:
  - No realiza ninguna acción, se puede usar para personalizar el renderizado del juego.

El codigo con todo lo necesario para correrlo se encuentra en la siguiente liga: [Proyecto 3](https://itecm-my.sharepoint.com/:f:/g/personal/l20120097_morelia_tecnm_mx/EqH2fVTDrHBDrTtfPYeoNO8Bt9_ST9z-0hnQWndTufhg_g?e=KccBsi)
