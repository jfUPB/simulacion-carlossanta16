### Entrega
## Motion 101

En el código proporcionado, el marco Motion 101 está presente en la estructura general del objeto Mover, ya que sigue estos principios:

* Posición (position): Representa la ubicación del objeto en el espacio.
* Velocidad (velocity): Define qué tan rápido y en qué dirección se mueve.
* Aceleración (acceleration): Modifica la velocidad con el tiempo.

``` js
update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
}
```

## ¿Cuáles eran los algoritmos usados en la unidad anterior para definir la aceleración?
``` js
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255);

  // Aceleración aleatoria
  let randomForce = createVector(random(-0.1, 0.1), random(-0.1, 0.1)); // Aceleración aleatoria
  mover.applyForce(randomForce);

  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-2, 2), random(-2, 2));
    this.acceleration = createVector(0, 0);
    this.damping = 0.98;
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.mult(this.damping);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }
```

* Comportamiento: El objeto se mueve de manera muy errática, con movimientos impredecibles en todas direcciones. La velocidad varía constantemente y el objeto parece “saltar” de un lado a otro.

* Por qué: Al aplicar una aceleración aleatoria, las fuerzas que afectan al objeto cambian constantemente, lo que hace que el objeto se mueva de manera no lineal y caótica.

## Relación a las leyes de Newton

1. Primera ley (Inercia):
* Si no hay aceleración (this.acceleration = 0), el objeto seguirá en reposo o en movimiento uniforme en línea recta.
2. Segunda ley (Fuerza = masa × aceleración, F = ma):
* En el código, la aceleración (this.acceleration) actúa como una fuerza aplicada al objeto.
La aceleración cambia la velocidad, lo que genera movimiento.
Si quisiéramos aplicar la ecuación completa, podríamos modificar la aceleración en función de la masa:

``` js
let fuerza = createVector(0.2, 0);
this.acceleration = p5.Vector.div(fuerza, this.mass);
```

3. Tercera ley (Acción y reacción):
* Si el objeto choca contra un borde (checkEdges()), podría rebotar con una velocidad inversa, simulando la reacción a la fuerza aplicada.










