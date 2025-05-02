# Animaciones

---

- [Transiciones](#transiciones)
- [Animaciones](#animacion)
- [Trayectos animados](#trayectos-animados)
- [Animaciones dirigidas por scroll](#animaciones-dirigidas-por-scroll)
- [View Transition](#view-transition)

---

Las animaciones son pequeños cambios en el contenido o aspecto visual de una página, de modo que sea más amigable su visualización. Pueden ser sencillas, como cambiar el color o tamaño de una imagen, así como animaciones más complejas, como por ejemplo transformaciones o movimientos específicos.

En las animaciones hay dos conceptos básicos importantes:

- `Estado`: Es el estado inicial en el que se encuentra un elemento de la web (imagen, botón, etc...)
- `Transición`: Es el paso que se realiza entre un estado concreto a otro estado diferente.

![](https://lenguajecss.com/animaciones/bases/que-son-animaciones/conceptos.png)

### Propósito de una animacion

Además de lo mencionado, crear una animación generalmente tiene varios propósitos u objetivos. Los principales suelen ser los siguientes:

- 1️⃣ **Mejorar la experiencia del usuario (UX):** El usuario sentirá que su estancia en la web es más satisfactoria y agradable, por lo que preferirá continuar su navegación.

- 2️⃣ **Guíar o dirigir la atención del usuario:** Las animaciones son buenas para llamar la atención del usuario y poner el foco en una parte concreta a la que debe darle prioridad.

- 3️⃣ **Retroalimentar las acciones del usuario:** Las animaciones permiten dar feedback al usuario para saber si está haciendo lo correcto o, por el contrario, se ha equivocado o ha hecho algo que no debe hacer.

- 4️⃣ **Crear narrativas o efectos visuales:** Por último, las animaciones se pueden utilizar para crear narrativas, historias, decorar la página o simplemente dotar de elementos atractivos a una web.


Para que una animación sea perceptible al ojo humano, se necesitan varios fotogramas. En los navegadores, esos fotogramas corresponden a diferentes estados del elemento. En lugar de definir cada fotograma manualmente, se usan fotogramas clave (keyframes), y el navegador se encarga de generar automáticamente los estados intermedios entre ellos durante la animación.

![](https://lenguajecss.com/animaciones/bases/que-son-animaciones/fotogramas.png)


### Tipo de animacion

| Tipo de animación       | Descripción                                                                 |
|--------------------------|------------------------------------------------------------------------------|
| Transiciones             | Una animación simple, desde un estado inicial a un estado final.           |
| Animaciones              | Una animación más compleja, con 2 o más estados.                           |
| Trayectos animados       | Movimiento de un elemento a lo largo de un trayecto o ruta.                |
| Animaciones de scroll    | Animación controlada por desplazamiento de ratón.                          |
| View Transition          | Animación de vistas, al cambiar de una página a otra.                      |
| WebAnimations            | Animaciones nativas complejas, creadas desde Javascript.                   |


### Transiciones

Una transición es un tipo de animación simple que ocurre entre dos estados diferentes, generalmente activada por la interacción del usuario. Su propósito es suavizar el cambio de estado. A diferencia de las animaciones más complejas o autónomas, las transiciones suelen ser más apropiadas en estos casos.


```html
<div class="box"></div>
```

```css
.box {
  width: 200px;
  height: 200px;

  background: indigo;
  transition: background 1s linear; /* <- transisción de cambio de color */

  &:hover {
    background: hotpink;
  }
}
```

Al mover el ratón sobre el elemento, se activa la transición de un estado inicial (sin ratón encima) a uno final (con ratón encima). En general, si es posible, tu primera opción debería ser realizar una transición.


#### Transición de entrada y salida

Las transiciones son los cambios de un estado a otro.

Es interesante tener en cuenta que hay dos tipos de transiciones: de entrada y de salida. Las transiciones de entrada se aplican cuando el estado inicial cambia al estado final (se produce la condición: el ratón encima del elemento), mientras que las transiciones de salida se aplican cuando se deja de cumplir dicha condición (se quita el ratón encima del elemento), volviendo a su estado inicial:

![](https://lenguajecss.com/animaciones/transiciones/que-son/transiciones-entrada-salida.png)

#### Transición de entrada

Sin embargo, hay que tener en cuenta que en su lugar, también es posible añadirla en el bloque .element:hover. De esta forma, la transición sólo se aplica cuando el usuario tiene el ratón encima del elemento, por lo que sólo ocurriría en la transición de entrada:

```css
/* <div class="element"></div> */
.element {
  width: 100px;
  height: 100px;
  background: red;
}

.element:hover {
  background: blue;
  transition: 2s;
}
```

La transición solo se dá cuando ponemos el cursor sobre el elemento. Cuando lo quitamos hay un cambio brusco de colores.

#### Transición de salida

Por otro lado, utilizando :not(:hover) podemos invertir la situación y conseguir que sólo se aplique la transición de salida, ya que sólo entrará en efecto cuando el usuario no tenga el ratón encima del elemento:

```css
/* <div class="element"></div> */
.element {
  width: 100px;
  height: 100px;
  background: red;
}

.element:not(:hover) {
  background: blue;
  transition: 2s;
}
```

La transición solo se dá cuando quitamos cursor sobre el elemento. Al principio hay un cambio bruco de colores.

#### Transiciones por propiedad

Es posible que queramos indicar (por ejemplo) diferentes duraciones dependiendo de la propiedad CSS. Por ejemplo, que tarde mucho en cambiar el ancho del elemento, pero muy poco en cambiar el color de fondo.

Para ello, podemos separar con comas las diferentes propiedades que queremos transicionar:


```css
/* <div class="element"></div> */
.element {
  width: 200px;
  height: 200px;
  background: grey;
  transition:
    width 4s,
    background 1s;
}

.element:hover {
  width: 400px;
  background: deeppink;
}
```

![](../img/transition%201.png)

Observa que en este caso, la transición de ancho (propiedad width de CSS) tardará 4 segundos en cambiar, mientras que la transición del color de fondo (propiedad background de CSS) tardará muy poco, sólo 1s.

#### Desencadenante de la transicion

En estos ejemplos hemos utilizado `:hover` como desencadenante de la transición CSS porque es muy sencillo de visualizar en los ejemplos. Sin embargo, existen muchísimas formas que podemos utilizar para desencadenar una transición:


| Desencadenante | Descripción                                                                 |
|----------------|------------------------------------------------------------------------------|
| `:hover`       | Cuando mueves el ratón (o dispositivo apuntador) sobre un elemento.         |
| `:active`      | Cuando estás pulsando con el ratón (o dispositivo apuntador) sobre un elemento. |
| `:focus`       | Cuando un elemento gana el foco (por ejemplo, entrar en un campo de texto `<input>`). |


#### Propiedades de transicion CSS

| Propiedades                 | Descripción                                     | Valor                                             |
|----------------------------|-------------------------------------------------|--------------------------------------------------|
| `transition-duration`      | Tiempo de duración.                             | `0` \ `time`                                            |
| `transition-property`      | Propiedades CSS afectadas por la transición.    | `all` \ `none` \ nombre de una propiedad CSS      |
| `transition-timing-function` | Ritmo de la transición.                        | Ver funciones de tiempo                          |
| `transition-delay`         | Tiempo de retardo inicial.                      | `0` \ `time`                                    |
| `transition-behavior`      | Permite realizar transiciones discretas.        | `normal` \ `allow-discrete`                     |


#### Propiedad `transition-duration`

Con la propiedad `transition-duration` especificaremos la duración de la transición, desde el inicio de la transición, hasta su finalización. Recuerda que por defecto, las transiciones tienen una duración de 0s, por lo que si no cambias este valor, cambiará de golpe y será lo mismo que no tener transición.

```css
/* <div class="element"></div> */
.element {
  transition-duration: 0.5s; /* duración de la animación */
  width: 200px;
  height: 200px;
  background: grey;
}

.element:hover {
  background: indigo;
}
```

#### propiedad `transition-property`

En primer lugar, la propiedad `transition-property` se utiliza para especificar la propiedad a la que que afectará la transición. Podemos especificar la propiedad concreta (`width` o `color`, por ejemplo) o simplemente especificar all para que se aplique a todos los elementos con los que se encuentre. Por otro lado, none hace que no se aplique ninguna transición.

| Propiedades     | Valor                                                                 |
|-----------------|-----------------------------------------------------------------------|
| `all`           | Aplica la transición a todas las propiedades CSS.                    |
| `none`          | No aplica transición. El cambio se producirá de golpe (brusco).       |
| `propiedad css` | Aplica la transición sólo a la propiedad CSS especificada.           |

Propiedades que se pueden animar en css:

| Categoría                 | Propiedades animables                                                 |
|--------------------------|------------------------------------------------------------------------|
| 🎨 Colores               | `color`, `background-color`, `border-color`, `outline-color`, `fill`, `stroke`, `text-decoration-color` |
| 📐 Tamaño y caja         | `width`, `height`, `max-width`, `max-height`, `min-width`, `min-height`, `padding`, `margin`, `border-width`, `outline-width`, `border-spacing` |
| 🔄 Transformaciones      | `transform` (como `rotate`, `scale`, `translate`, etc.)               |
| 🔳 Posición              | `top`, `right`, `bottom`, `left`, `inset`, `z-index` (solo en animaciones) |
| 🌫️ Opacidad             | `opacity`, `visibility` (solo con `allow-discrete`)                    |
| ✨ Sombras y filtros     | `box-shadow`, `text-shadow`, `filter`                                 |
| 🔠 Texto y fuente        | `letter-spacing`, `word-spacing`, `line-height`, `font-size`, `font-weight` |
| 🖼️ Fondo y objeto       | `background-position`, `background-size`, `object-fit`, `object-position` |
| 📐 Layout (limitado)     | `flex`, `flex-grow`, `flex-shrink`, algunas propiedades de `grid`     |


Ten en cuenta que para la transición se efectue correctamente, deberíamos tener un `estado inicial` y un `estado final`, en caso contrario, el navegador podría no saber uno de esos estados y por lo tanto, no podría efectuar la transición. En algunos casos no será necesario el estado inicial puesto que tomará el valor por defecto.

Ten en cuenta que puedes animar todas las propiedades CSS afectadas utilizando `all`:


```css
.element {
  /* Primer ejemplo: Anima todas las propiedades que cambien de estado */
  transition-property: all;
  transition-duration: 1s;

  /* Segundo ejemplo: Anima sólo el ancho, el resto no transicionan, cambian de golpe */
  transition-property: width;
  transition-duration: 1s;
}
```

#### Propiedad `transition-delay`

La propiedad `transition-delay` nos ofrece la posibilidad de retrasar el inicio de la transición un número de segundos determinado. Si se omite, la transición comienza inmediatamente.

Veamos un pequeño ejemplo de todas estas propiedades de transición:

```css
/* <div class="element"></div> */
.element {
  display: inline-block;
  background: #777;
  padding: 1rem;

  transition-property: all;
  transition-duration: 0.5s;
}

.element:hover {
  background: indigo;
  padding: 2rem 4rem;
  color: #fff;
}
```

En este ejemplo, con all hemos determinado animar todas las propiedades que cambien:

- La propiedad `background` de color de fondo cambiará de #777 a indigo
- La propiedad `color` de color de texto cambiará, de #000 (por defecto) a #fff.
- La propiedad `padding` del tamaño del relleno cambiará de 1rem a 2rem 4rem
- La propiedad `display` no cambiará, puesto que es inline-block en ambas.


#### Propiedad `transition-behavior`

Existe una nueva propiedad `transition-behavior` que permite realizar transiciones en propiedades con valores discretos. ¿Esto que significa? Tradicionalmente, en CSS, sólo se podían crear transiciones en propiedades que tengan valores cuantificables, como por ejemplo:

- `opacity`: Valores decimales entre 1 y 0 o porcentajes entre 0% y 100%.
- `background` o `color`: Los colores son valores hexadecimales (numéricos), por lo que son cuantificables.
- `padding` o `margin`: Son tamaños, cantidades numéricas.


```css
dialog {
  display: none;
  opacity: 0%;
  transition-duration: 1s;
  transition-property: opacity, display;
}

input:checked ~ dialog {
  transition-behavior: allow-discrete;
}

dialog[open] {
  opacity: 100%;
  display: block;
}
```

#### Atajo: propiedad `transition`

Como siempre, podemos resumir todas estas operaciones en una propiedad de atajo denominada `transition`. Los valores del ejemplo superior, se podrían escribir como se puede ver a continuación (si no necesitas algún valor, se puede omitir):


```html
<div class="box"></div>
```


```css
.box {
  /* transition: <property> <duration> <timing-function> <delay> <behavior> */
  transition: all 0.5s linear;

  background: grey;
  width: 200px;
  height: 200px;
}

.box:hover {
  background: indigo;
}
```

![](../img/transition%202.png)


#### Ejemplos usando transiciones

En el siguiente ejemplo haremos un elemento circulo que funcione como un pulser (latidos) cada que hacemos :hover.

>**Recordar:** La propiedad `transition` va siempre en el elemento (div, button...) donde empieza el estado inicial, **NO** en el :hover.

```html
<div class="pulser"></div>
```

```css
.pulser {
  width: 30px;
  height: 30px;
  background-color: #09f;
  border-radius: 50%;
  position: relative;

  /* 
  transition-property: background-color, scale;
  transition-duration: 1s;
  transition-timing-function: ease-in;
  transition-delay: .2s; 
  */
  transition: all 300ms ease-in .2s; /* <- atajo */
}

.pulser:hover {
  scale: 2;
  background-color: purple;
  box-shadow: 0 0 10px purple;
}
```

![](../img/transition%203.png)

Podemos hacer que cada propiedad tenga su estilo de transición, solo tienes que separar por comas y especificar los valores:

```css
/* atajo */
  transition: 
    background-color 1s ease-in .1s, /* <- transition para el fondo */
    scale 500ms ease-in-out .1s;     /* <- transition para el escalado */
```

### Animacion

Una vez conocemos las transiciones CSS, es muy fácil adaptarnos al concepto de animaciones CSS, el cual amplia lo que ya sabemos de transiciones, convirtiéndolo en algo mucho más flexible y potente, en el que no es necesario que el usuario desencadene la animación (como ocurre con las transiciones).

Para crear animaciones CSS es necesario realizar 2 pasos:

- 1️⃣ Utilizar la propiedad animation para indicar que elemento HTML vamos a animar.
- 2️⃣ Definir mediante la regla @keyframes los estados de la animación (fotogramas clave).

#### Propiedades de animacion CSS

Para el comportamiento de una animación, necesitamos conocer las siguientes propiedades, que son una «ampliación» de las propiedades de las transiciones CSS:


| Propiedad                  | Descripción                                      | Valor                                                             |
|---------------------------|--------------------------------------------------|-------------------------------------------------------------------|
| `animation-name`          | Nombre de la animación a aplicar.                | `none` \ nombre personalizado                                         |
| `animation-duration`      | Duración de la animación.                        | `0` (segundos) \ tiempo en `s` o `ms`                                           |
| `animation-timing-function` | Ritmo de la animación.                        | Ver funciones de tiempo (`ease`, `linear`, `ease-in`, etc.)       |
| `animation-delay`         | Retardo en iniciar la animación.                | `0` \ tiempo en `s` o `ms`                                           |
| `animation-iteration-count` | Número de veces que se repetirá.             | `1` \ `infinite` \ número                                                        |
| `animation-direction`     | Dirección de la animación.                      | `normal` \ `reverse` \ `alternate` \ `alternate-reverse`        |
| `animation-fill-mode`     | Cómo se «completa» la animación.                | `none` \ `forwards` \ `backwards` \ `both`                    |
| `animation-play-state`    | Estado de la animación.                         | `running` \ `paused`                                                |
| `animation-composition`   | Cómo se «mezclan» varias animaciones.           | Ver composición de animaciones                                    |
| `animation-timeline`      | Define una línea de tiempo animada.             | Ver animaciones de scroll (`scroll()`, personalizadas, etc.)      |

#### Atajo: Animaciones

Nuevamente, CSS ofrece la posibilidad de resumir todas estas propiedades en una sola, para hacer nuestras hojas de estilos más compactas. El orden recomendado para los valores de la propiedad de atajo sería el siguiente:

```css
.element {
  /* animation: <name> <duration> <timing-function> <delay> <iteration-count> <direction> <fill-mode> <play-state> */

  animation:
    change-color 5s linear 0.5s 4 normal forwards running;
}
```

#### Sintaxis de `@keyframes`

Para definir esos fotogramas clave, utilizaremos la regla `@keyframes`, la cuál es muy sencilla de utilizar. Se basa en el siguiente esquema:

![](https://lenguajecss.com/animaciones/animaciones/keyframes/keyframes-syntax.png)

Cada uno de estos time-selector será un momento clave de cada uno de los fotogramas clave de nuestra animación, y ya veremos que pueden definirse muchos en una misma animación.

| Parte               | Descripción                                                                 |
|---------------------|------------------------------------------------------------------------------|
| `@keyframes`        | Regla CSS que indica que se va a definir una animación.                     |
| `nombre-animation`  | Nombre de la animación. Debe estar en *kebab-case*. Evitar `camelCase`, `PascalCase` u otras. |
| `time-selector`     | Fotograma clave a definir. Puede ser un porcentaje (`0%`, `50%`, etc.) o un valor como `from` o `to`. |

#### Selectores from y to

Empecemos por la forma más sencilla. Vamos a crear un ejemplo utilizando los selectores from y to, ideados para indicar de forma simple el fotograma clave inicial y el fotograma clave final de la animación.

Esto siempre se ve mejor con un ejemplo, así que vamos a ello:

```css
@keyframes change-color {
  from { background: red; }  /* Primer fotograma clave */
  to { background: green; }  /* Segundo y último fotograma clave */
}
```

#### Estados y transiciones

Mientras que en temas anteriores aprendimos que las Transiciones CSS son cambios de un estado inicial a un estado final, en el caso de las Animaciones CSS se trata de un conjunto de transiciones entre estados, de modo que es posible cambiar entre dos o más estados, a diferencia de las transiciones, donde solo puedes cambiar entre dos estados.

![](https://lenguajecss.com/animaciones/animaciones/que-son/conceptos.png)

#### Animación y fotogramas

En las Animaciones CSS es necesario definir dos pasos para crear una animación:

- 1️⃣ En primer lugar, usar la propiedad animation en el elemento HTML a animar.
- 2️⃣ En segundo lugar, crear las animaciones mediante la regla @keyframes.

Veamos un ejemplo, muy sencillo de una animación de 3 estados:


```html
<div class="box"></div>
```

```css
.box {
  width: 200px;
  height: 200px;
  background: grey;

  animation: change-color 3s infinite alternate linear;
}


@keyframes change-color { /* <- nombre de la animación */
  0% { background: red; }
  50% { background: gold; }
  100% { background: green; }
}
```

![](../img/animation%201.png)


#### Animaciones multiples

Como en muchas propiedades de CSS, es posible separar sus valores mediante comas para indicar múltiples valores. En este caso, esos multiples valores indicarán que queremos realizar varias animaciones a la vez.

Observa el siguiente ejemplo, donde indicamos que tanto la animación move-right como la animación change-color deben empezar a la vez. Cada una de ellas durará 5 segundos:

```css
.element {
  animation:
    move-right 5s,
    change-color 5s;
}
```

Es posible encadenar animaciones utilizando animaciones múltiples combinadas con la propiedad animation-delay.

Observa el siguiente ejemplo donde se verá mucho mejor. El primer valor de tiempo es la duración de la animación, el segundo valor de tiempo es el tiempo que tarda en iniciarse la animación:

```css
.element {
  animation:
    move-right 5s 0s,   /* Comienza a los 0s (no hay anterior) */
    look-up 2.5s 5s,    /* Comienza a los 5s (5 de la anterior) */
    move-left 5s 7.5s,  /* Comienza a los 7.5s (5 + 2.5 de la anterior) */
    dissapear 2s 9.5s;  /* Comienza a los 9.5s (5 + 2.5 + 2 de la anterior) */
}
```

Ejemplo de animación multiple:

```html
<div class="element"></div>
```

```css
.element {
  width: 100px;
  height: 100px;
  background: grey;
  animation:
    move 3s infinite 0s,
    rotate 3s infinite 3s;
}


@keyframes move {
  to {
    transform: translateX(500px);
    background: red;
  }
}


@keyframes rotate {
  to {
    transform: rotate(360deg) scale(0.5);
    background: indigo;
  }
}
```

![](../img/animation%202.png)

### Trayectos animados

En alguna ocasión nos puede interesar animar un elemento a través de una ruta. Esto se puede lograr mediante los trayectos animados. Este tipo de animaciones son muy sencillas de crear, y se basa en definir una ruta mediante un trayecto SVG.


```html
<div class="box"></div>
```


```css
.box {
  width: 50px;
  height: 75px;
  border-left: 5px solid hotpink;
  border-right: 5px solid red;
  background: indigo;
  offset-path: path("m 0 25 h 150 v 100 h 100");
  animation: move-path 3s infinite alternate linear;
}

@keyframes move-path {
  0% { offset-distance: 0%; }
  100% { offset-distance: 100%; }
}
```

Aquí un ejemplo de como animar una imágen de Mario para hacer que se mueva en línea recta de forma infinita:

```html
<img src="https://w7.pngwing.com/pngs/495/459/png-transparent-super-mario-bros-mario-yoshi-bowser-mario-bros-angle-super-mario-bros-text-thumbnail.png" alt="">
```

```css
img {
  width: 70px;
  
  animation-name: mover;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
}

@keyframes mover {
  from {
    transform: translateX(0);
  }

  to {
    transform: translateX(200px);
  }
}
```

![](../img/animation%203.png)


Podemos cambiar la dirección de la animación de manera que empiece desde la to al from


```css
img {
  width: 70px;
  
  animation-name: mover;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  animation-direction: reverse; /* <- dirección de la animación: con el valor de  `alternate` podemos hacer que alterne de izquierda a derecha y viciversa */

}
```

Otra cosa que podemos hacer es pausar las animaciones, esto no es muy común pero puede utilizarse en casos especiales, por ejemplo en nuestra animación cuando hacemos `:hover` se pausa la animación.


```css
img:hover {
  animation-play-state: paused;
  opacity: .7;
  filter: contrast(150%);
  cursor: progress;
}
```

![](../img/animation%204.png)


Otro aspecto importante en la animaciones es que cuando esta termina su animación para ello tenemos la propiedad `animation-fill-mode` que define cómo se aplican los estilos de una animación antes de que comience o después de que termina..

| Valor        | Descripción                                                                                 |
|--------------|---------------------------------------------------------------------------------------------|
| `none`       | **Valor por defecto.** El elemento no conserva estilos de la animación antes o después.     |
| `forwards`   | Mantiene los estilos del **último fotograma** después de que la animación termina.          |
| `backwards`  | Aplica los estilos del **primer fotograma** antes de que la animación empiece (útil con `animation-delay`). |
| `both`       | Combina `forwards` y `backwards`: conserva estilos **antes y después** de la animación.     |


```css
img {
  width: 70px;
  
  animation-name: mover;
  animation-duration: 2s;
  /* animation-iteration-count: infinite; */
  animation-timing-function: linear;
  animation-direction: normal;
  animation-fill-mode: forwards; 
}
```

Podemos usar la propiedad de atajo `animation`.

```css
img {
  width: 70px;
  
  /* animation: mover;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  animation-direction: normal;
  animation-fill-mode: forwards;  */

  /* atajo */
  animation: mover 2s linear infinite;
}
```


### Animaciones dirigidas por scroll

Otro tipo de animaciones son las Scroll Driven Animation (Animaciones dirigidas por desplazamiento). Estas animaciones se basan en el scroll realizado por el usuario a lo largo de la página o de una región concreta. Observa el siguiente ejemplo, donde incrementamos o decrementamos la barra amarilla dependiendo del scroll realizado:


```html
<section class="page page-1">Página 1</section>
<section class="page page-2">Página 2</section>
<section class="page page-3">Página 3</section>
<section class="page page-4">Página 4</section>
<div class="indicator"><div class="bar"></div></div>
```


```css
body {
  margin: 0;
  height: 200px;
}

section.page {
  height: 100vh;
  color: white;
  background: color-mix(in srgb, indigo, black var(--dark));
}

.page-1 { --dark: 0% }
.page-2 { --dark: 25% }
.page-3 { --dark: 50% }
.page-4 { --dark: 75% }

.indicator {
  background: grey;
  width: 100px;
  height: 25px;
  position: fixed;
  top: 25px;
  right: 50px;

  & .bar {
    width: 0%;
    height: 100%;
    background: gold;
    animation: resize auto linear;
    animation-timeline: scroll(root block);
  }
}

@keyframes resize {
  0% { width: 0% }
  100% { width: 100% }
}
```

Veamos otro ejemplo de como usar las animaciones con scroll.

En este ejemplo haremos una barra de progreso la cual crece a medida que vamos haciendo scroll.


```html
<body>

  <div id="progress"></div>

  <main>
    <h1>La Importancia de Saber Tomar Buenas Notas</h1>

  <p>Tomar buenas notas es una habilidad fundamental tanto para estudiantes como para profesionales. No solo ayuda a registrar la información que se presenta en clases, reuniones o lecturas, sino que también facilita el proceso de comprensión, memorización y aplicación del conocimiento. A menudo se subestima el poder de una buena toma de notas, pero aquellos que dominan esta práctica suelen destacar por su capacidad de retener y utilizar información de manera más efectiva.</p>

  <p>Una buena nota no es simplemente una transcripción palabra por palabra de lo que se dice. De hecho, tomar notas de forma literal puede ser contraproducente. Lo ideal es que las notas sean un reflejo procesado de la información, escritas en palabras propias, destacando ideas clave, relaciones entre conceptos y puntos de interés. Esto obliga al cerebro a trabajar activamente, lo cual mejora significativamente la comprensión y el aprendizaje a largo plazo.</p>

  <h2>Beneficios de una Buena Toma de Notas</h2>

  ...
```

```css
body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  margin: 0;
  max-width: 800px;
}
main {
  padding: 32px;
}
h1, h2 {
  color: #2c3e50;
}
p {
  margin-bottom: 1em;
}

#progress {
  position: fixed;
  top: 0;
  width: 0%;
  background-color: red;
  height: 1em;

  /* 
    animation-name: progress-grow;
    animation-duration: auto;
    animation-timing-function: linear; 
  */
  animation: progress-grow auto linear; /* <- atajo */
  animation-timeline: scroll(root block);
}

@keyframes progress-grow {
  from { width: 0%; }
  to { width: 100%; }
}
```

![](../img/animation%20scroll%201.png)


### View Transition

Las View Transition (Transiciones de vista) son un tipo de animación que se produce al realizar un cambio de página. El navegador toma una captura del aspecto visual antes de cambiar de página, la congela y realizar el cambio a la otra página. Una vez en la otra página, realiza una transición suave hacia la nueva página.

De esta forma, las animaciones mostradas son muy agradables, y simulan ser instantáneas aunque realmente estén recargando toda la página.

---