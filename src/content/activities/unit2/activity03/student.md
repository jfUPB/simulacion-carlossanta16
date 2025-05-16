## Experimento
## Que espero obtener?
Espero que el código modifique el vector posicion dentro de la función playingVector(v) y que cuando imprima posicion después de la llamada, este tenga los valores (20, 30).
``` js
console.log(posicion.toString()); // → "p5.Vector { x: 20, y: 30 }"
```
## Que resultado obtuve?
Si agrego la impresión en setup() después de modificar el vector:
```js
console.log(posicion.toString());
```
El resultado en la consola del navegador es:
``` js
p5.Vector { x: 20, y: 30 }
```
Esto confirma que la función playingVector(v) sí modificó el vector original.
## Paso por valor vs paso por referencia en JavaScript
En JavaScript, los tipos primitivos (Number, String, Boolean, null, undefined, Symbol, BigInt) se pasan por valor, lo que significa que se copia el valor al pasar a una función.
Los objetos, incluidos p5.Vector, se pasan por referencia, lo que significa que cuando se pasa un objeto a una función, la función recibe una referencia al objeto original y puede modificarlo directamente.
### Paso por valor (no modifica la variable original)
``` js
function cambiarNumero(n) {
    n = 50; // Cambia solo la copia local
}
let numero = 10;
cambiarNumero(numero);
console.log(numero); // Sigue siendo 10 (No se modifica)
```
### Paso por referencia (modifica el objeto original)
``` js
function cambiarVector(v) {
    v.x = 50; // Modifica el objeto original
}
let vector = createVector(10, 20);
cambiarVector(vector);
console.log(vector.toString()); // "p5.Vector { x: 50, y: 20 }"
```
## Tipo de paso
Se está realizando paso por referencia, ya que p5.Vector es un objeto, y al pasarlo como parámetro a playingVector(v), cualquier modificación que se haga dentro de la función afecta directamente al objeto original.
## Aprendizaje
* Los tipos primitivos se pasan por valor, lo que significa que no pueden ser modificados dentro de una función.
* Los objetos (como p5.Vector) se pasan por referencia, lo que permite modificarlos dentro de una función sin necesidad de retornarlos.
* En p5.js, modificar un vector dentro de una función afecta el objeto original.
* Si quiero evitar que una función modifique el vector original, debo hacer una copia con .copy().
``` js
function safeVectorChange(v) {
    let newVector = v.copy(); // Se hace una copia
    newVector.x = 50;
    return newVector;
}
let vec = createVector(10, 20);
let newVec = safeVectorChange(vec);
console.log(vec.toString());
console.log(newVec.toString());
```
