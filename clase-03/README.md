# clase-03

Jueves 20 de agosto de 2026

Profesor: Christian Oyarzun Roa
Correo: coyarzun@error404.cl

## Apuntes de p5.js

### Color y contorno

Antes de dibujar una figura, p5.js permite controlar cómo se ve: su relleno, su
borde o la ausencia de ambos.

#### fill()

`fill()` define el color de relleno de las figuras que se dibujan después.

```js
fill(255, 0, 0);
triangle(100, 300, 200, 100, 300, 300);
```

En este ejemplo, el triángulo se dibuja con relleno rojo.

#### stroke()

`stroke()` define el color del contorno o línea de las figuras que se dibujan
después.

```js
stroke(0);
quad(120, 300, 180, 100, 220, 100, 280, 300);
```

En este ejemplo, el cuadrilátero se dibuja con contorno negro.

#### noFill()

`noFill()` elimina el relleno de las figuras. La forma queda vacía por dentro y
solo se ve su contorno, si tiene `stroke()` activo.

```js
noFill();
stroke(0);
triangle(100, 300, 200, 100, 300, 300);
```

#### noStroke()

`noStroke()` elimina el contorno de las figuras. La forma queda definida solo por
su relleno, si tiene `fill()` activo.

```js
noStroke();
fill(0);
quad(120, 300, 180, 100, 220, 100, 280, 300);
```

### Formas primitivas

En p5.js, las formas primitivas son figuras básicas que se dibujan directamente
en el canvas mediante coordenadas. Sirven como unidades mínimas para construir
formas más complejas, como letras, íconos, patrones o sistemas gráficos.

#### rect()

`rect()` dibuja un rectángulo. Recibe la posición inicial en `x, y`, el ancho y
el alto.

```js
rect(x, y, ancho, alto);
```

Por ejemplo:

```js
rect(100, 100, 200, 80);
```

Esta forma puede servir para construir módulos, bloques, astas verticales,
fondos o estructuras geométricas simples.

#### ellipse()

`ellipse()` dibuja una elipse u óvalo. Recibe una posición en `x, y`, un ancho y
un alto.

```js
ellipse(x, y, ancho, alto);
```

Por ejemplo:

```js
ellipse(200, 200, 120, 80);
```

Si el ancho y el alto tienen el mismo valor, la elipse se ve como un círculo.

#### arc()

`arc()` dibuja una parte de una elipse. Sirve para hacer medios círculos, curvas,
sonrisas, ojos, cortes o fragmentos de una forma circular.

```js
arc(x, y, ancho, alto, anguloInicio, anguloFinal);
```

Los dos últimos valores indican desde qué ángulo hasta qué ángulo se dibuja el
arco. En p5.js, por defecto, esos ángulos se escriben en **radianes** usando
valores como `PI`.

```js
arc(200, 200, 120, 120, 0, PI);
```

Este ejemplo dibuja medio círculo. Algunos valores útiles son:

- `0`: inicio del círculo hacia la derecha
- `PI / 2`: un cuarto de vuelta
- `PI`: media vuelta
- `TWO_PI`: vuelta completa

También se puede usar `PI` para construir dibujos con partes circulares:

```js
noFill();
stroke(0);
strokeWeight(4);

arc(200, 180, 120, 120, PI, TWO_PI);
arc(200, 220, 120, 120, 0, PI);
```

En este caso, el primer arco dibuja la mitad superior de un círculo y el segundo
dibuja la mitad inferior.

#### Radianes

Los **radianes** son una forma de medir ángulos. En p5.js, muchas funciones que
trabajan con rotación o curvas usan radianes por defecto.

La idea principal es que una vuelta completa equivale a `TWO_PI`. Media vuelta
equivale a `PI`, y un cuarto de vuelta equivale a `PI / 2`.

```js
0        // 0 grados
PI / 2   // 90 grados
PI       // 180 grados
PI * 1.5 // 270 grados
TWO_PI   // 360 grados
```

Por ejemplo, para rotar una forma media vuelta:

```js
rotate(PI);
```

Y para dibujar un arco de un cuarto de círculo:

```js
arc(200, 200, 120, 120, 0, PI / 2);
```

#### rectMode()

`rectMode()` cambia la manera en que p5.js interpreta las coordenadas de
`rect()`.

