## Proceso Generativo (Algoritmo)
### Lógica Central:

El sistema se basa en un sistema de partículas dentro de un flow field dinámico, combinado con un campo de fuerzas controlado por la música (usando amplitud y FFT). Las partículas reaccionan a un campo vectorial que fluye según el ritmo, y sus comportamientos se modifican con ruido Perlin alterado por frecuencia.

También hay formas geométricas pulsantes (diamantes, corazones abstractos) que giran y cambian de color según bandas de frecuencia específicas. Todo se mezcla en una atmósfera glam, líquida y con glitchs visuales en ciertos momentos.

### Técnicas Usadas:

* Sistema de partículas con aceleración y velocidad modificadas por FFT.

* Flow field dinámico guiado por ruido Perlin modulado por la amplitud.

* Ruido Perlin para modificar direcciones, colores y suavidad de movimientos.

* Visuales geométricos sincronizados con la música.

* Aleatoriedad controlada: usando randomSeed() inicializado por amplitud y pequeños cambios pseudoaleatorios en condiciones iniciales (colores base, dirección del flow, posiciones).

### Modulación por Inputs (Audio + Interacción)

Audio Inputs:

1. Amplitud:

* Controla la cantidad de partículas emitidas por frame.

* Modula el brillo y opacidad general.

* Afecta la dirección del flow field (modifica el offset del Perlin noise en X/Y).

2. FFT (frecuencias):

* Graves (0–100 Hz): aumentan la cohesión entre partículas, atrayéndose entre sí.

* Medios (100–500 Hz): cambian el ángulo de rotación de las formas geométricas (como corazones/diamantes).

* Agudos (500–1024 Hz): disparan destellos, chispas, colores neón y aumentan la velocidad máxima de partículas.

### Interacción:
MouseX: cambia la paleta de color activa (rosados, neón, dorados, monocromo).

MouseY: cambia la intensidad del flow field (cuánto afectan las fuerzas a las partículas).

Tecla “F”: alterna entre dos estilos: “fantasía líquida” y “geometría glam”.

Tecla “G”: provoca un glitch temporal: líneas cortadas, distorsiones, inversión de colores.

Tecla “R”: reinicia el sistema con nuevas condiciones aleatorias (seed, posiciones iniciales).

### Outputs Visuales

Elementos Visuales Generados:

1. Partículas:

* Forma: círculos o polígonos irregulares.

* Propiedades dinámicas: posición, velocidad, tamaño, color, opacidad.

* Comportamiento: se mueven según flow field y FFT.

2. Formas geométricas:

* Corazones, diamantes, estrellas abstractas.

* Aparecen según picos de frecuencia media-alta.

* Rotan, vibran y pulsan.

3. Destellos y texturas:

* Emitidos por agudos fuertes.

* Se generan en zonas aleatorias (aleatoriedad controlada).

* Colores brillantes (neón, blanco puro).

4. Glitchs:

* Líneas entre partículas que se distorsionan.

* Inversión de colores, ruido estático y efectos tipo “televisión rota”.

### Propiedades Modificables Dinámicamente:

* Posición (según flow y fuerzas).

* Tamaño (por amplitud).

* Velocidad (por FFT).

* Color/Brillo (por amplitud y mouseX).

* Opacidad (por FFT).

* Rotación de formas (frecuencias medias).

* Generación de partículas/destellos (amplitud y agudos).

### Naturaleza Generativa / No Repetitiva

Cada ejecución tiene condiciones iniciales distintas:

* randomSeed() se ajusta a una mezcla de amplitud + tiempo.

* El campo de ruido Perlin tiene offset variable.

* Las posiciones iniciales de partículas y colores base cambian cada vez.

El uso de ruido Perlin + música + interacción garantiza que la visualización no será idéntica aunque la canción sea la misma.

El input humano (mouse y teclas) también influye en el resultado final en tiempo real.
