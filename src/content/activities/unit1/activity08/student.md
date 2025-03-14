## Intención de Diseño
El arte generativo es un reflejo del caos y el orden coexistiendo en un mismo espacio. Esta pieza busca capturar la esencia del movimiento natural, evocando la trayectoria impredecible de una bandada de aves, la danza de partículas en el viento o incluso el comportamiento errático de sistemas caóticos como una tormenta eléctrica.
A través del uso de ruido Perlin, Levy Flight y distribuciones no uniformes, se genera una obra en constante cambio, donde cada instante es irrepetible. La interacción del usuario convierte este arte en algo vivo: con el teclado, se puede acelerar o ralentizar el flujo, mientras que con el mouse se altera la distribución de las formas, como si se estuviera moldeando un torbellino de energía.
## Conceptos Utilizados
### Ruido Perlin: 
Se utiliza para calcular la dirección en la que se mueven las partículas, generando trayectorias más orgánicas y fluidas en comparación con un movimiento completamente aleatorio.
### Levy Flight: 
En ocasiones, algunas partículas hacen movimientos largos y abruptos para romper la uniformidad del patrón y añadir un nivel de caos controlado.
### Distribución Uniforme y No Uniforme: 
Las partículas se distribuyen inicialmente de manera uniforme, pero al hacer clic con el mouse, su posición se redistribuye siguiendo una distribución normal (gaussiana), concentrándolas en torno al punto de clic.
## Interactividad
### Teclado:
W: Aumenta la velocidad de las partículas.
S: Reduce la velocidad de las partículas.
R: Restablece la velocidad original.
### Mouse:
Al hacer clic, las partículas se reubican en torno a la posición del mouse, creando patrones caóticos instantáneos.
## Referentes
Para la construcción de esta pieza me inspiré en:
### Paul Bourke 
Y sus estudios sobre Levy Flight en simulaciones de comportamiento caótico.
### Casey Reas y Ben Fry 
Creadores de Processing, quienes han explorado la interactividad y el arte generativo en muchos de sus trabajos.
### Tyler Hobbs 
Artista generativo que emplea ruido Perlin y variaciones de distribución para producir texturas complejas y orgánicas.
