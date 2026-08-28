# clase-04

Jueves 27 de agosto de 2026

Profesor: Christian Oyarzun Roa
Correo: coyarzun@error404.cl

## Apuntes de p5.js

### for

`for` es una estructura de repetición. Sirve para ejecutar una instrucción
varias veces sin tener que escribirla manualmente una y otra vez.

Aunque a veces se anota como `for();`, técnicamente no es una función de p5.js,
sino una herramienta de JavaScript. En p5.js se usa mucho para dibujar grillas,
patrones, series, repeticiones y variaciones.

La estructura básica de un `for` tiene tres partes:

```js
for (contador inicial; condicion; incremento) {
  // instrucciones que se repiten
}
```

- **contador inicial**: define desde dónde parte el conteo.
- **condición**: indica hasta cuándo se repite.
- **incremento**: cambia el valor en cada repetición.

Por ejemplo:

```js
for (let i = 0; i < 10; i++) {
  print(i);
}
```

En este caso, la variable `i` parte en `0`, aumenta de uno en uno y el ciclo se
repite mientras `i` sea menor que `10`.

### Contador

En un ciclo `for`, el contador es la variable que cambia en cada repetición.
Normalmente se usan nombres cortos como `i`, `j` o `k`.

```js
for (let i = 0; i < 10; i++) {
  print(i);
}
```

En este ejemplo, `i` es el contador. Parte en `0`, luego pasa a `1`, después a
`2`, y así sucesivamente hasta que la condición deja de cumplirse.

Cuando hay ciclos dentro de otros ciclos, se suelen usar distintos nombres para
no confundirlos:

- `i`: primer contador.
- `j`: segundo contador.
- `k`: tercer contador.

Estos nombres no son obligatorios, pero son una convención común en
programación. También podrían llamarse `fila`, `columna`, `paso` o cualquier
otro nombre que ayude a entender mejor el código.

### Incremento

El incremento es la parte del ciclo que cambia el valor del contador después de
cada repetición.

```js
for (let i = 0; i < 10; i++) {
  print(i);
}
```

En este caso, `i++` significa que `i` aumenta en `1` después de cada vuelta del
ciclo.

Algunas formas comunes de actualizar un contador son:

- `i++`: suma `1`.
- `i--`: resta `1`.
- `i += 2`: suma `2`.
- `i -= 2`: resta `2`.
- `i += 10`: suma `10`.

Por ejemplo, si se quiere contar de dos en dos:

```js
for (let i = 0; i < 10; i += 2) {
  print(i);
}
```

El resultado sería `0`, `2`, `4`, `6`, `8`.

También se puede contar hacia atrás usando `i--`:

```js
for (let i = 10; i > 0; i--) {
  print(i);
}
```

En este caso, el contador parte en `10` y va disminuyendo hasta que la condición
`i > 0` deja de cumplirse.

`i---` no se usa como incremento o decremento. Para restar uno se escribe
`i--`.

### if

`if` es una estructura condicional. Sirve para ejecutar una instrucción solo si
se cumple una condición.

```js
if (condicion) {
  // instrucciones que se ejecutan si la condicion es verdadera
}
```

La condición va entre paréntesis. Si esa condición es verdadera, se ejecuta el
código que está dentro de las llaves.

Por ejemplo:

```js
if (mouseX > 300) {
  print("el mouse esta a la derecha");
}
```

En este caso, el mensaje aparece solo si la posición del mouse en `x` es mayor
que `300`.

### Operadores de comparación

Para escribir condiciones se usan operadores de comparación:

- `>`: mayor que.
- `<`: menor que.
- `>=`: mayor o igual que.
- `<=`: menor o igual que.
- `==`: igual a.
- `!=`: distinto de.

Por ejemplo:

```js
if (i == 5) {
  print("i vale 5");
}
```

Este `if` pregunta si el valor de `i` es igual a `5`.

### else if

`else if` permite agregar una segunda condición cuando la primera condición no
se cumple.

