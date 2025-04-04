## Paso por valor y paso por referencia

### Paso por Valor

Cuando una variable se asigna por valor, significa que se copia el contenido de la variable original en una nueva ubicación de memoria. Cualquier modificación a la nueva variable no afectará la variable original. En JavaScript, los tipos de datos primitivos (números, booleanos, strings, etc.) se asignan por valor.

### Paso por Referencia

Cuando una variable se asigna por referencia, significa que ambas variables apuntan al mismo objeto en memoria. Si se modifica una, la otra también reflejará esos cambios. En JavaScript, los objetos, arreglos y otras estructuras de datos complejas se asignan por referencia.

### Aplicación en el Fragmento de Código

``` js
let friction = this.velocity.copy();
let friction = this.velocity;
``` 
En la primera línea:
``` js
let friction = this.velocity.copy();
```
Aquí, copy() genera una nueva instancia del objeto, lo que significa que friction es una copia independiente de this.velocity. Cualquier cambio en friction no afectará this.velocity, ya que son dos objetos diferentes en la memoria.

En la segunda línea:
``` js
let friction = this.velocity;
```
Aquí, friction no es una nueva instancia, sino una referencia a this.velocity. Esto significa que cualquier cambio en friction afectará directamente a this.velocity, ya que ambos apuntan al mismo objeto en memoria.

### ¿Qué podría salir mal?

Si friction se modifica después de la asignación con this.velocity, también se modificarán los valores de this.velocity, lo que puede generar errores inesperados en el comportamiento del programa. Por ejemplo, si friction se usa para calcular una fuerza de frenado y se modifica, la velocidad del objeto podría cambiar de manera no intencionada.
