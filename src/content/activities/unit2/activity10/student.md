## Intención de Diseño
Esta pieza interactiva busca simular un ecosistema acuático donde los renacuajos reaccionan al sonido del entorno. 
La idea es que el usuario pueda "asustarlos" con su voz, provocando que su color cambie de verde a morado y que sus movimientos se vuelvan erráticos. 
A medida que el sonido disminuye, los renacuajos recuperan su estado de calma, volviendo al verde y moviéndose de forma más pausada.
## Motion 101
1. *Forces & Motion* - Se usa una fuerza que varía con la entrada del micrófono para modificar la velocidad y dirección de los renacuajos. A mayor volumen, mayor intensidad de movimiento.
2. *Velocity & Acceleration* - Se implementa aceleración para dar un comportamiento más natural a las partículas, asegurando que reaccionen de manera progresiva en lugar de cambios bruscos.
3. *Constraints* - Se evita que los renacuajos escapen del canvas invirtiendo su dirección cuando tocan los bordes, lo que refuerza la idea de un "charco" delimitado.
4. *Randomness & Noise* - Se introduce aleatoriedad en los movimientos cuando el volumen es alto, simulando el comportamiento errático de un renacuajo asustado.
5. *Color Interpolation* - Se usa interpolación de color para transformar la apariencia de los renacuajos según la intensidad del sonido, creando una conexión visual con la interacción sonora.
## Referentes
* Casey Reas & Ben Fry - Inspiración en el uso de partículas y visualización generativa.
* Myriam Bleau - Uso del sonido como parámetro de transformación visual en tiempo real.
* Ecología - Comportamiento de renacuajos y su respuesta a estímulos externos en hábitats naturales.