```js
rectMode(CORNER);
rect(100, 100, 200, 80);
```

Con `CORNER`, la posición `x, y` indica la esquina superior izquierda del
rectángulo. Con `CENTER`, la posición `x, y` indica el centro.

```js
rectMode(CENTER);
rect(200, 200, 200, 80);
```

#### ellipseMode()

`ellipseMode()` cambia la manera en que p5.js interpreta las coordenadas de
`ellipse()`.

```js
ellipseMode(CENTER);
ellipse(200, 200, 120, 80);
```

Con `CENTER`, la posición `x, y` indica el centro de la elipse. Con `CORNER`, la
posición indica la esquina superior izquierda del rectángulo imaginario que
contiene la elipse.

#### triangle()

`triangle()` dibuja un triángulo a partir de tres puntos. Cada punto tiene una
coordenada `x` y una coordenada `y`.

```js
triangle(x1, y1, x2, y2, x3, y3);
```

Cada par de valores define una esquina del triángulo. Por ejemplo:

```js
triangle(100, 300, 200, 100, 300, 300);
```

Este triángulo puede servir como base para pensar la estructura de una letra
**A**, porque permite trabajar con dos diagonales y una forma triangular.

#### quad()

`quad()` dibuja un cuadrilátero a partir de cuatro puntos. También usa pares de
coordenadas `x, y`.

```js
quad(x1, y1, x2, y2, x3, y3, x4, y4);
```

Por ejemplo:

```js
quad(120, 300, 180, 100, 220, 100, 280, 300);
```

Esta forma permite construir figuras de cuatro lados que no necesariamente son
rectángulos. Puede usarse para generar astas, cuerpos inclinados o partes más
gruesas de un glifo.

### Formas personalizadas

Cuando una forma no calza con una primitiva como `triangle()` o `quad()`, se
puede construir punto por punto usando `beginShape()`, `vertex()` y
`endShape()`.

#### beginShape()

`beginShape()` indica el inicio de una forma personalizada. Después de llamarla,
p5.js empieza a registrar los puntos que compondrán esa figura.

```js
beginShape();
```

#### vertex()

`vertex()` agrega un punto a la forma. Cada vértice se define con una coordenada
`x` y una coordenada `y`.

```js
vertex(x, y);
```

El orden de los vértices importa, porque p5.js une los puntos siguiendo la
secuencia en que fueron escritos.

#### endShape()

`endShape()` marca el final de la forma. Si se usa solo, la figura termina en el
último vértice indicado.

```js
endShape();
```

#### CLOSE

`CLOSE` se usa dentro de `endShape()` para cerrar la figura, conectando el último
vértice con el primero.

```js
endShape(CLOSE);
```

Por ejemplo:

```js
beginShape();
vertex(100, 300);
vertex(180, 100);
vertex(220, 100);
vertex(300, 300);
vertex(240, 300);
vertex(200, 180);
vertex(160, 300);
endShape(CLOSE);
```

Este tipo de construcción permite dibujar glifos o letras como polígonos,
controlando manualmente cada punto de su estructura.

### Funciones en p5.js

Una **función** permite agrupar instrucciones bajo un nombre. Sirve para ordenar
el código, reutilizar una acción y separar partes del dibujo en bloques más
claros.

En p5.js ya usamos funciones especiales como `setup()` y `draw()`, pero también
podemos crear nuestras propias funciones.

```js
function dibujaCosa() {
  beginShape();
  vertex(100, 300);
  vertex(180, 100);
  vertex(220, 100);
  vertex(300, 300);
  vertex(240, 300);
  vertex(200, 180);
  vertex(160, 300);
  endShape(CLOSE);
}
```

Para que esa función se ejecute, hay que llamarla desde otra parte del programa,
por ejemplo dentro de `draw()`:

```js
function draw() {
  background(220);
  fill(0);
  noStroke();
  dibujaCosa();
}
```

En este caso, `dibujaCosa()` contiene la receta para dibujar una forma cerrada.
Cada vez que se llama a la función, p5.js ejecuta las instrucciones que están
dentro de sus llaves `{}`.

Esto también se puede entender como **encapsulación**: la función guarda una
serie de instrucciones dentro de un bloque con nombre. Desde afuera no es
necesario repetir todos los `vertex()` cada vez; basta con llamar a
`dibujaCosa()`. Así el código queda más ordenado y cada parte del dibujo puede
funcionar como una unidad.

