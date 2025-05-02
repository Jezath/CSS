# Responsive Web Design

---

- [Conceptos basicos](#conceptos-basicos)
- [Bases del Responsive Design](#bases-del-responsive-design)
- [Media Queries](#media-queries)
- [Container Queries](#container-queries)
- [Media querys mas usadas](#media-querys-mas-usadas)

---

Actualmente, el uso de diversos dispositivos móviles con acceso a Internet ha aumentado considerablemente, lo que ha generado nuevas formas de consumir contenido web, así como diferentes necesidades, problemas y soluciones debido a la variedad de tamaños y resoluciones de pantalla.

![](https://lenguajecss.com/css/responsive-web-design/que-es/responsive-web-design.png)


Hoy en día, al diseñar una web, es fundamental que se adapte a distintas resoluciones de pantalla, lo cual no siempre es sencillo. Antes se creaban versiones específicas para cada dispositivo o navegador, pero esto se abandonó por ser poco práctico. Actualmente, se utiliza el Responsive Web Design (RWD), una técnica que permite que una sola web se adapte visualmente a cualquier dispositivo, a diferencia de los antiguos diseños fijos.

### Conceptos basicos

#### Responsive vs Adaptative

El primero de ellos es la diferencia entre **diseño responsivo** y **diseño adaptativo**. Como se puede ver en la imagen a continuación, un diseño responsive responde (valga la rebuznancia) en todo momento a las dimensiones del dispositivo, mientras que un diseño adaptable es aquel que se adapta, pero no necesariamente responde en todo momento:

![](../img/Responsive%20vs%20Adaptative.png)

#### Unidades relativas vs estaticas

Por otro lado, para trabajar correctamente en diseños responsive hay que tener en cuenta que debemos trabajar con unidades relativas e intentar evitar las unidades fijas o estáticas, las cuales no responden a la adaptación de nuestros diseños flexibles:

![](../img/Unidades%20relativas%20vs%20estaticas.png)

#### Con maximos y sin maximos

Otra forma interesante de trabajar esa respuesta de los diseños responsive es utilizar propiedades como min-width o max-width, donde definimos tamaños mínimos o máximos, para que los elementos de nuestra página puedan ampliar o reducirse según sea necesario dependiendo de la pantalla del dispositivo utilizado.

![](../img/Con%20máximos%20y%20sin%20máximos.png)

#### Flujo vs Estático


Una característica clave del diseño responsive es mantener el flujo de los elementos al cambiar de tamaño, evitando que se solapen. Aunque adaptarse desde diseños estáticos puede ser complicado al principio, una vez logrado, se obtiene una mayor fluidez visual y una mejor experiencia para el usuario.

![](../img/Flujo%20vs%20Estático.png)

#### Con breakpoints vs sin breakpoints

Esto último va muy de la mano del sistema habitual de recolocación de elementos que se suele seguir en los diseños Responsive Design. Como se puede ver en la siguiente imagen, en un diseño responsive se utilizan ciertos «puntos de control».

Por ejemplo, se suele pensar que en una resolución de escritorio queremos mostrar la información dentro de una cuadrícula (grid) de 4 ó 5 celdas de ancho, mientras que en la versión de tablet será sólo de 3 celdas de ancho (el resto se desplazará a la siguiente fila) y en móviles será una sola celda de ancho, mostrándose el resto de celdas haciendo scroll hacia abajo:

![](../img/Con%20breakpoints%20vs%20sin%20breakpoints.png)

Esta forma de trabajar nos proporciona múltiples ventajas:

- Es mucho más sencillo mostrar la misma información desde diseños de pantalla grande.
- Ayuda a evitar la mala práctica de ocultar bloques de información en dispositivos móviles.
- Incentiva a diseñar siguiendo buenas prácticas para facilitar la creación responsive.


#### Estrategias de diseño

Por último, es aconsejable decidirse por una estrategia de diseño antes de comenzar. Aunque existen otras estrategias, las dos vertientes principales 


| Estrategia     | Descripción                                                                 |
|----------------|------------------------------------------------------------------------------|
| Mobile first   | Primero nos enfocamos en dispositivos móviles y luego pensamos en otros.    |
| Desktop first  | Primero nos enfocamos en dispositivos de escritorio, y luego pensamos en otros. |


### Bases del Responsive Design

#### Diseño con porcentajes

El primer paso para crear un diseño que se adapte correctamente, es comenzar a familiarizarse con un tipo de unidades: los porcentajes. Recordemos que los porcentajes son relativos al contenedor padre, por lo que si especificamos un porcentaje a un elemento, el navegador va a tomar dicho porcentaje del contenedor.

Empecemos usando porcentajes con las propiedades width en un ejemplo sencillo. Vamos a establecer:

- Un ancho de 100% a header, .page y footer
- Un ancho de 30% a .menu
- Un ancho de 70% a .content

```html
<header></header>
<div class="page">
  <div class="menu"></div>
  <div class="content"></div>
</div>
<footer></footer>
```

```css
header,
.page,
footer {
  min-height: 200px;
  background: grey;
}

.menu {
  min-height: 200px;
  display: inline-block;
  background: blue;
  width: 30%;
}

.content {
  min-height: 200px;
  display: inline-block;
  background: lightgrey;
  width: 70%;
}
```

Obtendríamos un diseño similar al siguiente:

![](https://lenguajecss.com/css/responsive-web-design/bases-responsive/rwd-porcentajes.png)


Sin embargo, utilizar porcentajes no nos garantiza un diseño adaptativo de calidad, hay que comprender bien varios detalles. El primer problema que encontraremos será que si sumamos el tamaño de los elementos `70%` + `30%`, junto a los bordes de cada uno, `2px` por cada lado, la suma es superior al `100%` del contenedor padre, por lo que no cabe en su interior. El segundo elemento se desplaza a la zona inferior, descuadrando todo el diseño. Lo mismo puede ocurrir si intentamos añadir `margin` o `padding`.

Hay varias formas de solucionarlo:

- Eliminar los bordes y reducir los porcentajes manualmente hasta que quepan en el 100% del padre.
- Entender la propiedad `box-sizing` y cambiar el modo en el que se gestiona el modelo de cajas.
- `Opción ideal`: Utilizar un sistema moderno como Flexbox o Grid.


#### Tamaños máximos y mínimos

Si buscamos un cierto grado de control aún mayor, una opción recomendable sería recurrir a las propiedades max-width y min-width, con las que podemos indicar el ancho de un elemento como máximo y el ancho de un elemento como mínimo respectivamente, consiguiendo así garantizar cierto grado de control del diseño.

```css
.picture {
  min-height: 200px;    /* Por defecto, height es 0 */
  background: grey;     /* Simplemente, para verlo visualmente */

  max-width: 1024px;
  min-width: 800px;
}
```

En este caso, el elemento tiene un tamaño máximo de 1024px, y un tamaño mínimo de 800px, por lo que si ajustamos el ancho de la ventana del navegador, dicho elemento iría variando en un rango de 800 a 1024 píxeles, y nunca saldría de estos rangos.

Con las imágenes, videos y contenidos multimedia, podemos hacer lo mismo, consiguiendo así que las imágenes se escalen y adapten al formato especificado o incluso al tamaño de pantalla de los diferentes dispositivos utilizados:


```css
img,
video,
object,
embed {
  max-width: 100%;
  height: auto;
}
```

#### El viewport del navegador

En muchos casos puede que oigas hablar del viewport del navegador. Esa palabra hace referencia a la región visible del navegador, o sea, la parte de la página que está visualizándose actualmente en el navegador. Los usuarios podemos redimensionar la ventana del navegador para reducir el tamaño del viewport y simular que se trata de una pantalla y dispositivo más pequeño.

Si queremos editar ciertos comportamientos del viewport del navegador, podemos editar el documento HTML para especificar el siguiente campo meta, antes de la parte del `</head>`:

```html
<meta name="viewport" content="initial-scale=1, width=device-width">
```

Las propiedades initial-scale , minimum-scale y maximum-scale permiten valores desde el 0.1 al 10 , aunque ciertos valores se traducen automáticamente a ciertos números determinados:

- yes = 1
- no = 0.1
- device-width = 10
- device-height = 10

![](https://lenguajecss.com/css/responsive-web-design/media-queries/device-width.png)

### Media Queries

Las media queries son reglas en CSS que permiten aplicar estilos específicos solo si se cumplen ciertas condiciones, como el tipo de dispositivo o navegador. Funcionan como condicionales de diseño, aplicando diferentes estilos según el entorno en que se visualiza la página.

#### La regla @media

Las reglas media queries (abreviadas como MQ) se indican en el código mediante la regla `@media,` indicando la condición en cuestión entre paréntesis. La sintaxis sería la siguiente:


| Regla                                 | Descripción                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| @media (<condición>)                 | Si se cumple la condición, se aplican los estilos de su interior.          |
| @media not (<condición>)             | Si no se cumple la condición, se aplican los estilos de su interior.       |
| @media only (<condición>)            | Si se cumple la condición y es un navegador moderno, se aplican los estilos.|
| @media (<condición>) and (<condición>) | Si se cumplen ambas condiciones, se aplican los estilos.                  |


Observa que, de utilizar la palabra clave not antes de los paréntesis, invertimos la condición. Así pues, veamos un pequeño ejemplo donde escribimos las dos opciones anteriores, pero sin entrar en detalles aún en la condición:


```css
@media (*condición*) {
  .container {
    background: green;
  }
}

@media not (*condición*) {
  .container {
    background: red;
  }
}
```

En el ejemplo anterior, si se cumple la condición establecida, se aplicará un color verde. Sin embargo, si no se cumple, se aplicará un color rojo. Recuerda que es similar al funcionamiento de un `if` / `else` en programación.


>**Nota:** No olvides que al escribir una regla `@media` podrías estar sobreeescribiendo los estilos CSS en otro fragmento posterior. Una buena forma de empezar a escribir MQ sería escribir las reglas `@media` siempre al final


Si lo deseas, es posible establecer múltiples condiciones en las reglas `@media`. De esta forma, se pueden conseguir situaciones mucho más específicas y flexibles. Ten mucho cuidado si aplicas el not en las condiciones, no sea que niegues de forma incorrecta los casos deseados:


```css
@media (*condición*) and (*condición) {
  .container {
    background: orangered;
  }
}
```

#### Condiciones de Media Queries (range syntax)

Aunque existen otras formas, hoy en día la forma preferida de escribir Media Queries es utilizando la modalidad de rangos de condiciones (Media Query Range Syntax), mucho más versátiles que las sintaxis anteriores, y mucho menos tediosas.

Para ello, vamos a escribir las condiciones utilizando operadores de comparación como <, <=, > o >=:


```html
<div class="container">
  <p>Redimensiona el navegador o mueve abajo a la derecha.</p>
  <ul>
    <li>Dispositivos <= 550px -> Lila</li>
    <li>Dispositivos entre 551px y 749px -> Gris</li>
    <li>Dispositivos >= 750px -> Verde</li>
  </ul>
  <p>¡No te olvides de seguir a Manz en sus redes sociales!</p>
</div>
```


```css
.container {
  background: var(--color, grey);
  min-height: 200px;
  padding: 1rem 2rem;
}

@media (width <= 550px) {
  .container {
    --color: indigo;
  }
}

@media (width >= 750px) {
  .container {
    --color: green;
  }
}
```

![](../img/responsive%20design%201.png)


Ahora, hagamos una pequeña variación del CSS anterior, y aprovechemos el CSS Nesting nativo y la anidación de reglas @media:


```css
.container {
  background: var(--color, grey);
  min-height: 200px;
  padding: 1rem 2rem;

  @media (width <= 550px) { --color: indigo; }
  @media (width >= 750px) { --color: green; }
}
```

Ten en cuenta que con la sintaxis de rangos también puedes hacer condiciones múltiples de este estilo, en el que el código CSS se aplica sólo si el navegador tiene un ancho de pantalla entre 400px y 800px:


```css
@media (400px <= width <= 800px) {
  /* Código CSS */
}
```

#### Tipos de medios

En algunas ocasiones, queremos indicar que las reglas @media sólo se pongan en funcionamiento en determinados tipos de dispositivos. Son los llamados tipos de medios, que pueden utilizarse en las condiciones de los media queries. Existen los siguientes:


| Tipo de medio | Significado                                                                 |
|----------------|-----------------------------------------------------------------------------|
| all            | Todos los dispositivos o medios. El que se utiliza por defecto.            |
| screen         | Monitores o pantallas de ordenador. Es el más común.                       |
| print          | Documentos de medios impresos o pantallas de previsualización de impresión.|
| speech         | Lectores de texto para invidentes (Antes aural, el cuál ya está obsoleto). |


Estos tipos de medios se pueden indicar como una condición más, de modo que podría quedar de la siguiente forma:


```css
/* Pantallas menores de 600px */
@media screen and (width <= 600px) {
  /* ... */
}

/* Previsualizaciones y formatos de impresión */
@media print {
  /* ... */
}
```

### Media Features

Hasta ahora, sólo hemos utilizado width como condición para los media queries, sin embargo, existe una amplia gama de características o features que podemos utilizar en nuestras condiciones para aplicar un estilo si se cumplen o se dejan de cumplir.

#### Tamaño o proporción de aspecto

Al igual que utilizamos width, también podemos utilizar otros valores que determinan capacidades del dispositivo. Por ejemplo, podemos utilizar los siguientes:


| Característica   | Valores | ¿Cuándo se aplica?                                                      |
|------------------|---------|---------------------------------------------------------------------------|
| width            | `size` | Si el dispositivo tiene un tamaño de ancho determinado.                  |
| height           | `size` | Si el dispositivo tiene un tamaño de alto determinado.                   |
| aspect-ratio     | `number` \ `number` | Si el dispositivo encaja con la proporción de aspecto indicada.     |


Observa que tanto width, height como aspect-ratio tienen valores numéricos con los que puede utilizarse los operadores <, >, <=, >=. La proporción de aspecto es un valor numérico, pero que también puede indicarse en forma de fracción.


```html
<div class="container">
  <p>¡Sígueme! ¡Estoy en Twitch de Martes a Jueves!</p>
</div>
```

```css
@media (aspect-ratio <= 6/2) {
  .container {
    background: red;
    color: white;
  }
}
```

#### Orientación del viewport

Mediante la feature orientation podemos aplicar estilos dependiendo de la orientación del viewport (región visible) del navegador del usuario. Ten en cuenta que orientación no se refiere a la orientación de la pantalla, sino a la orientación del viewport. En móviles, esto suele coincidir con la situación donde el usuario tiene el móvil en vertical (portrait) o en apaisado (landscape).

| Característica | Valores                | ¿Cuándo se aplica?                                             |
|----------------|------------------------|----------------------------------------------------------------|
| orientation    | landscape \| portrait  | Si el dispositivo está en posición vertical o apaisado.       |


Observa el siguiente ejemplo. En navegadores de escritorio, generalmente nos encontraremos con que el texto tiene estilo y aparece en fondo verde. En dispositivos móviles o tablets, dependerá indirectamente de la orientación del dispositivo.


```html
<div class="container">
  <p>¡Este mensaje aparecerá en verde si ha detectado
    modo <strong>landscape</strong> (apaisado)!
  </p>
</div>
```

```css
@media (orientation: landscape) {
  .container {
    background: green;
    color: white;
  }
}
```

#### Desbordamiento del contenido

El navegador es capaz de detectar que tipo de medio estás usando a través de la feature `overflow-block` y `overflow-inline`:


| Característica   | Valores                     | ¿Cuándo se aplica?                                                       |
|------------------|-----------------------------|---------------------------------------------------------------------------|
| overflow-block   | none \| scroll \| paged     | Si el dispositivo puede desbordar el contenido en su eje principal.      |
| overflow-inline  | none \| scroll              | Si el dispositivo puede desbordar el contenido en su eje secundario.     |

La feature `overflow-block` se refiere al eje principal (que en nuestro caso, suele ser eje Y).
La feature `overflow-inline` se refiere al eje secundario (que en nuestro caso, suele ser X).


- 1️⃣ `scroll`: Medio donde el usuario puede hacer scroll (móvil, tablet, desktop, etc...)
- 2️⃣ `paged:` Medio donde el usuario ve contenido paginado (ebook reader, impresión, etc...)
- 3️⃣ `none`: Medio que no cumple los criterios anteriores (plataformas publicitarias, etc...)

#### Modo de visualización

La feature `display-mode` nos permite aplicar estilo si el navegador se encuentra en una modalidad específica de las siguientes:

| Característica | Valores                                                  | ¿Cuándo se aplica?                                                           |
|----------------|----------------------------------------------------------|-------------------------------------------------------------------------------|
| display-mode   | fullscreen \| standalone \| browser \| minimal-ui \| picture-in-picture | Si el dispositivo está en alguno de estos modos especiales.           |


- 1️⃣ `fullscreen`: La página está en modo pantalla completa. Generalmente, ocurre al pulsar .
- 2️⃣ `standalone`: La página está en modo aplicación independiente nativa.
- 3️⃣ `minimal-ui`: Similar a standalone, pero con elementos mínimos de UI de navegación.
- 4️⃣ `browser`: La página está en el modo navegador tradicional.
- 5️⃣ `picture-in-picture`: La página está mostrando medios en una ventana flotante y siempre visible.


### Container Queries

Los media queries o regla @media son un mecanismo de CSS para dar estilo a elementos dependiendo de si se cumple una cierta condición, que generalmente tiene que ver con el tamaño, orientación o cierta característica de la página o dispositivo en el que nos encontramos. Es uno de los mecanismos principales del **responsive design**.

#### ¿Qué son los Container Queries?

Los CSS Container Queries son el mismo concepto de las Media Queries, pero en lugar de estar orientados a modificar los estilos dependiendo del tamaño de la página o dispositivo, lo hace dependiendo de un contenedor padre (o ancestro) específico. De esta forma, podemos cambiar el tamaño de ciertos elementos y hacer que tengan una forma o unos estilos concretos dependiendo del contexto donde se encuentren.

![](https://lenguajecss.com/css/responsive-web-design/css-container-queries/css-container-queries.png)


#### El contenedor

Para empezar, tenemos que determinar cuál será el elemento contenedor al que vamos a hacer referencia. En dicho elemento, necesitaremos establecer las siguientes propiedades, donde container-name es siempre obligatoria:


| Propiedad        | Valores                             | Descripción                                                                 |
|------------------|--------------------------------------|------------------------------------------------------------------------------|
| container-name   | none \| nombre del contenedor        | Establece un nombre de contenedor para poder hacer referencia a él.         |
| container-type   | normal \| size \| inline-size        | Establece el tipo de tamaño de contenedores (bloque, en línea, etc.).       |

La propiedad `container-name` le da un nombre de contenedor al elemento en el que nos encontramos. Sin este nombre no podremos hacer referencia luego, en la regla `@container`.


Por otro lado, la propiedad `container-type`, si la definimos, establecerá el tipo de tamaño que va a tener el contenedor en cuestión, donde puede ser `size` para elementos de tipo bloque, o `inline-size` para elementos de tipo en línea.


```css
.container {
  container-name: parent;
  container-type: inline-size;
}
```

#### Atajo: Propiedad `container`

Una forma de escribir menos código es utilizar la propiedad de atajo container, a la cuál le podemos indicar dos valores: el valor de la propiedad container-name y el valor de la propiedad container-type, siempre separadas por un /:


```css
.container {
  container: parent / inline-size;
}
```

#### La regla @container

Una vez tenemos nuestro contenedor definido, debemos establecer una regla @container que, de forma muy similar a las reglas @media va a establecer una condición dependiendo de un elemento contenedor específico.

Por ejemplo, en este ejemplo que tenemos a continuación, vamos a establecer nuestro elemento con clase .container con un elemento contenedor parent, y creamos una regla @container que afecta a los hijos del contenedor parent cuando, como máximo, tenga 500px de ancho:


```css
.container {
  container: parent;
}

@container parent (max-width: 550px) {
  .item {
    background: blue;
  }
}
```

Vamos ahora a aplicar este detalle a un ejemplo completo. Observa que la tarjeta aparece en formato horizontal. Sin embargo, si forzamos a reducir el ancho de la ventana, comprobaremos que el elemento reacciona al cambio y se muestra en versión vertical. Esto puede parecer lo mismo que un media query, pero realmente podemos hacer lo mismo reduciendo el tamaño de la tarjeta (esquina inferior-derecha), y también reacciona a su cambio de tamaño.

Esto ocurre porque hemos usado un Container Query en lugar de un Media Query:


```html
<p>Move from bottom-right corner</p>

<div class="container">
  <div class="item">
    <img src="https://manz.dev/apple-touch-icon.png" alt="ManzDev">
    <div class="data">
      <h1>Manz.dev</h1>
      <p>Página del canal de Twitch de ManzDev, donde se habla de Desarrollo web, front-end y se explican o crean proyectos variados utilizando tecnologías web como HTML, CSS y Javascript.</p>
    </div>
  </div>
</div>
```

```css
body {
  background: steelblue;
  height: 625px;
}

.container {
  container: card / inline-size;
  max-width: 1024px;
  min-width: 250px;
  overflow: hidden;
  resize: horizontal;
  border: 1px solid white;
  box-shadow: 4px 4px 10px #0005;
  background: white;
  color: black;

  & .item {
    display: flex;
    justify-content: center;
    align-items: center;
    background:
      linear-gradient(to right, transparent 180px, white 180px),
      linear-gradient(to bottom, #9146eb 50%, #ea17cf 50%);

    @container card (max-width: 550px) {
      flex-direction: column;
      background: linear-gradient(#9146eb, #ea17cf 180px, transparent 180px);
    }

    & img {
      position: relative;
      width: 180px;
      height: 180px;
    }

    & .data {
      margin: 1em;
    }
  }
}
```

![](../img/media%20container.png)


#### Unidades de contenedores

Cuando nos encontramos en el interior de una regla `@container` podemos utilizar ciertas unidades especiales como `cqw`, `cqh`, `cqi`, `cqb`, `cqmin` o `cqmax`. Básicamente, la idea es que si desconocemos el tamaño concreto del contenedor, podemos utilizar estas medidas para aplicar un porcentaje de su tamaño.

De esta forma, si utilizamos `50cqw`, significa que va a establecer un tamaño del 50% del ancho del contenedor. Funcionan de forma muy similar a las unidades `vw`, `vh`, `vmin` y `vmax`.

| Unidad   | Descripción                                                                 |
|----------|------------------------------------------------------------------------------|
| cqw      | Container Query Width. Porcentaje relativo al ancho del contenedor.         |
| cqh      | Container Query Height. Porcentaje relativo al alto del contenedor.         |
| cqi      | Container Query Inline Size. Porcentaje relativo al tamaño en línea.        |
| cqb      | Container Query Block Size. Porcentaje relativo al tamaño de bloque.        |
| cqmin    | Container Query Mínimo. Valor más pequeño entre `cqi` y `cqb`.              |
| cqmax    | Container Query Máximo. Valor más alto entre `cqi` y `cqb`.                 |


### Media querys mas usadas

📱 MÓVILES🔹 Teléfonos pequeños (hasta 480px)

```css
/* Clásica */
@media (max-width: 480px) {
  /* estilos para móviles pequeños */
}

/* Range syntax */
@media (width <= 480px) {
  /* estilos para móviles pequeños */
}
```

📱 MÓVILES🔹 Teléfonos estándar (hasta 576px)

```css
/* Clásica */
@media (max-width: 576px) {
  /* estilos para móviles estándar */
}

/* Range syntax */
@media (width <= 576px) {
  /* estilos para móviles estándar */
}
```

💊 TABLETS 🔹 Tablets en vertical (entre 577px y 768px)

```css
/* Clásica */
@media (min-width: 577px) and (max-width: 768px) {
  /* estilos para tablets en vertical */
}

/* Range syntax */
@media (577px <= width <= 768px) {
  /* estilos para tablets en vertical */
}
```

💊 TABLETS 🔹 Tablets en horizontal (entre 769px y 991px)

```css
/* Clásica */
@media (min-width: 769px) and (max-width: 991px) {
  /* estilos para tablets en horizontal */
}

/* Range syntax */
@media (769px <= width <= 991px) {
  /* estilos para tablets en horizontal */
}
```

💻 ESCRITORIOS 🔹 Escritorios estándar (entre 992px y 1200px)

```css
/* Clásica */
@media (min-width: 992px) and (max-width: 1200px) {
  /* estilos para escritorio estándar */
}

/* Range syntax */
@media (992px <= width <= 1200px) {
  /* estilos para escritorio estándar */
}
```

💻 ESCRITORIOS 🔹 Escritorios grandes (más de 1200px)

```css
/* Clásica */
@media (min-width: 1201px) {
  /* estilos para escritorios grandes */
}

/* Range syntax */
@media (width > 1200px) {
  /* estilos para escritorios grandes */
}
```

---
