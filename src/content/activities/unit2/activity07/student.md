## Motion 101
El concepto de Motion 101 en p5.js se basa en usar vectores para controlar el movimiento de un objeto en términos de posición, velocidad y aceleración. En lugar de modificar manualmente la posición de un objeto:

* Posición (position): Representa dónde está el objeto en el lienzo.
* Velocidad (velocity): Es el cambio en la posición por cada fotograma.
* Aceleración (acceleration): Cambia la velocidad con el tiempo, creando movimientos suaves.

En cada draw(), la nueva posición se obtiene así:

posición+ = velocidad
velocidad+ = aceleración
## Ejemplo
``` js
let position;
let velocity;
let acceleration;

function setup() {
    createCanvas(500, 300);
    position = createVector(50, height / 2); 
    velocity = createVector(0, 0); 
    acceleration = createVector(0.05, 0); 
}

function draw() {
    background(220);

    velocity.add(acceleration); 
    position.add(velocity); 

    fill(255, 0, 0);
    ellipse(position.x, position.y, 30, 30); 

    if (position.x > width) {
        position.x = 0;
        velocity.mult(0); 
    }
}
```
* En el ejemplo la pelota se mueve de izquierda a derecha acelerando hasta que toque el borde derecho del canvas, una vez lo toque, se reinicia la simulación.
