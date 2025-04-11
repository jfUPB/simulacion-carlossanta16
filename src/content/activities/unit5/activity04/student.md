## Bitácora

1. En mi proyecto, gestioné la creación de partículas utilizando un arreglo que almacena cada instancia nueva que se genera, ya sea por una interacción como el micrófono o por una condición específica.
   Para evitar que el programa se sobrecargue de partículas viejas, a cada una le asigné una vida útil mediante una variable lifespan, que se va reduciendo con el tiempo. Una vez que esa vida llega a cero, la partícula se elimina del arreglo con el método splice().
   Esto me permite mantener la memoria controlada y evitar fugas que podrían afectar el rendimiento a largo plazo.

2. El marco de movimiento motion 101 se basa en que las fuerzas afectan la aceleración, la aceleración modifica la velocidad y la velocidad actualiza la posición. En mis clases, utilicé esta estructura como base para el movimiento de las partículas.
   Cada partícula tiene sus propias propiedades de posición, velocidad y aceleración. En el método update(), primero sumo la aceleración a la velocidad y luego la velocidad a la posición. Después de cada actualización, reinicio la aceleración para que pueda volver a acumular fuerzas en el siguiente ciclo.
   Esta forma de trabajar me permitió simular un movimiento más realista y dinámico.

3. En mi proyecto apliqué distintas fuerzas externas a las partículas. Una de ellas fue la gravedad, que implementé como un vector constante hacia abajo.
   También trabajé con la resistencia del aire, que simulé disminuyendo levemente la velocidad de las partículas en cada actualización, multiplicando la velocidad por un valor menor a 1.
   Además, en la clase SpringParticle añadí una fuerza de resorte que tira a la partícula hacia un punto de anclaje, utilizando una fórmula proporcional a la distancia entre ambos puntos.
   También experimenté con una fuerza derivada del micrófono, que respondía al volumen y afectaba el movimiento. Estas fuerzas permitieron crear comportamientos variados y visualmente interesantes.

4. Para implementar herencia, primero creé una clase base llamada Particle que contiene todas las propiedades y métodos comunes a cualquier tipo de partícula.
   Luego, creé una subclase llamada SpringParticle que hereda de Particle, lo cual me permitió reutilizar código y agregar comportamientos más complejos sin partir de cero.
   A través del polimorfismo, redefiní algunos métodos en la subclase, como update() y display(), para que respondieran de forma diferente a las condiciones específicas del resorte. Esto me ayudó a crear una estructura flexible y extensible para distintos tipos de partículas.
