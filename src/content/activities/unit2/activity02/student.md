## Código con Vectores (Actividad 3, Unidad 1)
``` js
class Walker {
  constructor() {
    this.position = createVector(width / 2, height / 2); // Usamos un vector
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y);
  }

  step() {
    let step = createVector(0, 0); // Vector de movimiento inicializado en (0,0)
    let choice = floor(random(4));

    if (choice === 0) {
      step.set(1, -1);  // Movimiento en diagonal arriba-derecha
    } else if (choice === 1) {
      step.set(-1, 1); // Movimiento en diagonal abajo-izquierda
    } else if (choice === 2) {
      step.set(1, 1);  // Movimiento en diagonal abajo-derecha
    } else {
      step.set(-1, -1); // Movimiento en diagonal arriba-izquierda
    }

    this.position.add(step); // Sumamos el vector de movimiento a la posición
  }
}

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}
```
### ¿Qué cambia con p5.Vector?
* this.x y this.y se reemplazan por this.position (un p5.Vector).
* En vez de modificar x e y con ++ o --, usamos this.position.add(step).
* step.set(x, y) define el movimiento en cada iteración.

Este enfoque hace el código más limpio y flexible, permitiendo extenderlo con otras operaciones vectoriales más adelante.
