## Implementación - G.U.Y by Lady Gaga Visualizer

### Configuración p5.sound

Primero cargo el audio con loadSound() dentro de preload(). Luego lo reproduzco en loop en setup(). Para analizar el audio uso:

* p5.FFT() para obtener el espectro de frecuencias.

* p5.Amplitude() para el nivel general del audio.

``` js
let audio;
let fft, amp;

function preload() {
  audio = loadSound('assets/guy.mp3');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  fft = new p5.FFT();
  amp = new p5.Amplitude();
  audio.loop();
}
```

### Extracción de datos de audio

Con fft.getEnergy(banda) obtengo la energía (amplitud) de ciertas bandas de frecuencia para detectar kick, snare, etc.

``` js
let kick = fft.getEnergy(20, 100);   // Bajo (kick)
let snare = fft.getEnergy(150, 250); // Banda media (snare)
let level = amp.getLevel();           // Nivel general del audio
```

### Modulación del algoritmo generativo con datos de audio

Uso estos valores para modular diferentes parámetros:

* El flow field cambia con level para hacerlo más dinámico.

* El tamaño y pulso del corazón responde directamente a kick + snare.

* El movimiento de partículas se influye con el flow field que varía con el audio.

``` js
// Actualizar flow field con ruido modulado por nivel de audio
zoff += level * 0.1;

// Dibujar corazón pulsando según kick + snare
let beat = map(kick + snare, 0, 510, 1, 2.5, true);
scale(baseScale * beat);
```

### Control visual basado en audio

* El corazón cambia su escala pulsando fuertemente con los beats detectados.

* Las partículas ADN se mueven siguiendo un flow field que cambia con el audio.

* Aparecen palabras en pantalla sincronizadas con golpes de kick o snare fuertes.

``` js
// Partículas siguiendo flow field modulado por audio
for (let p of particles) {
  p.follow(flowField);
  p.update();
  p.display();
}

// Mostrar palabras cuando kick o snare son fuertes
if (tiempo > 8.7 && (kick > 180 || snare > 170)) {
  palabras.push(new Palabra(random(["ART", "RAVE", "APHRODITE", "VENUS"])));
}
``` 

## Implementación - G.U.Y by Lady Gaga Visualizer

``` js
// === Variables Globales ===
let particles = [];
let flowField;
let cols, rows;
let inc = 0.1;
let scl = 20;
let zoff = 0;
let audio;
let fft, amp;
let glitch = false;
let paleta = 0;
let modoGlam = false;
let seed;
let palabras = [];

// === Preload Audio ===
function preload() {
  audio = loadSound('assets/guy.mp3');
}

// === Setup Inicial ===
function setup() {
  createCanvas(windowWidth, windowHeight);
  cols = floor(width / scl);
  rows = floor(height / scl);
  flowField = new Array(cols * rows);

  fft = new p5.FFT();
  amp = new p5.Amplitude();
  audio.loop();

  seed = millis();
  randomSeed(seed);
  noiseSeed(seed);

  for (let i = 0; i < 200; i++) {
    particles.push(new ADNParticle(random(width), random(height)));
  }
}

// === Dibujar por Frame ===
function draw() {
  background(0, 40); // Fondo translúcido negro

  if (glitch) {
    filter(INVERT);
  }

  let level = amp.getLevel();
  let spectrum = fft.analyze();
  let bass = fft.getEnergy(20, 150);
  let mid = fft.getEnergy(150, 500);

  // Detectar kick y snare
  let kick = fft.getEnergy(20, 100);
  let snare = fft.getEnergy(150, 250);
  let tiempo = audio.currentTime();

  // Flow field dinámico
  let yoff = 0;
  for (let y = 0; y < rows; y++) {
    let xoff = 0;
    for (let x = 0; x < cols; x++) {
      let index = x + y * cols;
      let angle = noise(xoff, yoff, zoff) * TWO_PI * 4;
      let v = p5.Vector.fromAngle(angle);
      v.setMag(1);
      flowField[index] = v;
      xoff += inc;
    }
    yoff += inc;
  }
  zoff += level * 0.1;

  // Dibujar partículas ADN
  for (let p of particles) {
    p.follow(flowField);
    p.update();
    p.display();
  }

  // Corazón central más pequeño y con pulso fuerte
  push();
  translate(width / 2, height / 2);

  let baseScale = 0.6; // Tamaño base más pequeño
  let beat = map(kick + snare, 0, 510, 1, 2.5, true); // Pulso más intenso y limitado

  rotate(sin(frameCount * 0.1) * 0.3);
  scale(baseScale * beat);

  noStroke();
  fill(255, 0, 100);
  beginShape();
  for (let t = 0; t <= 360; t += 1) {
    let rad = radians(t);
    let x = 16 * pow(sin(rad), 3);
    let y = 13 * cos(rad) - 5 * cos(2 * rad) - 2 * cos(3 * rad) - cos(4 * rad);
    vertex(x * 15, -y * 15);
  }
  endShape(CLOSE);
  pop();

  // Palabras ART / RAVE / APHRODITE / VENUS
  if (tiempo > 8.7 && (kick > 180 || snare > 170)) {
    let opciones = ["ART", "RAVE", "APHRODITE", "VENUS"];
    palabras.push(new Palabra(random(opciones)));
  }

  for (let i = palabras.length - 1; i >= 0; i--) {
    palabras[i].update();
    palabras[i].display();
    if (palabras[i].isDone()) {
      palabras.splice(i, 1);
    }
  }
}

// === Partícula ADN ===
class ADNParticle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.maxSpeed = 4;
    this.history = [];
    this.angle = random(TWO_PI);
    this.r = random(2, 6);
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    this.history.push(this.pos.copy());
    if (this.history.length > 30) this.history.splice(0, 1);

    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  follow(vectors) {
    let x = floor(this.pos.x / scl);
    let y = floor(this.pos.y / scl);
    let index = x + y * cols;
    let force = vectors[index];
    this.applyForce(force);
  }

  display() {
    noFill();
    stroke(lerpColor(color("magenta"), color("cyan"), sin(this.angle)));
    beginShape();
    for (let i = 0; i < this.history.length; i++) {
      let p = this.history[i];
      vertex(p.x + sin(i * 0.3 + frameCount * 0.1) * 10, p.y + cos(i * 0.3 + frameCount * 0.1) * 10);
    }
    endShape();
    this.angle += 0.1;
  }
}

// === Palabras ===
class Palabra {
  constructor(txt) {
    this.txt = txt;
    this.x = random(width * 0.1, width * 0.9);
    this.y = random(height * 0.1, height * 0.9);
    this.alpha = 255;
    this.size = 60;
  }

  update() {
    this.alpha -= 5;
  }

  display() {
    textAlign(CENTER, CENTER);
    textSize(this.size);
    fill(255, this.alpha);
    text(this.txt, this.x, this.y);
  }

  isDone() {
    return this.alpha <= 0;
  }
}

// === Teclas ===
function keyPressed() {
  if (key === 'G' || key === 'g') glitch = !glitch;
  if (key === 'F' || key === 'f') modoGlam = !modoGlam;
  if (key === 'R' || key === 'r') {
    seed = millis();
    randomSeed(seed);
    noiseSeed(seed);
    particles = [];
    for (let i = 0; i < 200; i++) {
      particles.push(new ADNParticle(random(width), random(height)));
    }
    palabras = [];
  }
}

function mouseMoved() {
  paleta = floor(map(mouseX, 0, width, 0, 4));
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

``` 

https://editor.p5js.org/carlossanta16/sketches/HpmbPmHbv

![Obra GUY](../../../../assets/OBRAGUY.mp4)







