# clase-08

Jueves 1 de octubre de 2026

Profesor: Christian Oyarzun Roa
Correo: coyarzun@error404.cl

## Apuntes de p5.js: sonido

### Sonido en un sketch

El sonido agrega una dimensión temporal y física a un sketch. Puede funcionar
como material de una composición, como respuesta a una interacción o como dato
que modifica la imagen. En p5.js, la biblioteca **p5.sound** amplía p5.js con
reproducción de archivos, síntesis, entrada de micrófono y análisis de audio.

Para usarla, el proyecto debe cargar p5.sound además de p5.js. En el Web Editor
se puede agregar desde **Sketch → Add Library**. En un proyecto HTML, el script
de p5.sound debe aparecer después del de p5.js:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.10/p5.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.10/addons/p5.sound.min.js"></script>
```

Los navegadores suelen bloquear el audio automático. Por eso es mejor iniciar
la reproducción a partir de una acción explícita, como un clic o una tecla.
Esto permite que quien visita el sketch decida cuándo comienza a sonar.

### Cargar y reproducir un archivo

`loadSound()` carga un archivo de audio y devuelve un objeto `p5.SoundFile`.
Conviene cargarlo en `preload()`, antes de que empiece `setup()`, para que esté
disponible cuando el sketch lo necesite. El archivo debe estar dentro del
proyecto; una carpeta llamada `assets` permite mantener ordenados los recursos.

```js
let sonido;

function preload() {
  sonido = loadSound("assets/ambiente.mp3");
}

function setup() {
  createCanvas(500, 300);
  textAlign(CENTER, CENTER);
}

function draw() {
  background(30);
  fill(255);
  text("Haz clic para reproducir", width / 2, height / 2);
}

function mousePressed() {
  if (!sonido.isPlaying()) {
    sonido.play();
  }
}
```

Formatos como MP3 y WAV suelen funcionar en navegadores actuales. Para mejorar
la compatibilidad entre navegadores, `loadSound()` también acepta una lista de
rutas alternativas:

```js
sonido = loadSound(["assets/ambiente.ogg", "assets/ambiente.mp3"]);
```

Algunos métodos útiles de `p5.SoundFile`:

- `play()` inicia la reproducción.
- `pause()` pausa y permite continuar desde el mismo punto.
- `stop()` detiene y vuelve al inicio.
- `loop()` reproduce en ciclo.
- `isPlaying()` indica si está sonando.
- `setVolume(0.5)` ajusta el volumen entre `0` y `1`.
- `rate(1.5)` cambia la velocidad y también la altura del sonido.

### Sonido reactivo

Un sistema **reactivo** recibe información y modifica su comportamiento como
respuesta. En un sketch audiovisual, el sonido puede controlar propiedades
visuales, como el tamaño, el color o la velocidad de una forma. `p5.Amplitude`
mide la amplitud —una estimación de la intensidad o nivel del sonido— y entrega
un valor que normalmente se mueve cerca de `0` a `1`.

Este ejemplo analiza el archivo que está reproduciendo el sketch y convierte su
nivel en el diámetro de un círculo:

```js
let sonido;
let amplitud;

function preload() {
  sonido = loadSound("assets/ambiente.mp3");
}

function setup() {
  createCanvas(500, 300);
  amplitud = new p5.Amplitude();
  amplitud.setInput(sonido);
}

function draw() {
  background(20, 25, 40);

  let nivel = amplitud.getLevel();
  let diametro = map(nivel, 0, 0.3, 30, 260, true);

  noStroke();
  fill(90, 210, 255);
  circle(width / 2, height / 2, diametro);
}

function mousePressed() {
  if (sonido.isPlaying()) {
    sonido.pause();
  } else {
    sonido.play();
  }
}
```

`map()` traduce el rango pequeño de amplitud a un rango visual más evidente.
El último argumento `true` limita el resultado al rango de salida. Sin ese
límite, los niveles más altos pueden producir tamaños fuera del rango indicado.
Los valores exactos dependen del archivo, su volumen y la mezcla del sistema.

También se puede analizar el espectro con `p5.FFT`. La transformada rápida de
Fourier separa el sonido en bandas de frecuencia. Esto permite relacionar, por
ejemplo, las frecuencias graves con formas grandes y las agudas con detalles
pequeños.

```js
let sonido;
let fft;

function preload() {
  sonido = loadSound("assets/ambiente.mp3");
}

function setup() {
  createCanvas(500, 300);
  fft = new p5.FFT();
  fft.setInput(sonido);
}