#### Argumentos

Los **argumentos** son valores que se entregan a una función para que pueda
trabajar con información variable. Sirven para que una misma función no dibuje
siempre exactamente lo mismo.

```js
function dibujaCosa(x, y) {
  push();
  translate(x, y);
  beginShape();
  vertex(0, 100);
  vertex(80, -100);
  vertex(120, -100);
  vertex(200, 100);
  vertex(140, 100);
  vertex(100, -20);
  vertex(60, 100);
  endShape(CLOSE);
  pop();
}
```

En este ejemplo, `x` e `y` son argumentos. Funcionan como datos de entrada para
decidir dónde se dibuja la forma.

```js
function draw() {
  background(220);
  dibujaCosa(100, 300);
  dibujaCosa(250, 300);
}
```

La misma función se usa dos veces, pero con distintos valores. Así se pueden
repetir formas, cambiar posiciones y construir sistemas visuales sin copiar todo
el código.

### Variables

Una **variable** es un contenedor de valores. Permite guardar un dato bajo un
nombre para usarlo después en el código.

```js
let x = 100;
let y = 200;

ellipse(x, y, 50, 50);
```

En este ejemplo, `x` guarda el valor `100` e `y` guarda el valor `200`. Luego
esas variables se usan como coordenadas para dibujar una elipse.

#### Declaración de valores

Declarar una variable significa crear un nombre y asociarlo a un valor.

```js
// let indica que estamos creando una variable.
// x es el nombre de la variable.
// 100 es el valor que queda guardado dentro de x.
let x = 100;

// y guarda otro valor numérico.
let y = 200;

// tamano guarda el valor que usaremos como ancho y alto de la elipse.
let tamano = 50;

// Usamos los valores guardados en las variables.
ellipse(x, y, tamano, tamano);
```

El signo `=` no significa "igual" como en matemáticas, sino **asignación**: toma
el valor de la derecha y lo guarda en la variable de la izquierda.

Las variables pueden cambiar durante el programa:

```js
let x = 100;

function draw() {
  background(220);
  ellipse(x, 200, 50, 50);
  x = x + 1;
}
```

En este caso, el valor de `x` aumenta en cada frame, por eso la elipse se mueve.

#### Tipos de dato

Un **tipo de dato** o **datatype** indica qué clase de valor guarda una variable.
Algunos tipos comunes son:

- `number`: número, como `10`, `3.5` o `PI`
- `string`: texto, como `"hola"` o `"A"`
- `boolean`: valor lógico, `true` o `false`
- `object`: conjunto de datos organizados por propiedades

```js
let ancho = 80;
let letra = "A";
let encendido = true;
let puntos = [100, 200, 300];
```

En p5.js, elegir bien los nombres de las variables ayuda a entender qué controla
cada valor: posición, tamaño, color, velocidad, ángulo o estado.

#### Concatenación

La **concatenación** consiste en unir textos con otros textos o con valores
guardados en variables. En JavaScript se puede hacer usando el signo `+`.

```js
let letra = "A";
let ancho = 80;

text("La letra es " + letra, 20, 40);
text("El ancho es " + ancho, 20, 60);
```

En p5.js, `text()` permite dibujar texto en el canvas. Sus primeros argumentos
son el contenido que se quiere mostrar y la posición `x, y` donde aparecerá.

```js
text(contenido, x, y);
```

También se pueden concatenar varios valores:

```js
let x = 100;
let y = 200;

text("x: " + x + " / y: " + y, 20, 40);
```

Esto sirve para mostrar información del programa en pantalla, como posiciones,
valores de sliders, puntajes, estados o datos que cambian durante la ejecución.

#### nf()

`nf()` significa **number format**. Sirve para dar formato a un número antes de
mostrarlo, por ejemplo para controlar cuántos dígitos o decimales aparecen.

```js
nf(numero, digitosEnteros, digitosDecimales);
```

Por ejemplo:

```js
let valor = 3.14159;
let valorFormateado = nf(valor, 1, 2);

text("Valor: " + valorFormateado, 20, 40);
```

En este caso, `nf(valor, 1, 2)` muestra el número con **1 dígito entero** y
**2 decimales**. El resultado visible sería `3.14`.