```js
if (condicion1) {
  // instrucciones si condicion1 es verdadera
} else if (condicion2) {
  // instrucciones si condicion2 es verdadera
}
```

El programa revisa primero el `if`. Si esa condición es falsa, recién revisa el
`else if`.

Por ejemplo:

```js
if (mouseX < 200) {
  print("izquierda");
} else if (mouseX < 400) {
  print("centro");
}
```

En este caso, si el mouse está antes de `200`, aparece `"izquierda"`. Si no está
antes de `200`, pero sí antes de `400`, aparece `"centro"`.

### else

`else` sirve para definir qué ocurre cuando ninguna de las condiciones
anteriores se cumple.

```js
if (condicion1) {
  // instrucciones si condicion1 es verdadera
} else if (condicion2) {
  // instrucciones si condicion2 es verdadera
} else {
  // instrucciones si ninguna condicion anterior se cumple
}
```

Por ejemplo:

```js
if (mouseX < 200) {
  print("izquierda");
} else if (mouseX < 400) {
  print("centro");
} else {
  print("derecha");
}
```

En este caso, el código clasifica la posición del mouse en tres zonas:
izquierda, centro o derecha.

### Operadores booleanos

Los operadores booleanos permiten combinar o modificar condiciones. Son útiles
cuando una decisión depende de más de una pregunta.

En JavaScript y p5.js se escriben así:

- **AND**: `&&`
- **OR**: `||`
- **NOT**: `!`

### AND

`AND` se escribe como `&&`. Sirve para preguntar si dos condiciones se cumplen
al mismo tiempo.

```js
if (mouseX > 100 && mouseX < 400) {
  print("el mouse esta dentro de la zona");
}
```

En este caso, el mensaje aparece solo si `mouseX` es mayor que `100` y menor que
`400`.

### OR

`OR` se escribe como `||`. Sirve para preguntar si al menos una de las
condiciones se cumple.

```js
if (mouseX < 100 || mouseX > 500) {
  print("el mouse esta en un extremo");
}
```

En este caso, el mensaje aparece si el mouse está muy a la izquierda o muy a la
derecha.

### NOT

`NOT` se escribe como `!`. Sirve para negar una condición, es decir, para
invertir su valor.

```js
let estaPresionado = mouseIsPressed;

if (!estaPresionado) {
  print("el mouse no esta presionado");
}
```

Si `estaPresionado` es `false`, entonces `!estaPresionado` se vuelve `true`.

### map()

`map()` es una función de p5.js que sirve para convertir un número desde un
rango a otro rango.

Su estructura es:

```js
map(valor, inicio1, fin1, inicio2, fin2);
```

- `valor`: número que se quiere transformar.
- `inicio1` y `fin1`: rango original.
- `inicio2` y `fin2`: nuevo rango.

Por ejemplo:

```js
let tamano = map(mouseX, 0, width, 10, 100);
```

En este caso, la posición del mouse en `x` se transforma en un tamaño. Cuando
`mouseX` está cerca de `0`, `tamano` se acerca a `10`. Cuando `mouseX` está
cerca de `width`, `tamano` se acerca a `100`.

También se puede usar para controlar color, posición, rotación, transparencia o
cualquier variable numérica.

```js
let gris = map(mouseY, 0, height, 0, 255);
background(gris);
```

En este ejemplo, la posición vertical del mouse se convierte en un valor de gris
entre `0` y `255`.

### sin()

`sin()` calcula el seno de un ángulo. En p5.js se usa mucho para crear
movimientos ondulatorios, oscilaciones y variaciones suaves.

Por defecto, el ángulo se escribe en radianes.

```js
let y = sin(frameCount * 0.05);
```

El resultado de `sin()` oscila entre `-1` y `1`. Por eso suele combinarse con
multiplicaciones para hacerlo más visible:

```js
let y = sin(frameCount * 0.05) * 100;
```

### cos()

`cos()` calcula el coseno de un ángulo. Funciona de manera parecida a `sin()`,
pero parte desde otro punto de la onda.

```js
let x = cos(frameCount * 0.05) * 100;
```

