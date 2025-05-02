# Position 

---

- [Coordenadas de posicion](#coordenadas-de-posicion)
- [Profundidad](#profundidad)
- [Contexto de apilamiento](#contexto-de-apilamiento)
- [Tipos de position](#tipos-de-position)
  - [Propiedad position: static](#propiedad-position-static)
  - [Propiedad position: relative](#propiedad-position-relative)
  - [Propiedad position: absolute](#propiedad-position-absolute)
  - [Propiedad position: fixed](#propiedad-position-fixed)
  - [Propiedad position: sticky](#propiedad-position-sticky)

---

### La propiedad `position`

La propiedad `position` es una propiedad CSS que se puede utilizar para modificar la posición donde aparecerá un elemento. Se le pueden indicar los siguientes valores:


| Valor      | Significado                                                                 |
|------------|-----------------------------------------------------------------------------|
| `static`   | Posicionamiento estático. Utiliza el orden natural de los elementos HTML.   |
| `relative` | Posicionamiento relativo. Los elementos se mueven ligeramente en base a su posición estática. |
| `absolute` | Posicionamiento absoluto. Los elementos se colocan en base a un contenedor padre. |
| `fixed`    | Posicionamiento fijo. Idem al absoluto, pero aunque hagamos scroll no se mueve. |
| `sticky`   | Posicionamiento fijo con desplazamiento («pegajoso»). Muy usado para pegar elementos a una zona. |


> **Nota:** Por defecto el navegador posiciona los elementos con la propiedad `position: static`.

### Coordenadas de posicion

Si utilizamos un modo de posicionamiento diferente al estático (`absolute`, `fixed`, `sticky` o `relative`), podemos utilizar una serie de propiedades para modificar la posición de un elemento. Es importante tener en cuenta que dichas propiedades solo tendrán efecto si no tenemos la propiedad position establecida a `static`.

Estas propiedades son las siguientes:


| Propiedad | Valor | Significado                                                                 |
|-----------|-------|-----------------------------------------------------------------------------|
| `top`     | auto \ `size`  | Empuja el elemento una distancia desde la parte superior hacia el inferior. |
| `bottom`  | auto \ `size`  | Empuja el elemento una distancia desde la parte inferior hacia la superior. |
| `left`    | auto \ `size`  | Empuja el elemento una distancia desde la parte izquierda hacia la derecha. |
| `right`   | auto \ `size`  | Empuja el elemento una distancia desde la parte derecha hacia la izquierda. |
| `inset`   | auto \ `size`  | Propiedad de atajo para utilizar todas las anteriores.                      |


Estas propiedades, lo único que hacen es colocar o fijar el elemento en el punto concreto indicado, de modo que si indicas `left: 0` significa que quieres que el elemento esté colocado `0` píxeles desde la izquierda. Puede contener valores negativos, invirtiendo la dirección.

![](https://usingu.cdn3.cafe24.com/blog/getboundingclientrect.jpg)

![](../img/position%201.png)

### Atajo: Propiedad `inset`

La propiedad `inset` es una propiedad de atajo para las cuatro anteriores: top, right, bottom, left. Podemos utilizarla indicando diferentes parámetros:


- **1 parámetro:** Se aplica el mismo valor a todos: `top, right, bottom y left`.
- **2 parámetros:** Primer valor a `top` y ``bottom``, y el segundo a `left` y `right`.
- **3 parámetros:** Primer valor a `top`, el segundo a `right` y `left` y el tercero a ``bottom``.
- **4 parámetros:** Primer valor a `top`, el segundo a `right`, el tercero a ``bottom`` y el cuarto a `left`.

```css
.elemento {
  /* 
  top: 10px;
  right: 20px;
  bottom: 30px;
  left: 40px; 
  */

  /* atajo: */
  inset: 10px 20px 30px 40px;
}
```

### Profundidad

Es interesante conocer también la existencia de la propiedad `z-index`, que es una forma de indicar una distancia en el eje `Z`, es decir, en el eje de profundidad. CSS establece un nivel de profundidad en el que está un elemento sobre los demás. De esta forma, podemos hacer que un elemento se coloque encima o debajo de otro.

![](https://lenguajecss.com/css/posicionamiento/position/z-index.png)

Ejemplos de z-index:

![](https://www.programiz.com/sites/tutorial2program/files/css-z-index-example.png)


### Contexto de apilamiento

Al añadir un posicionamiento absoluto a un elemento, se dice que el elemento entra en un contexto de apilamiento diferente, ya que este ha sido posicionado en un espacio tridimensional, por lo que no interactua de la misma forma respecto a otros elementos.

En CSS existen múltiples formas de crear contextos de apilamiento, a parte de cuando posicionas de forma absoluta un elemento:

- A los hijos (directos) de un elemento `display: flex` o `display: grid` con `z-index` especificado.
- A elementos con un `opacity` diferente de `1` y sus elementos descendientes.
- A elementos con un `transform`, `filter`, `clip-path`, `mask` (o similares) esteblecido.
- A elementos con un `will-change` o un `contain` establecido.
- A ciertos elementos con un `container-type` o un `contain` establecido.
- A elementos con un `mix-blend-mode` establecido.
- A elementos con un `isolation` establecido a `isolate`.

Ejemplo de Contexto de apilamiento:

Tenemos los siguientes elementos apilados unos encima de otro.

```html
<section>
  <div>1</div>
  <div>2</div>
  <div>3</div>
</section>
```

```css
div {
  border: 1px solid;
  opacity: .9;
  width: 200px;
  height: 200px;
  background: #09f;
  margin-left: 50px;
  margin-top: -100px;
  box-shadow: 0 0 5px #000000dd;
}

div:first-child {
  background: yellow;
}

div:last-child {
  background: red;
}
```

![](../img/contexto%20de%20apilamiento%201.png)

Ahora queremos poner algunos elementos que estan visualmente atras de otros al frente.

Tenemos que crear el contexto de apilamiento, para ello usamos el `position: relative`.

```css
div {
  border: 1px solid;
  opacity: .9;
  width: 200px;
  height: 200px;
  background: #09f;
  margin-left: 50px;
  margin-top: -100px;
  box-shadow: 0 0 5px #000000dd;
  
  /* creamos el contexto de apilamiento con la propiedda position */
  position: relative;
}

div:first-child {
  background: yellow;

  z-index: 2; /* usamos el z-index para indicar la distancia entre elementos 0 -> num */
  left: 30px; /* movemos un poco el elemento para poder ver mejor a los demás */
}

div:last-child {
  background: red;
}
```

Usamos el `z-index` en el elemento hijo `div` que queremos mover al frente para indicar la distancia entre elementos 0 -> num.

![](../img/contexto%20de%20apilamiento%202.png)


> **Importante:** No se debe abusar del uso del `z-index`, sin embargo en el ejemplo anterior esta propiedad tiene que ir en los elementos hijos.


### Tipos de `position`

![](https://miro.medium.com/v2/resize:fit:1400/1*x5xm9DVS6QouWCAeII9w8A.png)


#### Propiedad `position: static`

Si no alteramos la propiedad `position`, es la forma por defecto como se colocan automáticamente los elementos en el navegador.
Como ya vimos anteriormente la colocación de los elementos depende del flujo de los elementos por su tipo de display, es decir los tipos `block` se colocan unos debajo de otros, y los tipos `inline` se colocan al lado de otros.


#### Propiedad `position: relative`

Al utilizar la propiedad `position: relative`, en este modo, los elementos se colocan exactamente igual que en el posicionamiento estático (permanecen en la misma posición), pero dependiendo del valor de las propiedades `top, bottom, left, right` o `inset`, variaremos ligeramente la posición del elemento.

Veamos un primer ejemplo sencillo:

```html
<section class="parent">

  <div class="a"></div>

  <div class="b"></div>

</section>
```

```css
body {
  background: rgb(219, 228, 235);
}

/* elemento padre */
.parent {
  border: 5px solid #b9b8b8;
  width: 250px;
  height: 250px;
  box-sizing: border-box;

}

/* elementos hijos, cuadros de colores */
.a {
  width: 100px;
  height: 100px;
  background: darkred;
}

.b { /* elemento b se coloca por encima del elemento a */
  width: 100px;
  height: 100px;
  background: indigo;

  position: relative;
  top: -50px;
  left: 50px;
}
```

![](../img/position%20relative%201.png)


Si queremos que el elemento `a` (rojo) se coloca encima del elemento `b` (morado), primero tenemos que colocarle un `position: relative` y luego un `z-index`

```css
.a {
  width: 100px;
  height: 100px;
  background: darkred;

  position: relative;
  z-index: 2;
}

.b {
  width: 100px;
  height: 100px;
  background: indigo;

  position: relative;
  top: -50px;
  left: 50px;
}
```

![](../img/position%20relative%202.png)

> **Importante:** Usamos `position: relative` en un elemento padre para crear un punto relativo y hacer que los elementos hijos lo tomen como referencia y poder posicionarse dentro del padre.



#### Propiedad `position: absolute`

Para entender como funciona el posicionamiento absoluto, hay que entender lo que hace el navegador. Antes de explicarlo, mostremos algunas importantes pautas previas:

- El elemento rojo es el elemento a posicionar, debe tener `position: absolute`.
- Utilizaremos propiedades de coordenadas (`top, left, right, bottom ` o `inset`) para mover el elemento.
- El elemento con borde amarillo es el marco de referencia, que no debe tener `position: static`.


![](https://lenguajecss.com/css/posicionamiento/position-absolute/position-absolute.png)


Los elementos con `position: absolute` van buscando en todos sus padres (elementos HTML) cual de ellos tienen un `position: relative` al cual tomar como referecia. Si no encuentra tomará al elemento `<body>`, que sería el último y el que utilizaría como marco de referencia.


Veamos como funciona el `position: absolute` con un ejemplo:

1. Colocamos un `position: absolute` al elemento hijo `.container`.
2. Colocamos sus coordenadas `top: 0` y `left: 0`.

```html
<section class="parent">

  <div class="container"></div>

</section>
```

```css
.parent {
  border: 5px solid #b9b8b8;
  width: 250px;
  height: 250px;
  box-sizing: border-box;
}

.container {
  background: #09f;
  width: 100px;
  height: 100px;

  position: absolute;
  top: 0;
  left: 0;
}
```

Como vemos el elemento interno `.container` se posiciona en la esquina de la pantalla, esto se debe a lo anteriormente mencianado, ninguno de sus padre tiene un `position: relative` por lo que se posiciona respecto al elemento `<body>`.

![](../img/position%20absolute%201.png)

Para arreglar esto simplemente le colocamos un `position: relative` al elemento padre `.parent`.

```css
.parent {
  border: 5px solid #b9b8b8;
  width: 250px;
  height: 250px;
  box-sizing: border-box;

  position: relative;
}

.container {
  background: #09f;
  width: 100px;
  height: 100px;

  position: absolute;
  top: 0;
  left: 0;
}
```

![](../img/position%20absolute%202.png)


#### Forma de centrar un elemento con `position`

La siguiente forma para centrar un elemento **NO** es la más recomendada porque existe otras formas mejores que ya veremos más adelante, sin embargo esta opción puede ser interesante para centrar modales.


```html
<section class="parent">

  <div class="container"></div>

</section>
```

```css
.parent {
  border: 5px solid #b9b8b8;
  width: 250px;
  height: 250px;
  box-sizing: border-box;

  position: relative;
}

.container {
  background: #09f;
  width: 100px;
  height: 100px;

  position: absolute;
  /* top: 0;
  right: 0;
  bottom: 0;
  left: 0; */
  inset: 0; /* <-- atajo */
  margin: auto;
}
```

![](../img/position%20absolute%203.png)


#### Propiedad `position: fixed`

El `position: fixed` es parecido al absolute con la diferencia que su padre **NO** necesita un `position`, en cambio toma como referencia el **viewport**, es decir la pantalla o vista del navegador.

Veamos un ejemplo para saber su comportamiento:

1. Duplicamos los elementos padres `.parent` para que haya un `scroll` en la pantalla.
2. Colocamos el elemento hijo `.container` a la esquina de la pantalla con `top: 0 `y `right: 0`;


```html
<section class="parent">

  <div class="container"></div>

</section>

<section class="parent">
</section>

<section class="parent">
</section>

<section class="parent">
</section>

<section class="parent">
</section>
```

```css
.parent {
  border: 5px solid #b9b8b8;
  width: 250px;
  height: 250px;
  margin-bottom: 50px;
  box-sizing: border-box;
}

.container {
  background: #09f;
  width: 100px;
  height: 100px;

  position: fixed;
  top: 0;
  right: 0;
}
```

![](../img/position%20fixed.png)

Como vemos aunque hagamos `scroll` el elemento `.container` se queda fijo en la esquina de la patalla.

Este tipo de posicionamiento es interesante en los menús flotantes o los botones de volver arriba.


#### Propiedad `position: sticky`

Es el posicionamiento más interesante de todos. Toma como referencia al elemento padre con `position: relative` incluso si hacemos scroll hacia abajo se queda pegado hasta donde llegue el borde de su contenedor padre.

Veamos un ejemplo para ver su funcionamiento:

1. Le damos más `height` al elemento `.parent` para observar como se mueve el elemento hijo con el scroll.
2. Como mencionamos elemento `.parent` tiene que ser `position: relative`.
3. Posicionamos el elemento hijo `.container` en la esquina superior con `top: 0 `y `right: 0`


```html
<section class="parent">

  <div class="container"></div>

</section>

<section class="parent">

  <div class="container"></div>

</section>
...
```

```css
.parent {
  border: 5px solid #b9b8b8;
  width: 250px;
  height: 550px;
  box-sizing: border-box;

  position: relative;
}

.container {
  background: #09f;
  width: 100px;
  height: 100px;

  position: sticky;
  top: 0;
  right: 0;
}
```

![](../img/position%20sticky%201.png)

Si hacemos scroll el elemento `.container` se mueve hasta que llegue al borde del elemento `.parent`.

Este posicionamiento se ve muy bonito en los headers con animaciones de scroll.

Veamos otro ejemplo:

```html
<div class="parent">
  <p>
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
  </p>
  <div class="element">Texto posicionado</div>
  <p>
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
    Esto es un ejemplo con contenido de texto para crear scroll.
  </p>
</div>
```

```css
body {
  height: 250px;
}

.parent {
  font-size: 3rem;
  background: grey;
}

.element {
  background: black;
  color: white;
  font-size: 1.5rem;
  padding: 25px;
  width: 200px;

  position: sticky;
  right: 0;
  top: 0;
}
```

Observa que en este caso, el elemento no se posiciona desde el principio, sino que mantiene su lugar en el HTML.

![](../img/position%20sticky%202.png)

En ese momento, desde que el elemento llega a la parte superior y va a desaparecer debido al scroll, el elemento «se pega» a la parte superior y permanece «sticky», acompañándonos hasta el final de la página o que volvamos a subir el umbral donde lo encontramos, donde volvería a su ubicación original y dejaría de seguirnos.

![](../img/position%20sticky%203.png)

---

Regresar al [README](../README.md)