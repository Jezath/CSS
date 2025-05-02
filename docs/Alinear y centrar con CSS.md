# Alinear y centrar con CSS

---

- [Centrar horizontalmente](#centrar-horizontalmente)
- [Centrar verticalmente](#centrar-verticalmente)
- [Multicolumnas CSS](#multicolumnas-css)
- [Separacion de columnas](#separacion-de-columnas)
- [Distribucion entre columnas](#distribucion-entre-columnas)

---

Antes de comenzar a aprender a utilizar mecanismos potentes de CSS como Flex o Grid, es conveniente conocer las bases y como podemos centrar o alinear elementos con CSS, sin necesitar utilizar dichos mecanismos.

### Resetear los estilos por defecto

En primer lugar, vamos a resetear los estilos por defecto. Los navegadores tienen ciertos estilos por defecto, como por ejemplo ese margen en el `<body>` que hace que el recuadro no esté pegado a los bordes.

Podemos utilizar un reset CSS, sin embargo, para simplificar el ejemplo, vamos a aplicar un margin: 0 al `<body>`. También le pondremos un fondo de color negro:

```css
body {
  margin: 0;
  background: black;
}
```

### Centrar horizontalmente

Para centrar horizontalmente un elemento sin Flex ni Grid, necesitamos cumplir algunas condiciones:

- 1️⃣ El elemento debe tener un `display: block` (no sirve `inline,` `inline-block` o derivados)
- 2️⃣ El elemento debe tener un tamaño de ancho.
Por lo tanto, vamos a darle un tamaño al .container de 300x250 y se mostrará a la izquierda de la página:


```html
<div class="container">ManzDev, tu streamer de CSS de confianza</div>
```

```css
.container {
  width: 300px;
  min-height: 250px;
  background: indigo;
  color: white;
  padding: 2rem;
}
```

![](../img/centrar%20horizontal%201.png)

Observa que utilizado `min-height` en lugar de `height`. Con esto no obligamos a que sea siempre ese alto, sino que en el caso de tener mucha información, se pueda hacer más grande.

Ahora vamos a aplicar un `margin` al elemento. Observa todo el espacio sobrante a su derecha. Al aplicar un `margin: auto` lo que hacemos es decirle que ese espacio restante lo divida en dos: el primero lo colocará a la izquierda, y el segundo lo colocará a la derecha, y como efecto «colateral» el elemento se centrará en pantalla:

```css
.container {
  width: 300px;
  min-height: 250px;
  margin: auto;
  background: indigo;
  color: white;
  padding: 2rem;
}
```

![](../img/centrar%20horizontal%202.png)


### Centrar verticalmente

Vamos ahora con el otro eje (vertical), que suele ser el más problemático, ya que se suele confundir con varios detalles adicionales. Recuerda que un documento HTML siempre tiene una etiqueta `<html>` que contiene una etiqueta `<body>`, y aunque sólo se le suele dar estilo al `<body>`, también se le podría dar al `<html>`.

En este nuevo ejemplo, ahora tengo pintado de color negro el fondo de la etiqueta `<body>` y de color rosa el fondo de la etiqueta `<html>`:


```html
<div class="container">ManzDev, tu streamer de CSS de confianza</div>
```

```css
html {
  background: hotpink;
}

body {
  margin: 0;
  background: black;
}

.container {
  width: 300px;
  min-height: 250px;
  margin: auto;
  background: indigo;
  color: white;
  padding: 2rem;
}
```

![](../img/centrar%20verticalemente%201.png)

Como puedes ver, si intento centrar el elemento .container verticalmente, ya lo tendré centrado, porque `<body>`, su padre inmediato, no tiene más espacio de alto como para poder centrarlo. Lo que suele ocurrir es que siempre tenemos el mismo color en el `<body>` y en el `<html>`, por lo que no solemos darnos cuenta de este detalle.

Una sencilla forma de solucionarlo, es seguir estos 3 sencillos pasos:

- 1️⃣ Le damos un alto de 100vh a `<html>`. Ocupará exactamente el tamaño de alto de pantalla.
- 2️⃣ Le damos un alto de 100% a `<body>`. Tomará el alto del padre, o sea, de `<html>`.
- 3️⃣ Asegurate de tener reseteado el margen de `<body>` con `margin: 0`.


```css
html {
  background: hotpink;
  height: 100vh;
}

body {
  margin: 0;
  height: 100%;
  background: black;
}

.container {
  width: 300px;
  min-height: 250px;
  margin: auto;
  background: indigo;
  color: white;
  padding: 2rem;
}
```

![](../img/centrar%20verticalemente%202.png)

De esta forma ya hemos forzado a que la página tenga el alto del navegador, y por lo tanto haya espacio para centrarlo. Recuerda que he dejado el color de fondo diferente en `<html>` y `<body>` para que diferencies hasta donde llega cada uno, si decides modificar el ejemplo.

#### Propiedad `align-content` en block

Aunque la propiedad `align-content` aparece por primera vez en contextos de `Flex` y `Grid`, recientemente se ha añadido la posibilidad de utilizarla en elementos con `display: block`, por lo que podemos utilizarla en este caso para centrar verticalmente de forma limpia.

Observa que al ejemplo anterior, hemos añadido al body un `align-content: center`, centrando así el elemento verticalmente.


```html
<div class="container">ManzDev, tu streamer de CSS de confianza</div>
```

```css
html {
  height: 100vh;
}

body {
  margin: 0;
  height: 100%;
  background: black;
  align-content: center;
}

.container {
  width: 300px;
  min-height: 250px;
  margin: auto;
  background: indigo;
  color: white;
  padding: 2rem;
}
```

![](../img/centrar%20verticalemente%203.png)

¡Ya tenemos nuestro elemento centrado verticalmente, con sólo una línea de CSS! La propiedad align-content como veremos en los próximos temas, puede tomar varios valores, pero de momento vamos a centrarnos en estos tres:

- `start`:	Alinea el elemento al inicio respecto a su contenedor padre.
- `center`:	Centra el elemento respecto a su contenedor padre.
- `end`:	Alinea el elemento al final respecto a su contenedor padre.

#### Centrar contenido

Por último, nos queda el contenido del elemento. Observa que el texto del interior del elemento no está aún centrado. Esto ocurre porque lo que hemos hecho hasta ahora ha sido sólo para alinear el elemento respecto a su contenedor padre.

Si queremos hacer lo mismo con su contenido, estaríamos alineando su contenido (hijos) sobre su contenedor padre, el propio elemento. Para hacer esto, la forma más sencilla es aplicar en .container los siguientes estilos:

- 1️⃣ Utiliza `text-align: center` para centrar el contenido horizontalmente.
- 2️⃣ Utiliza `align-content: center` para centrar verticalmente.


```html
<div class="container">ManzDev, tu streamer de CSS de confianza</div>
```

```css
html {
  height: 100vh;
}

body {
  margin: 0;
  height: 100%;
  background: black;
  align-content: center;
}

.container {
  width: 300px;
  min-height: 250px;
  margin: auto;
  background: indigo;
  color: white;
  padding: 2rem;
  text-align: center;
  align-content: center;
}
```

![](../img/centrar%20verticalemente%204.png)


### Multicolumnas CSS

El esquema de layouts en columnas es un antiguo sistema de maquetación de CSS en el que se puede dividir un texto o contenido en un número de columnas concreto, haciendo la tarea de división en columnas de forma automática por parte del navegador.

#### Creando multicolumnas CSS

Para entender bien este sistema de maquetación, vamos a traer a nuestra mente un ejemplo donde se ve muy claro: los antiguos periódicos o panfletos de prensa escrita. Estos medios de prensa utilizaban un esquema de varias columnas para separar separar la información, aprovechar el espacio y crear múltiples columnas con contenido.

Justo esta idea es la que trae el sistema de columnas CSS a la web, utilizando principalmente las propiedades `column-count` y `column-width` que vemos en la siguiente tabla:


| Propiedad     | Descripción                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `column-count ` | Indica el número de columnas que queremos establecer. Por defecto, auto.     |
| `column-width`  | Indica el tamaño ideal de cada columna. Por defecto, auto.                  |
| `columns`      | Propiedad de atajo de las dos anteriores: count y width.                     |


```html
<div class="container">
  <p>
    Hola a todos. Esto es un pequeño ejemplo donde podremos observar como funciona
    el sistema de multicolumnas de CSS. Este contenido se basa en un párrafo con
    información que será separado en varias columnas.
  </p>
  <h2>Más información</h2>
  <p>
    A lo largo del artículo veremos sus diferentes características y propiedades,
    y como podemos utilizarlo.
  </p>
  <p>
    En los streams de <strong>ManzDev</strong> puedes echar un vistazo a estas y
    otras cosas relacionadas con HTML, CSS y Javascript.
  </p>
</div>
```

```css
.container {
  width: 800px;
  column-count: 3;
  column-width: 300px;
}
```

![](../img/column%201.png)

Comprobaremos que a pesar de haber indicado **3 columnas**, al haberle dado un tamaño ideal de **300px** a cada columna, que no cabrá en los **800px** del contenedor, establece 2 columnas. Si reducimos el `column-width` a **200px**, veremos que si crea las **3 columnas**.

![](https://lenguajecss.com/css/layout/column-css/column-count.webp)

#### Atajo: Propiedad `columns`

Mediante la propiedad `columns` podemos establecer las dos propiedades anteriores de una sola vez. El siguiente fragmento de código sería equivalente al ejemplo anterior:


```css
.container {
  width: 800px;
  columns: 3 300px;
}
```

### Separacion de columnas

Retomando el ejemplo anterior, vamos ahora a intentar establecer un espacio entre las columnas. Para ello, tenemos a nuestra disposición la propiedad `column-gap,` que funciona de forma muy parecida a `flex` o `grid`. Con ella establecemos unos «huecos» entre columnas.

Pero a parte de esta propiedad tenemos algunas más con el prefijo `column-rule`:

| Propiedad            | Descripción                                                                   |
|----------------------|-------------------------------------------------------------------------------|
| `column-gap`           | Establece un hueco o espacio entre columnas con el tamaño indicado.           |
| `column-rule-width`    | Establece el tamaño de la línea divisoria entre columnas.                     |
| `column-rule-style `   | Establece el estilo de la línea divisoria entre columnas.                     |
| `column-rule-color`    | Establece el grosor de la línea divisoria entre columnas.                     |
| `column-rule `         | Propiedad de atajo de las tres anteriores.                                    |


Las reglas de columnas son unas líneas divisorias que podemos establecer entre columnas para que se vea más claramente la división creada. Funciona de forma muy similar a los bordes CSS, ya que también podemos establecer color, estilo y grosor, incluso con su propiedad `column-rule` de atajo.

En el caso de indicar `column-rule` y `column-gap` juntas, observa que simplemente se colapsan en el mismo espacio, por lo que es ideal para añadir una separación si con la regla no es suficiente:

![](https://lenguajecss.com/css/layout/column-css/column-gap.webp)


### Distribucion entre columnas

Tenemos algunas propiedades más para distribuir el texto entre columnas con diferentes matices. Las propiedades son las siguientes:


| Propiedad     | Descripción                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `column-span`   | Indica si debe ocupar sólo una columna o expandirse por todas. Por defecto, `none`. |
| `column-fill `  | Balancea el texto entre las columnas o rellena hasta que se agota. Por defecto, `balance`. |

La propiedad `column-span` es muy interesante. Esta propiedad, puede indicarse a elementos hijos como, por ejemplo, titulares, para indicar si deben ocupar sólo su espacio dentro de la columna que le toque, o si debe extenderse a lo largo de todas las columnas.

Observa que en nuestro ejemplo anterior hay un `<h2>`. Vamos a cambiarle el estilo y a indicarle que queremos que se entienda por todas las columnas:


```html
<div class="container">
  <p>
    Hola a todos. Esto es un pequeño ejemplo donde podremos observar como funciona
    el sistema de multicolumnas de CSS. Este contenido se basa en un párrafo con
    información que será separado en varias columnas.
  </p>
  <h2>Más información</h2>
  <p>
    A lo largo del artículo veremos sus diferentes características y propiedades,
    y como podemos utilizarlo.
  </p>
  <p>
    En los streams de <strong>ManzDev</strong> puedes echar un vistazo a estas y
    otras cosas relacionadas con HTML, CSS y Javascript.
  </p>
</div>
```

```css
.container {
  width: 800px;
  columns: 3 200px;
}

.container h2 {
  background: steelblue;
  column-span: all;
}
```

![](../img/column%202.png)

Con la propiedad `column-span `establecida a `all`, en lugar de que el `<h2>` ocupe sólo su columna, se establecerá que se extienda por encima, a lo largo de todas las columnas.

Por otro lado, la propiedad `column-fill` nos permite balancear y distribuir el texto de forma equivalente entre las diferentes columnas. Se aplica al padre y se puede indicar el valor `balance` (en algunos casos sólo balancea la última columna) o `balance-all` (balancea siempre todas las columnas). Sin embargo, también podemos indicar el valor `auto`, que no balancea, y distribuye el texto desde la primera columna hasta que se agote:


```css
.container {
  height: 250px;
  column-fill: auto;
}
```

En este ejemplo, fijamos el tamaño de alto del contenedor para forzar a que podamos ver los resultados, y le aplicamos el valor `column-fill` a `auto`. Comprueba la diferencia de este valor y los valores `balance` y `balance-all` (casi siempre suelen ser los mismos).

En general, el soporte de `column-fill` es bueno en navegadores, sin embargo, cuidado con el soporte del valor `balance-all` que aún está en fase experimental.

---

Regresar al [README](../README.md)