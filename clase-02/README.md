# clase-02

Jueves 13 de agosto de 2026

Profesor: Christian Oyarzun Roa
Correo: coyarzun@error404.cl

## Apuntes sobre p5.js

p5.js es una biblioteca libre y de código abierto escrita en JavaScript, pensada para programación creativa, arte generativo e interacción en la web. Hereda ideas de Processing, especialmente la noción de trabajar con código como *sketch* o boceto.

p5.js simplifica el uso de JavaScript y tecnologías web como HTML5 y `canvas`. En vez de programar directamente toda la lógica del navegador, ofrece una API con funciones como `createCanvas()`, `background()`, `circle()`, `setup()` y `draw()`.

El `canvas` funciona como una superficie de dibujo dentro de una página web. El p5.js Web Editor es un IDE en línea que permite escribir, ejecutar, guardar y compartir *sketches* desde el navegador, sin instalar herramientas locales.

API significa *Application Programming Interface*. En p5.js, la API es el conjunto de funciones y variables disponibles para dibujar, animar e interactuar, por ejemplo `createCanvas()`, `draw()`, `mouseX` o `keyPressed()`.

IDE significa *Integrated Development Environment*. En p5.js, el Web Editor funciona como un IDE porque permite escribir código, ejecutarlo, ver errores, guardar proyectos y compartirlos desde una misma interfaz.

## Lenguajes de máquina y compilación

Lenguajes como C, C++ y Java permiten escribir instrucciones en una forma entendible para las personas, pero esas instrucciones deben traducirse para que el computador pueda ejecutarlas.

En C y C++, el código fuente se compila: un programa llamado compilador traduce el código a lenguaje de máquina, es decir, instrucciones que el procesador puede ejecutar.

Java también se compila, pero de otra forma: el código se traduce primero a *bytecode*, un formato intermedio que luego se ejecuta en la máquina virtual de Java, o JVM. Esto permite que un mismo programa pueda correr en distintos sistemas si tienen instalada la JVM.

## Lenguajes de script

Los lenguajes de script, como JavaScript, Python o Ruby, suelen ejecutarse mediante un intérprete. Esto significa que el código no necesita convertirse previamente en un archivo ejecutable de lenguaje de máquina, sino que otro programa lo lee y lo ejecuta.

Estos lenguajes se usan mucho para automatizar tareas, crear páginas web interactivas, trabajar con datos y hacer prototipos rápidos. En la web, JavaScript es interpretado por el navegador, lo que permite modificar una página mientras está funcionando.

Actualmente, algunos lenguajes de script usan técnicas mixtas, como compilación en tiempo de ejecución o JIT (*Just-In-Time*), para mejorar el rendimiento. Por eso, la diferencia entre compilado e interpretado no siempre es absoluta, pero sirve para entender distintas formas de ejecutar código.

## Fuentes

p5.js. "About." https://p5js.org/about/

p5.js. "Setting Up Your Environment." https://p5js.org/tutorials/setting-up-your-environment/

p5.js. "Get Started." https://p5js.org/tutorials/get-started
