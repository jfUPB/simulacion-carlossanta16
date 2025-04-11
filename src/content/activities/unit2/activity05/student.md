## Código
``` js
let t = 0; 
let direction = 1; 

function setup() {
    createCanvas(500, 500);
}

function draw() {
    background(200);
    translate(width / 2, height / 2); 

    let scaleFactor = 2;
    let v0 = createVector(0, 0);
    let v1 = createVector(30, 0).mult(scaleFactor); 
    let v2 = createVector(0, 30).mult(scaleFactor); 

    let hypotenuse = p5.Vector.sub(v2, v1); 
    
    let v3 = p5.Vector.lerp(v1, v2, t);

    let dynamicColor = lerpColor(color('red'), color('blue'), t);

    drawArrow(v0, v1, 'red');    
    drawArrow(v0, v2, 'blue');   
    drawArrow(v1, hypotenuse, 'green'); 
    drawArrow(v0, v3, dynamicColor); 

    t += 0.01 * direction;

    if (t >= 1 || t <= 0) {
        direction *= -1; 
    }
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```
## lerp() y lerpColor()
La función lerp() se usa para encontrar un valor intermedio entre dos números.

* start: Valor inicial.
* end: Valor final.
* t: Un número entre 0 y 1, que indica cuánta interpolación se debe hacer.
* t = 0 - Devuelve start.
* t = 1 - Devuelve end.
* t = 0.5 - Devuelve el punto medio entre start y end.

lerpColor() es similar a lerp(), pero en lugar de interpolar entre números, interpola entre dos colores.

* color1: Color inicial.
* color2: Color final.
* t: Un valor entre 0 y 1 que indica cuánto interpolar entre los colores.

## drawArrow()
drawArrow() toma un punto de inicio y un vector de dirección, y dibuja una flecha en la dirección del vector.

1. push() y pop()
* Guarda el estado del lienzo antes de transformarlo y lo restaura después.
2. stroke(myColor) y fill(myColor)
* Define el color de la flecha.
3. translate(base.x, base.y)
* Mueve el origen al punto de inicio de la flecha.
4. line(0, 0, vec.x, vec.y)
* Dibuja la línea de la flecha desde (0,0) hasta la punta del vector.
5. rotate(vec.heading())
* Gira el lienzo en la dirección del vector.
6. triangle(...)
* Dibuja la punta de la flecha en el extremo de la línea.
