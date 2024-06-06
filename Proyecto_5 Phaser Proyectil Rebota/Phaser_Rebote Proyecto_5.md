# Proyecto 5 -Phaser Rebote

## Objetivo:

- Editar el Juego Phaser para que esquive proyectiles que rebota por el plano
- Diseña una red neuronal para que el juego sea capaz de aprender patrones de movimeinto y pueda jugarse de forma automatica.

### Variables Globales
- `w`: Ancho del juego.
- `h`: Alto del juego.
- `jugador`: Objeto representando al jugador.
- `fondo`: Imagen de fondo del juego.
- `bala`: Objeto representando la bala.
- `menu`: Imagen de menú.
- `cursors`: Referencia a las teclas de cursor.
- `key_der`, `key_izq`, `key_up`, `key_down`: Teclas de flecha.
- `reset`: Función para reiniciar el juego.
- `velocidadBala`: Velocidad inicial de la bala.
- `coordenada_X`, `coordenada_Y`, `dis_bala_jugador`: Coordenadas y distancia entre objetos.
- `estado_der`, `estado_izq`, `estado_arriba`, `estado_abajo`: Estados de movimiento del jugador.
- `jugadorPosInicial`, `balaPosInicial`: Posiciones iniciales del jugador y la bala.
- `timer`: Control del tiempo en el juego.
- `regresar`: Booleano para el movimiento de la bala.
- `nnNetwork`, `nnEntrenamiento`, `nnSalida`, `datosEntrenamiento`: Variables relacionadas con la red neuronal.
- `modoAuto`, `eCompleto`: Modo de juego y estado del entrenamiento.
- `juego`: Instancia del juego Phaser.

### Funciones
- `preload()`: Precarga de recursos del juego.
- `create()`: Creación de elementos del juego y configuración inicial.
- `update()`: Actualización del juego en cada fotograma.
- `render()`: Renderizado opcional de elementos.


### Funciones

#### `enRedNeural()`
- Entrena la red neuronal con los datos de entrenamiento.
- Parámetros:
  - `datosEntrenamiento`: Datos para el entrenamiento de la red.
- Devuelve un mensaje de confirmación por consola.

#### `datosDeEntrenamiento(param_entrada)`
- Calcula la salida de la red neuronal dadas las entradas.
- Parámetros:
  - `param_entrada`: Entradas para la red neuronal.
- Devuelve la acción a realizar por el jugador basada en la salida de la red.

#### `pausa()`
- Pausa el juego y muestra el menú de pausa en el centro de la pantalla.

#### `mPausa(event)`
- Maneja la pausa del juego y las interacciones con el menú de pausa.
- Parámetros:
  - `event`: Evento de clic del ratón.
- Permite reiniciar el juego o entrenar la red neuronal.

#### `resetVariables()`
- Restablece las variables del juego a sus valores iniciales.
- Restablece la velocidad y posición de la bala y del jugador.

#### `derecha()`, `izquierda()`, `arriba()`, `abajo()`
- Mueven al jugador a la posición correspondiente y actualizan los estados de movimiento.

#### `update()`
- Actualiza el estado del juego en cada fotograma.
- Gestiona el movimiento del jugador y la bala, la interacción con la red neuronal y la recopilación de datos de entrenamiento.

#### `posicion_inical()`
- Devuelve al jugador a su posición inicial si ha pasado un cierto tiempo desde el movimiento.

#### `colisionH()`
- Maneja la colisión entre la bala y el jugador, pausando el juego.

#### `render()`
- Función de renderizado opcional que no hace nada en este caso.

El codigo completo con todo lo necesario para poder correrlo se encunetra el la siguiente liga: [Proyecto 5](https://itecm-my.sharepoint.com/:f:/g/personal/l20120097_morelia_tecnm_mx/EqH2fVTDrHBDrTtfPYeoNO8Bt9_ST9z-0hnQWndTufhg_g?e=KccBsi)
