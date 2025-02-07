## Pregunta
¿Qué pasa si cambiamos la posición del objeto usando aceleración en lugar de velocidad constante y lo hacemos rebotar en los bordes?
## Hipótesis
Si introducimos aceleración, el objeto cambiará su velocidad y su dirección de forma progresiva, en lugar de moverse con una velocidad constante. Esto generará un movimiento más fluido y dinámico. Además, al hacer que rebote en los bordes, en lugar de simplemente "aparecer en el lado opuesto", podemos simular un rebote realista en el que la dirección del movimiento cambia al llegar a los bordes.
## Resultado
``` js
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255);
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-2, 2), random(-2, 2));
    this.acceleration = createVector(0, 0); // Aceleración inicial
    this.damping = 0.98;
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.mult(this.damping);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.velocity.x *= -1;
      this.position.x = width;
    } else if (this.position.x < 0) {
      this.velocity.x *= -1; 
      this.position.x = 0;
    }

    if (this.position.y > height) {
      this.velocity.y *= -1; 
      this.position.y = height;
    } else if (this.position.y < 0) {
      this.velocity.y *= -1; 
      this.position.y = 0; 
    }
  }

  applyForce(force) {
    this.acceleration.add(force);
  }
}
```
* El objeto ya no se mueve con velocidad constante, sino que tiene aceleración, lo que hace que su velocidad cambie con el tiempo.
* Hemos añadido un factor de "atenuación" para que el objeto no siga acelerando indefinidamente, simulando la fricción en el entorno.
* Cuando el objeto toca los bordes, su velocidad se invierte, simulando un rebote.
## Explicación
* La aceleración es una forma de modificar la velocidad de manera progresiva, lo que crea movimientos más naturales y dinámicos.
* Al invertir la velocidad en los bordes, conseguimos un comportamiento de rebote realista, donde la dirección del movimiento cambia al llegar a los límites de la pantalla.
## Conclusión
Al agregar aceleración y rebote, el objeto ahora tiene un movimiento más fluido y realista. Su velocidad cambia gradualmente, y cuando llega a los bordes, rebota en lugar de desaparecer o teleportarse. Esto simula un entorno más físico y dinámico.
