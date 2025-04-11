## Motion 101
### Modificación necesaria para incluir fuerzas acumulativas

Cuando queremos agregar fuerzas, es necesario hacer que la aceleración sea acumulativa en cada frame. Esto se logra reiniciando la aceleración después de cada actualización para evitar que las fuerzas previas sigan afectando el objeto indefinidamente.

``` js
velocity.add(acceleration);
position.add(velocity);
acceleration.mult(0); // Reset después de aplicar fuerzas
```

Este reinicio es crucial porque en el modelo de fuerzas, la aceleración no es constante sino el resultado de varias fuerzas aplicadas en cada momento.

### Identificación del Attractor y cambio de color

El Attractor es un objeto en la simulación que genera una fuerza atractiva sobre otros objetos. Para cambiar su color, podemos modificar su función display():

``` js
fill(0, 255, 0); // Cambiar el color del Attractor a verde
```
### Modificación para mover el Attractor con el mouse y cambiar su color al pasar sobre él

Para permitir que el Attractor sea arrastrado con el mouse y cambie de color cuando el cursor esté sobre él, podemos modificar su código agregando estas funciones:

``` js
class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.dragging = false;
    this.rollover = false;
  }

  update() {
    if (this.dragging) {
      this.position.set(mouseX, mouseY);
    }
  }

  display() {
    noStroke();
    fill(this.rollover ? color(255, 0, 0) : color(0, 255, 0)); // Rojo si el mouse está encima
    ellipse(this.position.x, this.position.y, 20, 20);
  }

  checkMouse() {
    let d = dist(mouseX, mouseY, this.position.x, this.position.y);
    this.rollover = d < 10;
  }

  pressed() {
    if (this.rollover) {
      this.dragging = true;
    }
  }

  released() {
    this.dragging = false;
  }
}

function mousePressed() {
  attractor.pressed();
}

function mouseReleased() {
  attractor.released();
}
```

Esto hace que:

* Si el mouse está sobre el Attractor, cambia su color.
* Si se hace clic en él, se puede arrastrar.
* Cuando se suelta el botón, deja de moverse.