function draw() {
  background(15);
  let graves = fft.getEnergy("bass"); // valor entre 0 y 255
  let diametro = map(graves, 0, 255, 20, 280);

  noStroke();
  fill(255, 120, 70);
  circle(width / 2, height / 2, diametro);
}

function mousePressed() {
  if (!sonido.isPlaying()) sonido.loop();
  else sonido.pause();
}
```

La amplitud resume la intensidad total en un número; el FFT permite observar
cómo se distribuye la energía entre frecuencias. Para visualizar el espectro
completo se puede usar `fft.analyze()`, que devuelve un arreglo de valores.

### Entrada de micrófono

`p5.AudioIn` permite usar el micrófono como fuente de datos. El navegador pedirá
permiso a la persona usuaria y el acceso depende de sus ajustes de privacidad.
Para iniciar el micrófono, se recomienda hacerlo tras un clic:

```js
let microfono;
let amplitud;

function setup() {
  createCanvas(500, 300);
  microfono = new p5.AudioIn();
  amplitud = new p5.Amplitude();
  amplitud.setInput(microfono);
  textAlign(CENTER, CENTER);
}

function draw() {
  background(25);
  let nivel = amplitud.getLevel();
  let diametro = map(nivel, 0, 0.25, 20, 280, true);
  circle(width / 2, height / 2, diametro);
  text("Haz clic y permite el acceso al micrófono", width / 2, height - 25);
}

function mousePressed() {
  microfono.start();
}
```

El nivel del micrófono también es información sensible: hay que explicar cuándo
se activa y diseñar la experiencia con cuidado. No es necesario grabar ni guardar
audio para reaccionar visualmente al nivel de entrada.

### Controles HTML: sliders e inputs de texto

Además del canvas, p5.js permite crear elementos HTML para que la persona
interactúe con el sketch. Un **slider** (`createSlider()`) sirve para elegir un
número dentro de un rango. Un **input de texto** (`createInput()`) permite
escribir una palabra o frase. Estos controles se pueden leer en `draw()` o
cuando ocurre un evento, y sus valores pueden modificar tanto la imagen como el
sonido.

#### Slider

`createSlider(mínimo, máximo, valorInicial, paso)` crea un control deslizante.
Por ejemplo, este slider controla el tamaño de un círculo:

```js
let sliderTamanio;

function setup() {
  createCanvas(500, 300);
  sliderTamanio = createSlider(20, 250, 100, 1);
  sliderTamanio.position(20, 320);
}

function draw() {
  background(240);
  let tamanio = sliderTamanio.value();
  circle(width / 2, height / 2, tamanio);
}
```

Los argumentos del ejemplo significan: mínimo `20`, máximo `250`, valor inicial
`100` y paso de `1`. El método `.value()` obtiene el número seleccionado. Como
`draw()` se ejecuta repetidamente, el sketch refleja el cambio mientras se mueve
el slider.

Para modificar el volumen de un archivo de audio, se puede usar un slider con
valores entre `0` y `1`:

```js
let sonido;
let sliderVolumen;

function preload() {
  sonido = loadSound("assets/ambiente.mp3");
}

function setup() {
  createCanvas(500, 250);
  sliderVolumen = createSlider(0, 1, 0.5, 0.01);
  sliderVolumen.position(20, 270);
}

function draw() {
  background(30);
  sonido.setVolume(sliderVolumen.value());
  fill(255);
  text(`Volumen: ${sliderVolumen.value()}`, 20, 40);
  text("Haz clic para reproducir", 20, 70);
}

function mousePressed() {
  if (!sonido.isPlaying()) sonido.loop();
}
```

#### Input de texto

`createInput()` crea un campo de texto. `.value()` entrega lo que la persona
escribió; ese valor puede mostrarse en el canvas o usarse para cambiar una
propiedad visual:

```js
let campoTexto;

function setup() {
  createCanvas(500, 300);
  campoTexto = createInput("Escribe algo");
  campoTexto.position(20, 320);
  textAlign(CENTER, CENTER);
}

function draw() {
  background(35, 45, 65);
  fill(255);
  textSize(32);
  text(campoTexto.value(), width / 2, height / 2);
}
```

El campo HTML y el canvas son elementos separados: `position()` ubica el input
en la página y no dentro del sistema de coordenadas del canvas. Si se cambia el
tamaño del canvas, puede ser necesario ajustar también la posición del control.

#### Responder al cambio o al envío

Para reaccionar solo cuando el valor cambia, se puede usar `.input()` con una
función. Para un formulario sencillo, `.changed()` se activa cuando se confirma
el cambio, por ejemplo al presionar Enter o salir del campo:

```js
let campoTexto;
let mensaje = "Escribe y presiona Enter";

