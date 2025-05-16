## Reporte
1. Aceleración constante:

Comportamiento: El objeto comienza a moverse lentamente, pero a medida que pasa el tiempo, su velocidad aumenta de manera continua. El movimiento es predecible y constante.

Por qué: La aceleración no cambia, por lo que el objeto siempre se mueve en la misma dirección y a una velocidad que crece de manera uniforme.

``` js
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255);
  
  // Aceleración constante
  mover.applyForce(createVector(0.1, 0)); // Aceleración en la dirección X
  
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

2. Aceleración aleatoria:

Comportamiento: El objeto se mueve de manera muy errática, con movimientos impredecibles en todas direcciones. La velocidad varía constantemente y el objeto parece "saltar" de un lado a otro.

Por qué: Al aplicar una aceleración aleatoria, las fuerzas que afectan al objeto cambian constantemente, lo que hace que el objeto se mueva de manera no lineal y caótica.

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

3. Aceleración hacia el mouse:

Comportamiento: El objeto tiende a moverse hacia el puntero del mouse. La aceleración aumenta cuando el objeto está lejos y disminuye cuando se acerca.

Por qué: La aceleración siempre está dirigida hacia el mouse, por lo que el objeto se "atrae" hacia él. La magnitud de la aceleración depende de la distancia entre el objeto y el puntero.

``` js
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255);
  
  // Aceleración hacia el mouse
  let mouseForce = createVector(mouseX - mover.position.x, mouseY - mover.position.y);
  mouseForce.setMag(0.1); // Magnitud de la aceleración hacia el mouse
  mover.applyForce(mouseForce);

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

Conclusión:

Al variar el tipo de aceleración, observamos que cada una produce un tipo distinto de movimiento. La aceleración constante resulta en un movimiento predecible, la aleatoria crea un movimiento caótico, y la aceleración hacia el mouse produce un movimiento que parece seguir al puntero, con una respuesta dinámica.
