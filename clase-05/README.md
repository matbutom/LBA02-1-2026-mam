# clase-05

Jueves 3 de septiembre de 2026

Profesor: Christian Oyarzun Roa
Correo: coyarzun@error404.cl

## Apuntes de p5.js

### Arreglos

Un **arreglo** o **array** es una estructura que permite guardar varios valores
en una sola variable.

En JavaScript se escriben usando corchetes `[]`.

```js
let numeros = [10, 20, 30, 40];
let nombres = ["Ana", "Pedro", "Sofia"];
let colores = ["red", "blue", "yellow"];
```

Un arreglo sirve para organizar información que pertenece a un mismo grupo:
posiciones, tamaños, colores, nombres, velocidades, figuras, sonidos, etc.

Sin arreglos, habría que crear muchas variables separadas:

```js
let x1 = 100;
let x2 = 200;
let x3 = 300;
```

Con un arreglo, esos valores pueden guardarse juntos:

```js
let posicionesX = [100, 200, 300];
```

Esto hace que el código sea más ordenado y más fácil de modificar.

### Índices

Cada elemento de un arreglo tiene una posición llamada **índice**.

En JavaScript, los índices empiezan en `0`, no en `1`.

```js
let colores = ["red", "blue", "yellow"];
```

En este arreglo:

- `colores[0]` es `"red"`.
- `colores[1]` es `"blue"`.
- `colores[2]` es `"yellow"`.

Para acceder a un elemento se escribe el nombre del arreglo y luego el índice
entre corchetes:

```js
let primerColor = colores[0];
```

También se puede usar directamente dentro de una función de p5.js:

```js
fill(colores[1]);
circle(200, 200, 80);
```

En este caso, el círculo se dibuja con el segundo color del arreglo.

### Cambiar un elemento

Los valores de un arreglo pueden cambiarse indicando su índice.

```js
let tamanos = [20, 40, 60];

tamanos[1] = 100;
```

Después de esa instrucción, el arreglo queda así:

```js
[20, 100, 60]
```

Esto permite modificar datos durante el programa, por ejemplo cambiar una
posición, reemplazar un color o actualizar el tamaño de una figura.

### length

`.length` indica cuántos elementos tiene un arreglo.

```js
let numeros = [10, 20, 30, 40];

print(numeros.length);
```

El resultado sería `4`, porque el arreglo tiene cuatro elementos.

`.length` es muy útil cuando se combina con un ciclo `for`, porque permite
recorrer todos los elementos sin tener que escribir manualmente la cantidad.

```js
let colores = ["red", "blue", "yellow"];

for (let i = 0; i < colores.length; i++) {
  print(colores[i]);
}
```

En cada vuelta del ciclo, `i` funciona como índice:

- cuando `i` vale `0`, se lee `colores[0]`;
- cuando `i` vale `1`, se lee `colores[1]`;
- cuando `i` vale `2`, se lee `colores[2]`.

### Recorrer un arreglo con for

Recorrer un arreglo significa revisar sus elementos uno por uno.

Esto se hace mucho en p5.js para dibujar varias figuras usando datos guardados
en un arreglo.

```js
let posicionesX = [80, 160, 240, 320, 400];

function setup() {
  createCanvas(500, 300);
}

function draw() {
  background(240);

  for (let i = 0; i < posicionesX.length; i++) {
    circle(posicionesX[i], 150, 50);
  }
}
```

En este ejemplo, cada número del arreglo se usa como posición `x` de un
círculo.

El ciclo evita escribir esto:

```js
circle(80, 150, 50);
circle(160, 150, 50);
circle(240, 150, 50);
circle(320, 150, 50);
circle(400, 150, 50);
```

### Agregar elementos con push()

`push()` agrega un elemento al final de un arreglo.

```js
let numeros = [10, 20, 30];

numeros.push(40);
```

Después de usar `push()`, el arreglo queda así:

```js
[10, 20, 30, 40]
```

En p5.js, `push()` puede servir para guardar información mientras el programa
está funcionando.

