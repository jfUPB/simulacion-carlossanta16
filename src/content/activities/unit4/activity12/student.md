## Análisis

El concepto principal utilizado en esta obra es la oscilación de resortes acoplados, donde los nodos están conectados por muelles ideales que intentan mantener una distancia de equilibrio. Este sistema es análogo a las oscilaciones en una red de partículas conectadas por fuerzas elásticas, como ocurre en las telas de araña o las estructuras flexibles en la naturaleza.

### Implementación:

* Se creó una malla de puntos conectados con "resortes" (objetos Spring).

* Cada resorte tiene una longitud de equilibrio y una fuerza restauradora proporcional a la diferencia entre la distancia real y la distancia ideal.

* La fuerza de restauración aplicada a los puntos crea una oscilación similar a la de un sistema de resortes, haciendo que la estructura vibre y se adapte dinámicamente a la interacción del usuario.

## Cómo funciona?

1. Arrastrar nodos: Al hacer clic sobre un nodo y arrastrarlo, se modifica la posición de ese punto, alterando la tensión en los resortes conectados. Al soltarlo, la estructura oscila hasta volver a su estado de equilibrio.

2. Cambio de color por tensión: Los resortes cambian de azul (relajado) a rojo (tensionado), permitiendo visualizar la energía en el sistema.

3. Deformación global: Múltiples interacciones pueden generar ondas que se propagan a través de la red, creando un efecto visual dinámico y fluido.

## Desafíos

1. Mantener la estabilidad de la simulación

* Problema: Cuando se aplicaban fuerzas demasiado grandes, la red colapsaba o los puntos se movían de manera errática.

* Solución: Se limitó la magnitud de las fuerzas aplicadas y se ajustó el coeficiente de restauración de los resortes para evitar oscilaciones incontroladas.

2. Optimizar la interacción con los nodos

* Problema: La detección del clic en los nodos no siempre era precisa, y a veces era difícil seleccionar el punto deseado.

* Solución: Se amplió el área de detección de los nodos y se implementó un método de selección basado en la distancia más cercana.

3. Hacer que la red se viera natural

* Problema: Sin un sistema de amortiguación, la oscilación continuaba indefinidamente, lo que no se sentía realista.

* Solución: Se introdujo una pequeña disipación de energía en los resortes, lo que permite que la red se estabilice con el tiempo.

## Aprendizaje

* Las oscilaciones no solo son útiles para simular movimiento realista, sino que pueden emplearse para crear comportamientos emergentes en arte generativo.

* La combinación de resortes y fuerzas dinámicas permite obtener formas orgánicas y patrones complejos a partir de reglas simples.

* La interactividad en tiempo real hace que la oscilación sea más intuitiva y expresiva, permitiendo que el usuario influya en la evolución del sistema.

* Experimentar con oscilaciones en estructuras visuales me ayudó a entender cómo el concepto de armonía y equilibrio en la física puede traducirse en una experiencia estética y lúdica.


