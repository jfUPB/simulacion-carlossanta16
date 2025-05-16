## Bitácora

1. Flujo de trabajo

El flujo de trabajo para integrar Matter.js en p5.js empieza configurando el motor físico en setup(). Ahí se inicializa el Engine y se extrae el World, se crean los cuerpos físicos (en mi caso, círculos que representaban letras) y se añaden al mundo con World.add(). También es donde se crean los límites del canvas (paredes invisibles) y se configura el MouseConstraint para interacción.

En draw(), primero se actualiza el motor de Matter con Engine.update(engine) y luego se dibujan los cuerpos. Es clave sincronizar las propiedades del cuerpo (posición y orientación) con los elementos visuales de p5.js, que en este caso eran círculos y texto que representaban cada letra.

2. Representación visual vs. simulación física

Matter.js gestiona las posiciones, colisiones y fuerzas físicas, pero su parte visual es mínima. Así que tuve que usar p5.js para dibujar lo que Matter.js estaba simulando.

El desafío fue mantener una representación clara de las letras (como texto dentro de burbujas) sin perder la conexión con el cuerpo físico que realmente colisiona y se mueve. Opté por cuerpos circulares porque son más fáciles de manejar y dan un efecto visual "suave", ideal para la palabra “flotar”. Si hubiese querido usar polígonos con forma exacta de letras, el proceso sería más complejo y tedioso.

3. Creación de formas complejas

En vez de crear formas exactas para cada letra, que es difícil con Matter.js (habría que usar Bodies.fromVertices() o importar SVGs), usé círculos como base para cada letra, y les dibujé la letra encima con text(). Esta técnica fue simple pero efectiva: se mantiene la simulación física realista mientras se representa tipográficamente la palabra.

Limitación: perdí un poco de detalle visual al no usar las formas reales de cada letra como cuerpo físico, pero a cambio gané fluidez y facilidad de implementación.

4. Física para la semántica

Usar física para representar una palabra fue muy efectivo en este caso. Elegí la palabra "FLOTAR", y reforcé su significado con:

* Gravedad negativa para que las letras subieran.

* Fuerzas suaves oscilantes para que parecieran impulsadas por el viento o el agua.

* Cuerpos ligeros y elásticos (con alta restitución).

Palabras que tienen significados relacionados al movimiento, fuerza, gravedad o interacción funcionan especialmente bien con esta técnica: caer, rebotar, repeler, romper, unir.

En cambio, conceptos más abstractos como tristeza o libertad serían más difíciles de simular directamente, aunque podrían trabajarse desde lo simbólico.

5. Potencial exploratorio

La combinación de p5.js y Matter.js tiene muchísimo potencial. No solo para tipografía animada, sino para:

* Esculturas digitales interactivas con física.

* Juegos educativos sobre fuerzas y movimiento.

* Visualizaciones abstractas con datos que afectan cuerpos.

* Experiencias sensoriales (p. ej. sonidos que afectan cuerpos físicos).

* Instalaciones de arte generativo en tiempo real.