```js
let puntosX = [];
let puntosY = [];

function setup() {
  createCanvas(500, 300);
}

function draw() {
  background(240);

  for (let i = 0; i < puntosX.length; i++) {
    circle(puntosX[i], puntosY[i], 20);
  }
}

function mousePressed() {
  puntosX.push(mouseX);
  puntosY.push(mouseY);
}
```

En este ejemplo, cada vez que se hace clic se guarda la posición del mouse en
dos arreglos. Luego el `for` dibuja todos los puntos guardados.

### Quitar elementos con pop()

`pop()` elimina el último elemento de un arreglo.

```js
let numeros = [10, 20, 30, 40];

numeros.pop();
```

Después de usar `pop()`, el arreglo queda así:

```js
[10, 20, 30]
```

Puede usarse para borrar el último dato agregado, como si fuera un deshacer
simple.

```js
function keyPressed() {
  if (key == "z") {
    puntosX.pop();
    puntosY.pop();
  }
}
```

Si los datos están relacionados, como `puntosX` y `puntosY`, es importante
agregar y quitar elementos en ambos arreglos al mismo tiempo.

### Arreglos y color

Los arreglos son útiles para guardar paletas de color.

```js
let paleta = ["#f72585", "#7209b7", "#3a0ca3", "#4cc9f0"];

function setup() {
  createCanvas(500, 300);
  noStroke();
}

function draw() {
  background(240);

  for (let i = 0; i < paleta.length; i++) {
    fill(paleta[i]);
    circle(100 + i * 100, 150, 70);
  }
}
```

En este caso, el índice `i` sirve para elegir un color y también para calcular
la posición de cada círculo.

### Elegir un elemento al azar

Se puede usar `random()` para elegir un elemento aleatorio de un arreglo.

Como los índices deben ser números enteros, se combina con `floor()`.

```js
let palabras = ["linea", "punto", "forma", "ritmo"];

let indice = floor(random(palabras.length));
let palabra = palabras[indice];
```

`random(palabras.length)` entrega un número entre `0` y la cantidad de elementos
del arreglo. `floor()` redondea ese número hacia abajo, para que pueda usarse
como índice.

En p5.js también se puede usar `random()` directamente sobre un arreglo:

```js
let palabra = random(palabras);
```

Esta forma es más corta, pero es importante entender primero la versión con
índice, porque ayuda a comprender cómo funciona el arreglo por dentro.

### Arreglos de objetos

Un arreglo también puede guardar objetos.

Esto es útil cuando cada elemento necesita tener varias propiedades, por
ejemplo posición, tamaño, color y velocidad.

```js
let circulos = [
  { x: 100, y: 150, tamano: 40, color: "red" },
  { x: 200, y: 150, tamano: 70, color: "blue" },
  { x: 300, y: 150, tamano: 50, color: "yellow" }
];

function setup() {
  createCanvas(400, 300);
  noStroke();
}

function draw() {
  background(240);

  for (let i = 0; i < circulos.length; i++) {
    fill(circulos[i].color);
    circle(circulos[i].x, circulos[i].y, circulos[i].tamano);
  }
}
```

En este ejemplo, cada objeto representa un círculo completo. El arreglo guarda
la colección de círculos.

### Arreglos vacíos

Un arreglo puede partir vacío.

```js
let puntos = [];
```

Esto significa que todavía no tiene elementos, pero se pueden agregar después
con `push()`.

Los arreglos vacíos son útiles cuando no se sabe de antemano cuántos elementos
va a tener el programa. Por ejemplo:

- cantidad de clics del usuario;
- partículas que aparecen durante una animación;
- puntos de un dibujo;
- textos escritos en pantalla;
- posiciones guardadas en el tiempo.

### Clases

Una **clase** es una especie de molde para crear objetos.

Si un objeto permite agrupar datos relacionados, una clase permite definir cómo
serán muchos objetos parecidos.

Por ejemplo, si se quiere dibujar muchos círculos, cada círculo podría tener:

- una posición `x`;
- una posición `y`;
- un tamaño;
- un color;
- una velocidad.

En vez de escribir cada círculo a mano, se puede crear una clase `Circulo`.

