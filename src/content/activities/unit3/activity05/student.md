## Entrega
### Problema
El problema con la implementación dada en applyForce(force) es que estamos sobrescribiendo la aceleración en cada llamada en lugar de acumular las fuerzas.

Si en un mismo frame se aplican varias fuerzas (como el viento y la gravedad), la última llamada a applyForce() simplemente reemplazará la aceleración anterior, ignorando cualquier otra fuerza aplicada antes.

Por ejemplo:
``` js
mover.applyForce(wind);
mover.applyForce(gravity);
```
Esto hace que solo la última fuerza aplicada tenga efecto, lo cual no es correcto según la Segunda Ley de Newton.
### Solución 
Para solucionar este problema, en lugar de reemplazar la aceleración, debemos sumar todas las fuerzas aplicadas. 
Y ya que establecimos que la masa es 1.
La corrección en el método applyForce(force) sería sumar la fuerza a la aceleración en cada frame en lugar de sobrescribirla:
``` js
applyForce(force) {
  this.acceleration.add(force);
}
```
### Implementación en p5.js
``` js
let mover;

function setup() {
    createCanvas(640, 360);
    mover = new Mover();
}

function draw() {
    background(255);
    
    let wind = createVector(0.1, 0);
    let gravity = createVector(0, 0.2);
    
    mover.applyForce(wind);
    mover.applyForce(gravity);
    
    mover.update();
    mover.checkEdges();
    mover.show();
}

class Mover {
    constructor() {
        this.position = createVector(width / 2, height / 2);
        this.velocity = createVector(0, 0);
        this.acceleration = createVector(0, 0);
    }

    applyForce(force) {
        this.acceleration.add(force); 
    }

    update() {
        this.velocity.add(this.acceleration);
        this.position.add(this.velocity);
        this.acceleration.mult(0); 
    }

    checkEdges() {
        if (this.position.x > width) {
            this.position.x = width;
            this.velocity.x *= -1;
        }
        if (this.position.y > height) {
            this.position.y = height;
            this.velocity.y *= -1;
        }
    }

    show() {
        fill(50);
        ellipse(this.position.x, this.position.y, 20, 20);
    }
}
```
