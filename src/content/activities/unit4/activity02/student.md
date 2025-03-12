## heading() y pop()
¿Qué hace la función heading()?

heading() devuelve el ángulo en radianes de un vector con respecto al eje X positivo. En este caso, obtiene la dirección del vector de velocidad para que el objeto apunte en la dirección en la que se mueve.

¿Qué hacen las funciones push() y pop()?

* push() guarda el estado actual del sistema de coordenadas (posición, rotación, etc.).
* pop() restaura el estado guardado con push(), evitando que las transformaciones afecten a otros elementos en la escena.

¿Qué hace rectMode(CENTER)?

Cambia la forma en que se dibujan los rectángulos. Por defecto, rect(x, y, w, h) toma (x,y) como la esquina superior izquierda. Con rectMode(CENTER), (x,y) se vuelve el centro del rectángulo, lo que facilita la rotación alrededor de su propio eje.

Relación entre el ángulo de rotación y el vector de velocidad

El ángulo de rotación del objeto es el mismo que el ángulo del vector de velocidad, lo que garantiza que el objeto siempre apunte en la dirección en la que se mueve.
