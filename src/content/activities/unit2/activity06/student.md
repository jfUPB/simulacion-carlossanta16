## Código
``` js
let t = 0;
let direction = 1;

function setup() {
    createCanvas(500, 500); // Aumentamos el tamaño del lienzo
}

function draw() {
    background(200);

    let baseX = map(mouseX, 0, width, -width / 4, width / 4);
    let baseY = map(mouseY, 0, height, -height / 4, height / 4);
    let base = createVector(baseX, baseY); // Base controlada por el mouse

    let scaleFactor = map(mouseX, 0, width, 1, 3); // La escala cambia con el mouse
    let v1 = createVector(30, 0).mult(scaleFactor); // Vector rojo
    let v2 = createVector(0, 30).mult(scaleFactor); // Vector azul

    let hypotenuse = p5.Vector.sub(v2, v1);
    let v3 = p5.Vector.lerp(v1, v2, t);

    let dynamicColor = lerpColor(color('red'), color('blue'), t);

    translate(width / 2, height / 2); // Centramos la escena

    drawArrow(base, v1, 'red'); 
    drawArrow(base, v2, 'blue'); 
    drawArrow(p5.Vector.add(base, v1), hypotenuse, 'green'); 
    drawArrow(base, v3, dynamicColor); 

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
## Solución 
* baseX y baseY se mapean desde mouseX y mouseY con map() para que la base de los vectores se mueva suavemente.
* base = createVector(baseX, baseY);
* Se usa map(mouseX, 0, width, 1, 3) para cambiar la escala de los vectores según la posición del mouse en el eje X.
* Esto hace que los vectores crezcan o se reduzcan dinámicamente.