Cuando `sin()` y `cos()` se usan juntos, sirven para ubicar puntos alrededor de
un círculo:

```js
let angulo = frameCount * 0.05;
let x = cos(angulo) * 100;
let y = sin(angulo) * 100;
```

En este caso, `x` e `y` forman una posición circular.

### abs()

`abs()` entrega el valor absoluto de un número. Esto significa que transforma un
número negativo en positivo.

```js
abs(-10); // devuelve 10
abs(10);  // devuelve 10
```

En p5.js puede servir para trabajar con distancias, diferencias o valores que no
deberían ser negativos.

```js
let distancia = abs(mouseX - width / 2);
```

En este ejemplo, `distancia` mide qué tan lejos está el mouse del centro del
canvas en el eje `x`, sin importar si está a la izquierda o a la derecha.

### Ideas importantes

- `for` sirve para repetir instrucciones.
- Evita escribir muchas veces el mismo código.
- Permite construir patrones, grillas y sistemas visuales.
- La variable del ciclo puede usarse como coordenada, tamaño, color o cantidad.
- Es una herramienta clave para pensar obras generativas.
- Los contadores como `i`, `j` o `k` permiten saber en qué repetición va el
  ciclo.
- El incremento controla cómo cambia el contador en cada repetición.
- `if` permite tomar decisiones dentro del código según una condición.
- `else if` permite revisar otra condición si la primera no se cumple.
- `else` define qué pasa cuando ninguna condición anterior se cumple.
- Los operadores booleanos permiten combinar condiciones.
- `&&` significa AND, `||` significa OR y `!` significa NOT.
- `map()` permite transformar un valor de un rango a otro.
- `sin()` y `cos()` permiten crear ondas, oscilaciones y posiciones circulares.
- `abs()` convierte un número en su valor positivo.

## Referente: Victor Vasarely

Victor Vasarely (Pécs, Hungría, 1906 - París, Francia, 1997) fue un artista
húngaro-francés asociado al **Op Art** o arte óptico. Su obra trabaja con
geometría, color, repetición, patrones e ilusiones visuales.

Aunque Vasarely no pertenece directamente al arte computacional, es un referente
importante para pensar imágenes construidas desde sistemas visuales. Muchas de
sus obras parecen funcionar como si tuvieran una lógica programada: módulos que
se repiten, grillas que se deforman, colores que cambian gradualmente y formas
que producen sensación de movimiento o volumen.

### Op Art

El **Op Art** busca activar la percepción del espectador. No representa objetos
del mundo real, sino que usa líneas, formas y colores para producir efectos
ópticos: vibración, profundidad, movimiento aparente o distorsión espacial.

En Vasarely, una grilla plana puede parecer una esfera, una superficie curva o
un espacio que se hunde y se expande. Esto ocurre porque modifica tamaños,
posiciones, contrastes y relaciones de color dentro de una estructura ordenada.

### Relación con arte generativo

Vasarely es útil como referente para p5.js y el arte generativo porque sus obras
pueden analizarse como sistemas:

- uso de grillas y módulos;
- repetición de formas geométricas;
- variaciones progresivas de tamaño, color o posición;
- ilusión de movimiento sin animación real;
- transformación de una estructura regular en una imagen dinámica.

### Obras de referencia

