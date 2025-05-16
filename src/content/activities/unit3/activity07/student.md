## Problema
El problema principal es que force es un objeto de la clase p5.Vector, lo que significa que se pasa por referencia en JavaScript. Cuando se divide force por 10 usando force.div(10), se está modificando directamente el vector original en lugar de una copia. Esto implica que cualquier otro uso de force en otro contexto también se verá afectado, lo cual es un comportamiento no deseado.

### Solución propuesta:

En lugar de modificar directamente force, se debe crear una copia del vector y luego modificar la copia antes de sumarla a acceleration. En p5.js, esto se puede hacer utilizando el método copy() de p5.Vector:

``` js
applyForce(force) {
    let f = force.copy();
    f.div(10);
    this.acceleration.add(f);
}
```

### Explicación:

1. Se crea una copia de force usando copy(), asegurando que el vector original no se modifique.

2. Se divide la copia entre 10 para aplicar la relación de masa correctamente.

3. Se agrega la fuerza resultante a la aceleración sin afectar el estado externo de force.

Con esta corrección, cada applyForce() manejará las fuerzas de manera independiente y evitará modificar accidentalmente vectores que podrían ser utilizados en otros cálculos. Esto garantiza un comportamiento más predecible y realista en la simulación.
