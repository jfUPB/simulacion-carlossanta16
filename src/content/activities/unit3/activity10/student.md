## Simulaciones
### Friccion
``` js
let ball;

function setup() {
  createCanvas(600, 400);
  ball = new Ball(width / 2, height / 2);
}

function draw() {
  background(220);
  ball.applyFriction(0.05);
  ball.update();
  ball.display();
}

class Ball {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(5, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  applyFriction(mu) {
    let friction = this.velocity.copy();
    friction.normalize();
    friction.mult(-1 * mu);
    this.applyForce(friction);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    fill(0);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}
```

https://editor.p5js.org/carlossanta16/sketches/wSukPPeNs
### Resistencia de aire y fluidos
```js
let ball;

function setup() {
  createCanvas(600, 400);
  ball = new Ball(width / 2, 50);
}

function draw() {
  background(220);
  let gravity = createVector(0, 0.2);
  ball.applyForce(gravity);
  ball.applyDrag(0.02);
  ball.update();
  ball.display();
}

class Ball {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  applyDrag(c) {
    let drag = this.velocity.copy();
    drag.normalize();
    let speedSq = this.velocity.magSq();
    drag.mult(-c * speedSq);
    this.applyForce(drag);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    fill(0);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}
```
https://editor.p5js.org/carlossanta16/sketches/vg0cC7EAY

### Fuerza gravitacional
``` js
let planet, ball;

function setup() {
  createCanvas(600, 400);
  planet = new Attractor(width / 2, height / 2, 20);
  ball = new Ball(random(width), random(height / 2));
}

function draw() {
  background(220);
  let force = planet.attract(ball);
  ball.applyForce(force);
  ball.update();
  planet.display();
  ball.display();
}

class Ball {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    fill(0);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}

class Attractor {
  constructor(x, y, mass) {
    this.position = createVector(x, y);
    this.mass = mass;
    this.G = 1;
  }

  attract(mover) {
    let force = p5.Vector.sub(this.position, mover.position);
    let distance = constrain(force.mag(), 5, 25);
    let strength = (this.G * this.mass * mover.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  display() {
    fill(255, 0, 0);
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
}
```

https://editor.p5js.org/carlossanta16/sketches/aD33ItLmL

## Explicacion

* Fricción: La bola se mueve hasta que la fricción la detiene.
* Resistencia del aire: La bola cae y su velocidad disminuye debido a la resistencia.
* Atracción gravitacional: Una bola es atraída por un "planeta" rojo en el centro.

