## Modificaciones

1. Relación entre r y theta con las posiciones x y y

Las coordenadas polares representan un punto en un espacio 2D usando:

* r: La distancia del punto al origen.
* theta: El ángulo desde el eje X positivo.
  
Para convertirlas a coordenadas cartesianas, usamos las fórmulas:

𝑥 = 𝑟⋅cos⁡(𝜃)

𝑦 = 𝑟⋅sin⁡(𝜃)

En el código original:

``` js
let x = r * cos(theta);
let y = r * sin(theta);
```

Esto coloca el punto en la pantalla según su distancia al origen y su ángulo de rotación.

### ¿Qué ocurre con la segunda modificación?
Modificación:

``` js
let v = p5.Vector.fromAngle(theta);
```

Ahora v es un vector unitario con magnitud 1, ya que p5.Vector.fromAngle(theta) crea un vector de longitud 1 apuntando en la dirección de theta.

Pero se comete un error en esta línea:

``` js
line(0, 0, x, y);  // x y y no existen en esta versión
```

x e y ya no están definidos, por lo que el código no funciona. Si corregimos esto usando v.x y v.y, lo que veremos es que el punto se mueve en un círculo de radio 1 porque r no se usa, por lo que el vector mantiene una magnitud fija.

### ¿Qué ocurre con la tercera modificación?
Modificación:

``` js
let v = p5.Vector.fromAngle(theta, r);
```

Aquí estamos creando un vector con una magnitud específica r en la dirección de theta. Esto significa que el punto ahora se moverá en un círculo con radio r, en lugar de solo usar un vector unitario.

Esto es equivalente a hacer:

``` js
let x = r * cos(theta);
let y = r * sin(theta);
```

Pero usando p5.Vector. La diferencia es que p5.Vector encapsula la conversión y permite operaciones vectoriales más fácilmente.