[![Victor Vasarely, Vega-Nor, 1969](https://buffaloakg.org/sites/default/files/styles/callout_fixed_height/public/artwork/K1971_022_006_o2.jpg?itok=0zCOnvYZ)](https://buffaloakg.org/artworks/k196929-vega-nor)

`Vega-Nor`, 1969. Obra donde una grilla geométrica produce la ilusión de una
forma volumétrica que sobresale o se curva hacia el espectador.

[![Victor Vasarely, Permutations, 1968](https://media.artmuseum.princeton.edu/iiif/3/collection/INV26552/full/%211024%2C1024/0/default.jpg)](https://artmuseum.princeton.edu/art/collections/objects/11032)

`Permutations`, 1968. Serie de serigrafías donde se exploran combinaciones
geométricas, variación modular y repetición sistemática.

[![Victor Vasarely, Vega WA-2, 1968](https://www.phillipscollection.org/sites/default/files/styles/feature_extra_large_no_crop_1200_/public/2026-01/2025.002.0009w.jpg?itok=VMKTWRPY)](https://www.phillipscollection.org/collection/vega-wa-2)

`Vega WA-2`, 1968. Obra de la serie `Vega`, basada en deformaciones de grilla
que producen ilusión de volumen.

[![Victor Vasarely, Planetary Folklore Participations No. 1, c. 1969](https://emuseum.mfah.org/internal/media/dispatcher/66264/preview)](https://emuseum.mfah.org/objects/78537/planetary-folklore-participations-no-1)

`Planetary Folklore Participations No. 1`, c. 1969. Sistema de unidades
geométricas y colores combinables, cercano a la idea de un alfabeto visual.

## Apuntes sobre Vera Molnár

Vera Molnár (Budapest, 1924 - 2023) fue una artista húngaro-francesa y una de
las pioneras del arte computacional, algorítmico y generativo. Su obra trabaja
principalmente con formas geométricas simples, como líneas, cuadrados,
rectángulos y grillas.

Antes de tener acceso a computadores reales, Molnár ya pensaba sus dibujos como
si fueran programas. A este método lo llamó **machine imaginaire**: una
"máquina imaginaria" donde la artista definía reglas, pasos y variaciones para
producir una imagen.

En 1968 comenzó a usar computadores en un laboratorio de la Sorbona, en París.
Aprendió a programar en FORTRAN y produjo dibujos mediante plotter, una máquina
que mueve un lápiz sobre el papel siguiendo instrucciones generadas por el
computador.

### Ideas importantes en su trabajo

- La imagen se construye desde una **regla** o sistema.
- El computador no reemplaza a la artista: funciona como una herramienta para
  explorar muchas variaciones posibles.
- La obra aparece entre el **orden** y el **desorden**.
- El azar no es completamente libre, sino que está controlado por límites
  definidos por la artista.
- Una figura simple puede cambiar mucho si se transforma paso a paso.

### Transformations

`Transformations` es una obra de Vera Molnár de 1976. Está compuesta por 23
dibujos hechos con plotter sobre papel continuo Benson Créteil.

La obra muestra una serie de cuadrados concéntricos organizados en una grilla.
A medida que avanza la serie, esa estructura regular empieza a deformarse y se
vuelve progresivamente más caótica.

Lo interesante no es solo la imagen final, sino el proceso de cambio:

- primero aparece una forma ordenada;
- luego se introducen pequeñas alteraciones;
- esas alteraciones se acumulan;
- finalmente, la grilla inicial se transforma en una composición más inestable.

Esta obra permite entender el arte generativo como una práctica basada en
instrucciones. La artista define un sistema visual y luego observa qué ocurre
cuando ese sistema se modifica.

### Imágenes de referencia

Las imágenes están enlazadas a sus fichas o páginas de origen.

[![Vera Molnár, Transformations, 1976](https://thomafoundation.org/wp-content/uploads/2020/04/Molnar-Transformations-Recto-1-Vera-Molnar-lo-res-2015.02.13.jpg)](https://thomafoundation.org/artwork/transformations/)

`Transformations`, 1976. Serie de dibujos de plotter con cuadrados concéntricos
que se deforman progresivamente.

[![Vera Molnár, Hypertransformations, 1975-1976](https://dam.org/museum/wp-content/uploads/2020/10/Molnar1974Hypertransformations2-481x500.png)](https://dam.org/museum/artists_ui/artists/molnar-vera/hypertransformations/)

`Hypertransformations`, 1975-1976. Variaciones sobre cuadrados regulares a
partir de pequeños cambios en los ejes `x` e `y`.

[![Vera Molnár, (Des)Ordres, 1974](https://dam.org/museum/wp-content/uploads/2020/09/Molnar1974DesOrdres1-copy-2000x1981.jpg)](https://dam.org/museum/artists_ui/artists/molnar-vera/des-ordres/)

`(Des)Ordres`, 1974. Grilla de cuadrados concéntricos donde el orden se altera
mediante distorsiones aleatorias.

Más obras para revisar:

- [`Interruptions`, 1969, National Gallery of Art](https://www.nga.gov/artworks/216160-interruptions)
- [`Molndrian`, 1974, MoMA](https://www.moma.org/collection/works/417832)
- [Página de Vera Molnár en DAM Museum](https://dam.org/museum/artists_ui/artists/molnar-vera/)

### Relación con p5.js

En p5.js se puede pensar una obra como `Transformations` usando:

- `for`, para repetir figuras;
- `rect()`, para dibujar cuadrados;
- `translate()` o coordenadas, para ubicarlos en una grilla;
- `random()` o `noise()`, para introducir variaciones;
- variables, para controlar cuánto se deforma cada figura.

Un esquema posible sería dibujar varios cuadrados concéntricos y modificar su
posición, tamaño o rotación según el paso de la serie. La lógica no está solo en
dibujar una figura, sino en definir un sistema que pueda variar.

## Apuntes sobre Edward Zajec

Edward Zajec, también mencionado como Edvard Zajec, nació en Trieste en 1938.
Es un artista pionero del arte computacional, especialmente por sus dibujos de
plotter y sus investigaciones sobre sistemas visuales, variación, estructura e
interactividad.

En 1968 comenzó a trabajar con computadores en Carleton College, en Minnesota.
Usó un computador IBM 1620 y programó en FORTRAN IV. En ese contexto desarrolló
sus primeras obras algorítmicas, entre ellas la serie `RAM`.

### RAM Series

La serie `RAM` fue realizada entre 1968 y 1969. Consiste en dibujos generados
por computador y trazados con plotter. Las composiciones usan una grilla
rectangular donde aparecen elementos lineales, módulos geométricos y formas que
recuerdan cubos o estructuras espaciales.

El nombre `RAM` se relaciona con el uso de procedimientos aleatorios y memoria
computacional. En estas obras, Zajec distribuye elementos sobre una retícula a
partir de probabilidades variables. El resultado combina repetición, ritmo,
orden y azar.

En vez de dibujar una composición única de manera manual, Zajec define un
sistema de reglas. El computador permite probar muchas combinaciones posibles
de un mismo vocabulario visual.

### Ideas importantes en RAM

- La imagen se organiza desde una **retícula**.
- Los elementos visuales se distribuyen mediante **probabilidad**.
- La repetición genera ritmo, pero el azar introduce variaciones.
- Las líneas y módulos producen sensación de profundidad y espacio.
- La obra funciona como una exploración de combinaciones posibles, no solo como
  una imagen final.

### Imágenes de referencia

Las imágenes están enlazadas a la exhibición `Plotter Drawings from 1960s` de
DAM Museum.

[![Edward Zajec, ram2/6, 1969](https://www.dam.org/mix/zajec-ram-2-6--dam-11452-0mJAi-de-2.jpg)](https://dam.org/dox/2658.kL95E.H.1.De.php)

`ram2/6`, 1969. Dibujo de plotter con módulos cúbicos, tramas de líneas y
variaciones dentro de una estructura regular.

[![Edward Zajec, ram10/4, 1969](https://www.dam.org/mix/zajec-ram-10-4--dam-11455-L0mRX-de-2.jpg)](https://dam.org/dox/2658.kL95E.H.1.De.php)

`ram10/4`, 1969. Composición basada en líneas, bloques geométricos y ritmos
espaciales.

[![Edward Zajec, Prostor2, 1969](https://www.dam.org/mix/zajec-prostor-prostor2--dam-11848-JKTpt-de-2.jpg)](https://dam.org/dox/2658.kL95E.H.1.De.php)

`Prostor2`, 1969. Obra relacionada con la investigación espacial de Zajec, donde
la línea construye volúmenes dentro de un plano.

### Relación con p5.js

La serie `RAM` se puede pensar en p5.js a través de:

- grillas;
- módulos repetidos;
- líneas paralelas;
- formas cúbicas o isométricas;
- azar controlado;
- probabilidades para decidir qué se dibuja y dónde aparece.

Esto conecta con la idea de programar una imagen como un conjunto de reglas:
primero se define una estructura base y luego se deja que ciertas decisiones
varíen dentro de límites.

## Apuntes sobre Mark Wilson

Mark Wilson (Cottage Grove, Oregon, 1943) es un artista, autor y programador
estadounidense asociado al arte computacional desde comienzos de los años 80.
Antes de trabajar con computadores, desarrollaba pinturas y dibujos abstractos
basados en geometría, repetición e imágenes de apariencia tecnológica.

En 1980 compró un microcomputador Texas Instruments 99/4a y comenzó a aprender
programación para producir obras visuales. Poco después empezó a trabajar con
computadores personales, plotters y software propio. Su práctica es importante
porque conecta la tradición de la pintura abstracta con los procedimientos de
la programación.

### Dibujo, programa y pixel mapping

Wilson entendía la pintura y el dibujo como procesos que podían tener reglas,
pasos y decisiones internas. Al empezar a programar, encontró una relación entre
la creación artística y el pensamiento algorítmico.

Una de sus técnicas centrales fue el **pixel mapping**. Primero generaba una
imagen simple en la pantalla del computador. Luego esa imagen se traducía a una
superficie física, dibujando o imprimiendo pixel por pixel. Los pixeles podían
convertirse en círculos, cuadrados, cruces, líneas u otras marcas.

Además, esos pixeles podían mapearse sobre distintas superficies geométricas:
planos, cilindros, conos o estructuras en perspectiva. Esto permitía transformar
una imagen digital de baja resolución en una composición compleja, densa y con
una apariencia más cercana al dibujo o la pintura.

### Drawing with Computers

En 1985 publicó `Drawing with Computers: The Artist's Guide to Computer
Graphics`, un libro pensado para artistas que querían aprender a usar el
computador como herramienta visual. El libro explicaba conceptos de programación
y mostraba cómo producir imágenes con computadores personales y plotters.

Este libro es importante porque muestra un momento en que el computador empieza
a salir del laboratorio y entra en el taller del artista. A diferencia de los
pioneros de los años 60, Wilson trabaja en el contexto de la computación
personal.

### Ideas importantes en su trabajo

- El computador permite generar muchas versiones de una imagen.
- El artista no solo usa software: también puede escribir sus propias
  herramientas.
- El pixel no se oculta como error técnico, sino que se vuelve material visual.
- La imagen digital puede traducirse a papel, tela u otros soportes físicos.
- La programación puede entenderse como un procedimiento artístico, similar a
  una receta o conjunto de instrucciones.

### Obras de referencia

Las imágenes están enlazadas a la página de Mark Wilson en DAM Museum.

[![Mark Wilson, 30C91, 1991](https://dam.org/museum/wp-content/uploads/2020/11/Wilson1991_30C91-scaled.jpeg)](https://dam.org/museum/artists_ui/artists/wilson-mark/)

`30C91`, 1991. Obra computacional donde una estructura de líneas y tramas se
curva como si estuviera proyectada sobre una superficie tridimensional.

[![Mark Wilson, Douat Dump A20, 1982](https://dam.org/museum/wp-content/uploads/2026/04/Wilson1982DouatDumpA20-scaled.jpeg)](https://dam.org/museum/artists_ui/artists/wilson-mark/)

`Douat Dump A20`, 1982. Dibujo temprano de plotter hecho con computador
personal, basado en líneas, densidad gráfica y procedimientos programados.

[![Mark Wilson, 30A94, 1994](https://dam.org/museum/wp-content/uploads/2020/11/Wilson1994_30A94.jpg)](https://dam.org/museum/artists_ui/artists/wilson-mark/wilson-plotter-drawings/)

`30A94`, 1994. Composición de apariencia arquitectónica o de circuito, formada
por módulos, grillas y pequeños signos repetidos.

[![Mark Wilson, csq3600_hd, 2008](https://dam.org/museum/wp-content/uploads/2020/11/csq3600_hd_2008-copy.jpg)](https://dam.org/museum/artists_ui/artists/wilson-mark/)

`csq3600_hd`, 2008. Obra posterior donde el pixel mapping se vuelve más denso y
colorido mediante impresión digital de gran formato.

### Relación con p5.js

El trabajo de Mark Wilson se puede relacionar con p5.js a través de:

- imágenes construidas por pixeles o módulos;
- grillas transformadas;
- repetición de unidades mínimas;
- uso de azar y permutaciones;
- traducción de datos visuales en formas geométricas;
- capas de procesos que vuelven la imagen más compleja.

En p5.js, esto invita a pensar cada punto, cuadrado o línea como una unidad que
puede cambiar de tamaño, posición, color o forma según una regla.

### Conceptos clave

- **Arte generativo**: obra creada a partir de reglas, sistemas o algoritmos.
- **Plotter**: máquina que dibuja físicamente siguiendo instrucciones digitales.
- **Algoritmo visual**: conjunto de pasos para producir una imagen.
- **Variación**: cambio controlado dentro de una estructura.
- **Orden/desorden**: tensión entre una grilla estable y alteraciones azarosas.
- **Pixel mapping**: traducción de una imagen digital a una superficie mediante
  unidades visuales como puntos, cuadrados, cruces o líneas.

### Fuentes consultadas

- Thoma Foundation, ficha de `Transformations`: https://thomafoundation.org/artwork/transformations/
- Victoria and Albert Museum, `Digital art`: https://www.vam.ac.uk/articles/digital-art
- MoMA, ficha de Vera Molnár: https://www.moma.org/artists/37083-vera-molnar
- DAM Museum, página de Vera Molnár: https://dam.org/museum/artists_ui/artists/molnar-vera/
- National Gallery of Art, `Interruptions`: https://www.nga.gov/artworks/216160-interruptions
- DAM Museum, `Plotter Drawings from 1960s`: https://dam.org/dox/2658.kL95E.H.1.De.php
- DAM Archive, `RAM 1968-1969`: https://dam.org/archive/zajec/1968-69-ram.htm
- ZKM, ficha de Edward E. Zajec: https://zkm.de/en/persons/edward-e-zajec
- DAM Museum, ficha de Mark Wilson: https://dam.org/museum/artists_ui/artists/wilson-mark/
- DAM Museum, `Plotter drawings` de Mark Wilson: https://dam.org/museum/artists_ui/artists/wilson-mark/wilson-plotter-drawings/
- DAM Museum, `Works from 1990-92` de Mark Wilson: https://dam.org/museum/artists_ui/artists/wilson-mark/works-from-90s/
- DAM Museum, entrevista `Mark Wilson: painting is an algorithmic procedure`: https://dam.org/museum/mark-wilson-interview/
- Digital Art Museum Archive, statement de Mark Wilson: https://digitalartmuseum.org/wilson/biog2.html
- Google Books, `Drawing with Computers`: https://books.google.com/books/about/Drawing_with_Computers.html?id=5u0YAQAAIAAJ
- MoMA, ficha de Victor Vasarely: https://www.moma.org/artists/6109-victor-vasarely
- Buffalo AKG Art Museum, `Vega-Nor`: https://buffaloakg.org/artworks/k196929-vega-nor
- Städel Museum, retrospectiva de Victor Vasarely: https://vasarely.staedelmuseum.de/en/
- Princeton University Art Museum, `Permutations`: https://artmuseum.princeton.edu/art/collections/objects/11032
- The Phillips Collection, `Vega WA-2`: https://www.phillipscollection.org/collection/vega-wa-2
- MFAH, `Planetary Folklore Participations No. 1`: https://emuseum.mfah.org/objects/78537/planetary-folklore-participations-no-1
