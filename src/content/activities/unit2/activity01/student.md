## Suma de Vectores
La suma de vectores se hace sumando sus componentes una por una. En JavaScript con Three.js, la mejor forma de sumarlos es usando el método .add(). Es decir, A=(Ax,Ay,Az) 𝐵=(𝐵𝑥,𝐵𝑦,𝐵𝑧), entonces la suma es A+B=(Ax+Bx,Ay+By,Az+Bz).
## El error
position.add(velocity); funciona porque position es un objeto Vector3, y .add() es un método que sabe cómo sumar correctamente. position = position + velocity; no funciona porque JavaScript no sabe cómo sumar objetos directamente.