```js
class Circulo {
  constructor(x, y, tamano, color) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
    this.color = color;
  }
}
```

En este ejemplo, `Circulo` es el nombre de la clase. Por convención, los nombres
de las clases suelen empezar con mayúscula.

### constructor

`constructor()` es una función especial que se ejecuta cuando se crea un nuevo
objeto a partir de una clase.

Sirve para recibir los valores iniciales del objeto.

```js
class Circulo {
  constructor(x, y, tamano) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
  }
}
```

Los valores entre paréntesis, como `x`, `y` y `tamano`, son parámetros. Esos
parámetros llegan desde afuera cuando se crea el objeto.

```js
let miCirculo = new Circulo(100, 200, 50);
```

En este caso:

- `x` recibe `100`;
- `y` recibe `200`;
- `tamano` recibe `50`.

### this

`this` significa "este objeto".

Dentro de una clase, `this` se usa para guardar y leer las propiedades del
objeto que se está creando o usando.

```js
class Circulo {
  constructor(x, y, tamano) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
  }
}
```

En este ejemplo:

- `x` es el parámetro que llega al constructor;
- `this.x` es la propiedad guardada dentro del objeto.

Aunque se llamen parecido, no son exactamente lo mismo.

```js
this.x = x;
```

Esta línea puede leerse así: "guarda el valor de `x` dentro de la propiedad
`x` de este objeto".

Sin `this`, el valor queda solo como una variable temporal del constructor y no
queda guardado en el objeto.

### new

`new` se usa para crear un objeto nuevo a partir de una clase.

```js
let circulo1 = new Circulo(100, 150, 40);
let circulo2 = new Circulo(250, 150, 80);
```

Aunque ambos objetos vienen de la misma clase, cada uno tiene sus propios datos.

```js
print(circulo1.x); // 100
print(circulo2.x); // 250
```

La clase es el molde. Los objetos creados con `new` son las copias concretas.

### Métodos

Un **método** es una función que pertenece a una clase.

Sirve para definir acciones que el objeto puede realizar.

```js
class Circulo {
  constructor(x, y, tamano, color) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
    this.color = color;
  }

  dibujar() {
    fill(this.color);
    circle(this.x, this.y, this.tamano);
  }
}
```

En este caso, `dibujar()` es un método. Está dentro de la clase y usa `this`
para acceder a las propiedades del objeto.

Para llamar un método se usa punto:

```js
let miCirculo = new Circulo(100, 150, 60, "red");

miCirculo.dibujar();
```

### Métodos para movimiento

Una clase puede tener más de un método.

Por ejemplo, se puede separar la acción de dibujar y la acción de moverse.

```js
class Circulo {
  constructor(x, y, tamano, color) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
    this.color = color;
    this.velocidadX = random(-2, 2);
    this.velocidadY = random(-2, 2);
  }

  mover() {
    this.x = this.x + this.velocidadX;
    this.y = this.y + this.velocidadY;
  }

  dibujar() {
    fill(this.color);
    circle(this.x, this.y, this.tamano);
  }
}
```

El método `mover()` cambia la posición del objeto. El método `dibujar()` muestra
el objeto en pantalla.

Separar acciones en métodos hace que el código sea más ordenado y más fácil de
leer.

### Clases y arreglos

Las clases se combinan muy bien con los arreglos.

Un arreglo puede guardar muchos objetos creados con la misma clase.

```js
let circulos = [];

function setup() {
  createCanvas(500, 300);
  noStroke();

  for (let i = 0; i < 20; i++) {
    let x = random(width);
    let y = random(height);
    let tamano = random(20, 80);
    let colorCirculo = random(["red", "blue", "yellow", "black"]);

    circulos.push(new Circulo(x, y, tamano, colorCirculo));
  }
}

function draw() {
  background(240);

  for (let i = 0; i < circulos.length; i++) {
    circulos[i].mover();
    circulos[i].dibujar();
  }
}

class Circulo {
  constructor(x, y, tamano, color) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
    this.color = color;
    this.velocidadX = random(-2, 2);
    this.velocidadY = random(-2, 2);
  }

  mover() {
    this.x = this.x + this.velocidadX;
    this.y = this.y + this.velocidadY;
  }

  dibujar() {
    fill(this.color);
    circle(this.x, this.y, this.tamano);
  }
}
```