También puede servir para ordenar números visualmente:

```js
let contador = 7;

text("Frame: " + nf(contador, 3, 0), 20, 60);
```

El resultado sería `Frame: 007`, porque se piden 3 dígitos enteros y 0
decimales.

#### constrain()

`constrain()` sirve para limitar un valor dentro de un rango mínimo y máximo.
Esto evita que un número crezca o baje más allá de los límites que nos interesan.

```js
constrain(valor, minimo, maximo);
```

Por ejemplo:

```js
let x = mouseX;
x = constrain(x, 50, 350);

ellipse(x, 200, 40, 40);
```

En este caso, aunque `mouseX` salga de ese rango, `x` queda limitado entre `50`
y `350`.

También se puede usar para proteger valores que cambian con el tiempo:

```js
let tamano = 10;

function draw() {
  background(220);

  tamano = tamano + 1;
  tamano = constrain(tamano, 10, 100);

  ellipse(200, 200, tamano, tamano);
}
```

Así, el tamaño de la elipse aumenta, pero nunca pasa de `100`.

### Transformaciones

Las transformaciones permiten cambiar la posición, rotación o tamaño de una
forma sin modificar uno por uno sus vértices.

#### translate()

`translate()` mueve el origen del sistema de coordenadas. Después de usarlo, las
formas se dibujan desplazadas según los valores indicados.

```js
translate(200, 200);
dibujaCosa();
```

#### rotate()

`rotate()` rota el sistema de coordenadas. En p5.js, por defecto, el ángulo se
escribe en radianes.

```js
rotate(PI / 4);
dibujaCosa();
```

#### scale()

`scale()` cambia el tamaño del dibujo. Un valor mayor que `1` agranda la forma y
un valor menor que `1` la reduce.

```js
scale(0.5);
dibujaCosa();
```

Para aplicar transformaciones a una sola forma, conviene usar `push()` y
`pop()`. `push()` guarda el estado actual del dibujo y `pop()` lo recupera.

#### push() y pop()

`push()` y `pop()` funcionan como una forma de aislar cambios visuales o
transformaciones. Todo lo que se escribe entre ambos queda contenido dentro de
ese bloque.

`push()` guarda el estado actual del dibujo: posición del sistema de
coordenadas, rotación, escala, relleno, contorno y otros estilos. Luego se pueden
hacer cambios sin afectar necesariamente al resto del programa.

`pop()` recupera el estado que había antes de llamar a `push()`. Por eso se usa
después de dibujar una forma transformada o con un estilo específico.

```js
push();
fill(255, 0, 0);
translate(200, 200);
dibujaCosa();
pop();

dibujaCosa();
```

En este ejemplo, solo la primera forma se dibuja roja y desplazada. La segunda
forma vuelve al estado anterior, porque `pop()` deshace los cambios realizados
dentro del bloque.

```js
function draw() {
  // Limpia el canvas en cada frame con un fondo gris claro.
  background(220);

  // Guarda el estado actual del sistema de coordenadas.
  push();

  // Mueve el origen del dibujo al punto x: 200, y: 200.
  translate(200, 200);

  // Rota el sistema de coordenadas 30 grados aproximadamente.
  rotate(PI / 6);

  // Reduce el tamaño de la forma al 80%.
  scale(0.8);

  // Dibuja la forma usando las transformaciones anteriores.
  dibujaCosa();

  // Recupera el estado original del sistema de coordenadas.
  pop();
}
```

Así, el movimiento, la rotación y la escala afectan solo a `dibujaCosa()` y no a
los demás elementos del canvas.

---

### [Sketch de referencia](https://editor.p5js.org/coyarzun/sketches/pImXXyAf4)

Este sketch es una base para generar el glifo de la letra **A** a partir de una
estructura geométrica. Usa guías tipográficas como línea base, línea de
capitulares, ascendente, descendente y altura x, y permite modificar esas
proporciones mediante sliders.

El dibujo se arma con puntos fijos y puntos variables: los puntos fijos definen
la estructura principal de la A, mientras que los puntos variables se calculan a
partir de la intersección con la altura x. Con esos puntos se dibuja el esqueleto
del glifo, mostrando cómo una letra puede construirse como sistema de relaciones
entre medidas, ejes e inclinación.
