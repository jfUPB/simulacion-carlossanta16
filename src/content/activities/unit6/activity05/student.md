## Comparaciones

### Diferencias fundamentales

La principal diferencia entre ambos algoritmos está en dónde residen las reglas que guían el comportamiento de los agentes:

Flow Fields: la inteligencia está en el entorno. El espacio contiene un campo vectorial que define cómo debe moverse un agente en cada punto. El agente solo consulta el campo y sigue la dirección indicada.

Flocking: la inteligencia está en los agentes y sus interacciones. Cada boid observa a sus vecinos y ajusta su comportamiento según tres reglas (separación, alineación y cohesión), sin necesidad de un entorno con estructura previa.

En resumen:
* Flow Fields → movimiento guiado desde el exterior (entorno).
* Flocking → movimiento guiado desde el interior (interacción entre agentes).

## Tipos de comportamiento emergente

Flow Fields genera trayectorias suaves, controladas y predecibles, lo cual es ideal para simular cosas como:

* Viento o corrientes de agua.

* Tinta dispersándose en el agua.

* Movimiento “hipnótico” o repetitivo de partículas.

Flocking, por otro lado, genera comportamientos sociales y orgánicos, ideales para simular:

* Grupos de seres vivos (aves, peces, personas).

* Recuerdos, pensamientos, o incluso emociones conectadas.

* Dinámicas más impredecibles y visualmente más complejas.

En mi pieza “Memories”, logré un comportamiento suave pero caótico de memorias agrupándose o alejándose, cosa que sería mucho más difícil de lograr con un flow field tradicional.

## Ventajas y desventajas

Flow Fields

Ventajas:

* Fácil de controlar visualmente.

* Predecible y suave.

* Excelente para representar medios físicos (viento, fuego, fluido).

Desventajas:

* Poco realista para comportamientos sociales.

* Falta de interacción entre partículas/agentes.

Flocking

Ventajas:

* Comportamiento más orgánico y social.

* Más potencial para emergencia.

* Versátil para simular lo vivo o lo simbólico.

Desventajas:

* Más difícil de estabilizar.

* Mayor consumo de recursos si hay muchos agentes.

## El agente autónomo

Ambos algoritmos me ayudaron a entender que un agente autónomo:

* Tiene una identidad propia (posición, velocidad, dirección).

* Decide su comportamiento con base en información local (vecinos o entorno).

* No necesita una autoridad central para funcionar.

* Puede generar comportamientos colectivos complejos.

En Flow Fields, el agente es como una partícula obediente.

En Flocking, es como un individuo social que reacciona al grupo.

## Emergencia

La emergencia la observé claramente cuando:

* En Flocking, un grupo de boids comenzaba a formar patrones inesperados, como remolinos, agrupaciones compactas o “decisiones colectivas” sobre hacia dónde moverse, sin que eso estuviera programado explícitamente.

* En mi pieza Memories, algunos boids parecían “perseguir” a otros o “huir”, generando dinámicas emocionales sutiles. El caos aparente tomaba forma con el tiempo.

* Esa es la magia de la emergencia: reglas simples → resultados complejos y sorprendentes.