En este ejemplo:

- `circulos` es un arreglo vacío;
- `new Circulo(...)` crea un objeto nuevo;
- `push()` guarda ese objeto dentro del arreglo;
- el `for` de `draw()` recorre todos los objetos;
- cada objeto ejecuta sus propios métodos `mover()` y `dibujar()`.

### Crear objetos con el mouse

También se pueden crear objetos mientras el programa está funcionando.

```js
let circulos = [];

function setup() {
  createCanvas(500, 300);
  noStroke();
}

function draw() {
  background(240);

  for (let i = 0; i < circulos.length; i++) {
    circulos[i].dibujar();
  }
}

function mousePressed() {
  let tamano = random(20, 80);
  let colorCirculo = random(["red", "blue", "yellow"]);

  circulos.push(new Circulo(mouseX, mouseY, tamano, colorCirculo));
}

class Circulo {
  constructor(x, y, tamano, color) {
    this.x = x;
    this.y = y;
    this.tamano = tamano;
    this.color = color;
  }

  dibujar() {
    fill(this.color);
    circle(this.x, this.y, this.tamano);
  }
}
```

Cada clic crea un nuevo objeto `Circulo` en la posición del mouse y lo guarda en
el arreglo.

### ¿Por qué usar clases?

Las clases ayudan cuando un programa tiene muchos elementos parecidos, pero cada
uno necesita guardar sus propios datos.

Por ejemplo:

- muchas partículas;
- muchas pelotas;
- muchas letras;
- muchas líneas;
- muchos botones;
- muchas figuras que se mueven de manera independiente.

Una clase permite juntar datos y acciones en un solo lugar. En vez de tener
variables sueltas, cada objeto sabe dónde está, cómo se ve y qué puede hacer.

### Errores comunes

- Olvidar que el primer índice es `0`.
- Intentar leer un índice que no existe.
- Escribir `colores(0)` en vez de `colores[0]`.
- Usar `i <= arreglo.length` en vez de `i < arreglo.length`.
- Cambiar un arreglo relacionado y olvidar cambiar el otro.
- Escribir `this.x = x` fuera de una clase o método donde `this` no corresponde.
- Olvidar usar `new` cuando se crea un objeto desde una clase.
- Definir un método con `function dibujar()` dentro de una clase. Dentro de una
  clase se escribe solo `dibujar()`.
- Intentar usar una propiedad sin `this`, por ejemplo escribir `x` cuando se
  debería escribir `this.x`.

Por ejemplo, este ciclo tiene un error:

```js
for (let i = 0; i <= colores.length; i++) {
  print(colores[i]);
}
```

El problema es que `i <= colores.length` llega a un índice que no existe.

La forma correcta es:

```js
for (let i = 0; i < colores.length; i++) {
  print(colores[i]);
}
```

### Ideas importantes

- Un arreglo guarda varios valores en una sola variable.
- Los arreglos se escriben con corchetes `[]`.
- Cada elemento tiene un índice.
- El primer índice siempre es `0`.
- `.length` indica la cantidad de elementos del arreglo.
- `push()` agrega un elemento al final.
- `pop()` elimina el último elemento.
- Un ciclo `for` permite recorrer un arreglo completo.
- Los arreglos sirven para guardar posiciones, colores, tamaños, textos y
  objetos.
- En p5.js ayudan a crear dibujos, animaciones y sistemas visuales con muchos
  elementos.
- Una clase es un molde para crear objetos.
- `constructor()` define los valores iniciales de un objeto.
- `this` significa "este objeto" y permite acceder a sus propiedades.
- `new` crea un objeto nuevo a partir de una clase.
- Un método es una función que pertenece a una clase.
- Las clases sirven para organizar objetos que tienen datos y acciones propias.
- Los arreglos pueden guardar muchos objetos creados con una clase.