function setup() {
  createCanvas(500, 250);
  campoTexto = createInput("");
  campoTexto.position(20, 270);
  campoTexto.changed(actualizarMensaje);
}

function actualizarMensaje() {
  mensaje = campoTexto.value();
}

function draw() {
  background(235);
  text(mensaje, 20, 60);
}
```

Se puede limitar el campo a un tipo de dato, por ejemplo números, usando el
atributo HTML `type`:

```js
let campoNumero;

function setup() {
  createCanvas(400, 250);
  campoNumero = createInput("100", "number");
  campoNumero.position(20, 270);
}

function draw() {
  background(230);
  let valor = Number(campoNumero.value());
  circle(width / 2, height / 2, constrain(valor, 10, 300));
}
```

`value()` devuelve texto, incluso si el campo parece numérico. `Number()` lo
convierte a número; `constrain()` mantiene el resultado entre límites válidos
para el diámetro.

#### Ubicación y presentación

Los elementos de interfaz creados con `createSlider()` y `createInput()` son
elementos HTML del DOM. Algunas funciones útiles para ordenarlos y darles estilo
son:

- `.position(x, y)` establece su posición en la página.
- `.size(ancho, alto)` ajusta sus dimensiones.
- `.style("propiedad", "valor")` aplica un estilo CSS.
- `.value()` lee o establece su valor.
- `.input(funcion)` ejecuta una función mientras cambia el valor.
- `.changed(funcion)` ejecuta una función al confirmar el cambio.

Ejemplo de estilo:

```js
let slider;

function setup() {
  createCanvas(400, 250);
  slider = createSlider(0, 100, 50);
  slider.position(20, 270);
  slider.style("width", "300px");
}
```

Una interfaz clara indica qué controla cada elemento, muestra el valor cuando
sea útil y ofrece rangos apropiados. Por ejemplo, un slider de volumen se
entiende mejor con una etiqueta “Volumen” y un rango entre `0` y `1` que con
números sin explicación.

### Tipografía como geometría: `textToPoints()` y funciones relacionadas

Normalmente `text()` dibuja letras como texto. Con una fuente cargada mediante
`loadFont()`, los métodos de `p5.Font` permiten acceder a los contornos de las
letras y usarlos como geometría: puntos para dibujar, contornos para construir
formas o comandos de ruta para trabajar con curvas.

La fuente debe ser un archivo compatible, por ejemplo `.ttf` u `.otf`, incluido
en el proyecto. `loadFont()` se ejecuta en `preload()` para que esté lista antes
de dibujar:

```js
let fuente;

function preload() {
  fuente = loadFont("assets/mi-fuente.otf");
}

function setup() {
  createCanvas(600, 300);
  noLoop();
}

function draw() {
  background(245);
  let puntos = fuente.textToPoints("HOLA", 50, 200, {
    sampleFactor: 0.15
  });

  stroke(20, 80, 180);
  strokeWeight(4);
  for (let punto of puntos) {
    point(punto.x, punto.y);
  }
}
```

`textToPoints(texto, x, y, opciones)` devuelve un arreglo de puntos que
muestrean el borde de las letras. Cada punto contiene `x`, `y` y `alpha` (ángulo
de la trayectoria). `sampleFactor` controla la densidad: un valor mayor crea más
puntos y más detalle, pero también requiere más trabajo de dibujo. Por defecto,
`x, y` ubican la caja del texto y `y` corresponde a su parte inferior.

Los puntos pueden convertirse en elementos gráficos animados:

```js
let fuente;
let puntos = [];

function preload() {
  fuente = loadFont("assets/mi-fuente.otf");
}

function setup() {
  createCanvas(600, 300);
  puntos = fuente.textToPoints("P5", 80, 210, { sampleFactor: 0.2 });
}

function draw() {
  background(15);
  noStroke();
  fill(255, 120, 60);
  for (let p of puntos) {
    let pulso = 3 + 2 * sin(frameCount * 0.05 + p.x * 0.04);
    circle(p.x, p.y, pulso);
  }
}
```

#### `textToContours()`

`textToContours()` devuelve un arreglo de contornos, uno por cada borde cerrado
que forma el texto. Una letra con un hueco, como la “O”, tiene un contorno
exterior y otro interior. Esta estructura sirve para deformar bordes o recorrer
cada contorno por separado.

```js
let fuente;

function preload() {
  fuente = loadFont("assets/mi-fuente.otf");
}

