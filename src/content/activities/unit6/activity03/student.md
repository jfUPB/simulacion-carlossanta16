## Flocking

### Reglas fundamentales
Separación (Separation)

* Objetivo: Evitar el hacinamiento, que los boids no se monten unos encima de otros.

* Lógica: Calcula un vector de fuerza que apunta lejos de cada vecino que esté demasiado cerca. Suma esos vectores y los promedia, para luego aplicarlo al movimiento del boid.

* Efecto: Esta fuerza hace que cada boid mantenga distancia mínima respecto a sus vecinos.

Alineación (Alignment)

* Objetivo: Coordinarse en la misma dirección general que el grupo cercano.

* Lógica: Calcula el promedio de las velocidades de los boids vecinos. La fuerza resultante apunta hacia ese promedio, guiando al boid a moverse en sincronía.

* Efecto: Los boids tienden a volar en la misma dirección, como una bandada bien organizada.

Cohesión (Cohesion)

* Objetivo: Mantener unido al grupo, evitar que se dispersen.

* Lógica: Calcula la posición promedio de los vecinos cercanos. La fuerza apunta hacia ese centro, atrayendo al boid al grupo.

* Efecto: Los boids se agrupan, manteniendo coherencia como un solo enjambre.

### Parámetros Clave

* perceptionRadius: define el rango dentro del cual un boid considera a otros como “vecinos”.

* maxforce: la fuerza máxima que puede aplicar un boid para cambiar su aceleración (generalmente valores como 0.05).

* maxspeed: velocidad máxima que puede alcanzar (ej: 2 o 4).

* Pesos para reglas: en muchos ejemplos se aplican pesos como separation.mult(1.5);, alignment.mult(1.0);, cohesion.mult(1.0);.

### Modificación

Aumenté drásticamente el peso de Separación y reduje a cero el de Cohesión, dejando Alineación normal.

```js
separation.mult(3.0); // Separación con mucho más peso
alignment.mult(1.0);  // Alineación normal
cohesion.mult(0.0);   // Sin cohesión
```

El enjambre se desorganiza: los boids ya no se atraen al centro del grupo y tienden a dispersarse. Algunos aún se mueven en la misma dirección (alineación), pero se ve una especie de enjambre inestable y abierto, como si el grupo estuviera colapsando hacia el caos. Se forman pequeños subgrupos o líneas temporales, pero no se mantiene un centro.

* Con cohesión en 0, el enjambre se rompe.
* Con separación muy alta, cada boid quiere estar solo.
