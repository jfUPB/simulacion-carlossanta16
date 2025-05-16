## Fuerza Neta
En el método update() del objeto mover, la aceleración se multiplica por cero al final de cada frame. Esto es un paso crucial para asegurar que la aceleración no se acumule incorrectamente en cada iteración del bucle de actualización.

Para entender por qué es necesario hacer esto, consideremos cómo funciona la física en este sistema. La aceleración es la consecuencia de la suma de todas las fuerzas aplicadas a un objeto, de acuerdo con la Segunda Ley de Newton:

Dado que en cada frame pueden actuar múltiples fuerzas sobre el objeto, estas fuerzas se suman en la variable acceleration mediante el método applyForce(). Sin embargo, en la naturaleza, las fuerzas sobre un objeto pueden cambiar de un instante a otro, dependiendo del contexto (por ejemplo, el viento puede cambiar de dirección, la gravedad puede ser la única fuerza presente, etc.).

Si no reiniciamos la aceleración a cero al final de cada frame, estaríamos acumulando valores de aceleración de frames anteriores, lo cual es físicamente incorrecto. En cada frame, la aceleración debe calcularse únicamente en función de las fuerzas actuales que actúan sobre el objeto en ese momento.

El orden en update() es clave:

* Se actualiza la velocidad sumando la aceleración.

* Se actualiza la posición sumando la velocidad.

* Se multiplica la aceleración por cero (this.acceleration.mult(0)).

Multiplicar la aceleración por cero al final del método update() garantiza que en el siguiente frame el objeto comience sin aceleración previa, y solo se le sumen las nuevas fuerzas que se le apliquen en ese instante.

En resumen, la aceleración debe resetearse a cero en cada frame para que el cálculo de las fuerzas sea correcto y refleje de manera precisa el estado actual del sistema físico. De lo contrario, el objeto acumularía aceleración incorrectamente, lo que llevaría a un comportamiento irreal en la simulación.