function setup() {
  createCanvas(600, 300);
}

function draw() {
  background(245);
  let contornos = fuente.textToContours("O", 180, 220, {
    sampleFactor: 0.15
  });

  noFill();
  stroke(20, 100, 180);
  strokeWeight(2);
  for (let contorno of contornos) {
    beginShape();
    for (let p of contorno) {
      let desplazamiento = 4 * sin(p.y * 0.04 + frameCount * 0.05);
      vertex(p.x + desplazamiento, p.y);
    }
    endShape(CLOSE);
  }
}
```

Cada contorno es una secuencia de vértices. `beginShape()` y
`endShape(CLOSE)` trazan esa secuencia y cierran su borde. En letras con huecos,
el relleno requiere preservar correctamente la relación entre el borde exterior
y los interiores; para observar y deformar las líneas, `noFill()` evita ese
problema.

#### `textToPaths()` y métodos asociados

`textToPaths()` devuelve comandos de ruta vectorial, como mover el punto, trazar
una línea o describir una curva Bézier. Sirve cuando se necesitan las curvas
originales y no una aproximación mediante puntos. `textToModel()` transforma el
texto en geometría 3D para dibujar en un canvas `WEBGL`.

Otras funciones útiles para texto convencional son `textWidth()` para medir el
ancho, `textAscent()` y `textDescent()` para consultar métricas verticales, y
`textBounds()` para obtener una caja ajustada. Estas funciones calculan medidas;
no devuelven los puntos del contorno.

| Función | Resultado | Uso frecuente |
| --- | --- | --- |
| `text()` | Dibuja texto | Mostrar títulos o instrucciones |
| `textWidth()` / `textBounds()` | Medidas del texto | Alinear y ubicar texto |
| `textToPoints()` | Un arreglo de puntos | Partículas y dibujo punto a punto |
| `textToContours()` | Arreglos de puntos agrupados por contorno | Recorrer y deformar bordes |
| `textToPaths()` | Comandos de ruta vectorial | Procesar curvas y trazos |
| `textToModel()` | Geometría 3D | Tipografía en `WEBGL` |

`textToPoints()`, `textToContours()` y `textToPaths()` son métodos del objeto
fuente (`fuente` en los ejemplos), no funciones globales. Si la fuente no carga,
revisa la ruta, el nombre del archivo y que esté incluido en el proyecto.

### Ideas para explorar

- ¿Qué cambia si el sonido controla la posición en vez del tamaño?
- ¿Cómo se transforma la imagen si el sonido se reproduce en ciclo?
- ¿Qué diferencias aparecen entre reaccionar a la amplitud y a una banda de
  frecuencias?
- ¿Cómo podría una persona controlar el ritmo, el volumen o el momento de inicio?
- ¿Qué relaciones visuales hacen que la respuesta se sienta conectada al sonido?
- ¿Qué cambia en una composición cuando sus parámetros se pueden controlar con
  sliders o escribir mediante un input?
- ¿Cómo se transforma una palabra al convertir su contorno en puntos y animar
  esos puntos?

## Referencias

- p5.js, [p5.sound](https://p5js.org/reference/p5.sound/).
- p5.js, [loadSound()](https://p5js.org/reference/p5/loadSound/).
- p5.js, [p5.SoundFile](https://p5js.org/reference/p5.sound/p5.SoundFile/).
- p5.js, [p5.Amplitude](https://p5js.org/reference/p5.sound/p5.Amplitude/).
- p5.js, [p5.FFT](https://p5js.org/reference/p5.sound/p5.FFT/).
- p5.js, [p5.AudioIn](https://p5js.org/reference/p5.sound/p5.AudioIn/).
- p5.js, [createSlider()](https://p5js.org/reference/p5/createSlider/).
- p5.js, [createInput()](https://p5js.org/reference/p5/createInput/).
- p5.js, [Element](https://p5js.org/reference/p5.Element/).
- p5.js, [loadFont()](https://p5js.org/reference/p5/loadFont/).
- p5.js, [p5.Font](https://p5js.org/reference/p5/p5.Font/).
- p5.js, [textToPoints()](https://p5js.org/reference/p5.Font/textToPoints/).
- p5.js, [textToContours()](https://p5js.org/reference/p5.Font/textToContours/).
- p5.js, [textToPaths()](https://p5js.org/reference/p5.Font/textToPaths/).
- p5.js, [textToModel()](https://p5js.org/reference/p5.Font/textToModel/).
- p5.js, [textBounds()](https://p5js.org/reference/p5/textBounds/).
