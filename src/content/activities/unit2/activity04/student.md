## mag() y magSq()
El método mag() calcula la magnitud (o norma) de un vector, es decir, su longitud en el espacio.
El método magSq() devuelve el cuadrado de la magnitud del vector, sin calcular la raíz cuadrada.
### Cuál es más eficiente?
magSq() es más eficiente porque evita la operación costosa de calcular la raíz cuadrada. Si solo necesitas comparar magnitudes sin el valor exacto, magSq() es la mejor opción.
## Normalize
Esto es útil para trabajar con direcciones sin alterar las proporciones de los vectores.
El método normalize() convierte un vector en un vector unitario (de magnitud 1) manteniendo su dirección original. Se calcula dividiendo cada componente del vector por su magnitud.
## dot() explicado a un periodista
El producto punto (dot product) mide cuánta influencia tiene un vector sobre otro en términos de alineación. Si es positivo, apuntan en una dirección similar; si es cero, son perpendiculares; si es negativo, apuntan en direcciones opuestas.
## Diferencia entre la versión estática e instancia de dot()
* Versión de instancia: v1.dot(v2) calcula el producto punto entre el vector v1 y v2.
* Versión estática: Vector.dot(v1, v2) hace lo mismo, pero sin necesidad de que v1 sea un objeto de la clase.
  
La versión estática es útil cuando no tienes una instancia de vector y solo quieres operar sobre dos vectores dados.
## Interpretación geométrica del producto cruz
El producto cruz (cross product) de dos vectores en 3D genera un tercer vector perpendicular a ambos. Su orientación sigue la regla de la mano derecha y su magnitud representa el área del paralelogramo formado por los dos vectores de entrada.

Donde θ es el ángulo entre los vectores.

* Si los vectores son paralelos, el resultado es cero (no hay área).
* Si son ortogonales, el resultado es máximo.
## ¿Para qué sirve el método dist()?
El método dist(v1, v2) calcula la distancia euclidiana entre dos vectores (puntos en el espacio). Es útil para calcular proximidad, detección de colisiones, o seguimiento de objetivos.
## normalize() y limit()
* normalize(): Ajusta un vector para que tenga magnitud 1 sin cambiar su dirección.
* limit(): Restringe la magnitud de un vector a un valor máximo sin alterar su dirección. Es útil en sistemas físicos para evitar velocidades excesivas o mantener movimientos controlados.
