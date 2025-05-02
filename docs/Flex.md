# Flex

---

- [Propiedad flex](#propiedad-flex)
- [Propiedad flex-direction](#propiedad-flex-direction)
- [Contenedor flex multilinea](#contenedor-flex-multilinea)
- [Gap](#gap)
- [Elementos flexibles](#elementos-flexibles)
- [Alinear y centrar con Flex CSS](#alinear-y-centrar-con-flex-css)
- [Alineacion multilinea](#alineacion-multilinea)
- [Alineaciones especificas](#alineaciones-especificas)
  
---

En CSS, flex hace referencia a un modelo de diseño llamado Flexbox (Flexible Box Layout). Es una herramienta muy útil para alinear y distribuir el espacio entre elementos en un contenedor, incluso cuando su tamaño es desconocido o dinámico.

El modelo Flexbox permite que los elementos dentro de un contenedor se ajusten de manera flexible, tanto en una dirección (horizontal o vertical) como en la forma de distribuir el espacio entre ellos.

### Propiedad `flex`

Es una propiedad que establece como deben de funcionar el contenedor respecto a sus elementos hijos. Para hacer que un elemento padre sea de tipo `flex` cambiamos su tipo en la propiedad: `display: flex`.

#### Dirección de los ejes

Para saber como posicionar los elementos tenemos tener en cuenta las direcciones que existen cuando trabajamos con flex:

- **main axis:** Define el eje horizontal.
- **croos axis:** Define el eje vertical.

![](https://miro.medium.com/v2/resize:fit:1183/1*ubDrM-3m22gLF_pZ4DCdMw.png)


> **Importante:** Con `flex` trabajamos siempre en un mismo eje `filas` o `columnas`. Esto quiere decir que cuando establecemos la dirección que queremos usar, los elementos se van colocan siempre de esa dirección unidireccional.


### Propiedad `flex-direction`

Con `flex-direction` podemos modificar la dirección del eje principal del contenedor para que se oriente en horizontal (valor por defecto) o en vertical. Además, también podemos incluir el sufijo -reverse para indicar que coloque los ítems en orden inverso.

| Valor           | Descripción                                                     |
|-----------------|-----------------------------------------------------------------|
| `row`           | Establece la dirección del eje principal en horizontal.         |
| `row-reverse`   | Establece la dirección del eje principal en horizontal invertido. |
| `column`        | Establece la dirección del eje principal en vertical.          |
| `column-reverse`| Establece la dirección del eje principal en vertical invertido. |


```html
<section class="parent">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</section>
```

```css
.parent {
  display: flex;
  flex-direction: row; /* row, row-reverse, column, column-reverse */
}

.item {
  border: 1px solid;
  opacity: .9;
  width: 100px;
  height: 100px;
  background: #09f;
}

.item:first-child {
  background: yellow;
}

.item:last-child {
  background: red;
}
```

![](../img/flex%20%20flex-direction%202.png)

![](../img/flex%20%20flex-direction%201.png)


### Contenedor flex multilinea

En general, `flex` se suele utilizar para estructuras de una sola dimensión, es decir, contenedores que sólo van en una dirección. Sin embargo, existe una propiedad denominada `flex-wrap` con la que podemos especificar un comportamiento especial del contenedor.


#### Propiedad `flex-wrap`

Por defecto, si un elemento no cabe dentro de nuestro contenedor `flex`, los elementos se harán más pequeños (son flexibles) para ajustarlos al contenedor. Este es el comportamiento por defecto de un contenedor `flex`. Sin embargo, con la propiedad `flex-wrap` podemos cambiar este comportamiento y permitir que nuestro contenedor `flex` se desborde, convirtiéndose en un contenedor `flex` multilínea.

| Valor           | Descripción                                                     |
|-----------------|-----------------------------------------------------------------|
| `nowrap`        | Los ítems se ajustan para ocupar el tamaño del contenedor (no permite desbordamiento en múltiples líneas). Valor por defecto. |
| `wrap`          | Establece los ítems en modo multilínea (permite que se desborde el contenedor). |
| `wrap-reverse`  | Establece los ítems en modo multilínea, pero en dirección inversa. |


Veamos como funciona los diferentes valores de la propiedad `flex-wrap`.

- Establecemos un `width` en contenedor padre `.parent`.
- El contenedor padre, al ser de tipo `flex` los elementos hijos se ajustan automáticamente al tamaño `width` del padre aunque estos tengan sus propios tamaños.

```css
.parent {
  width: 200px;
  border: 2px solid;
  
  display: flex;
  flex-direction: row;
  flex-wrap: wrap; /* nowrap, wrap, wrap-reverse */
}

.item {
  border: 1px solid;
  opacity: .9;
  width: 100px;
  height: 100px;
  background: #09f;
}

.item:first-child {
  background: yellow;
}

.item:last-child {
  background: red;
}
```

Los elementos hijos tienen un `width` definio pero el contenedor padre es más pequeño. Con `flex-wrap: wrap` los elementos hijos mantienen sus tamaños y da salto de linea tratando de encajar dentro del contenedor.

![](../img/flex%20flex-wrap%201.png)

El valor `wrap-reverse` simplemente voltea los elementos.

#### Atajo: Dirección de los ejes `flex-flow`

Recuerda que existe una propiedad de atajo (short-hand) llamada `flex-flow`, con la que podemos resumir los valores de las propiedades `flex-direction` y `flex-wrap`, especificándolas en una sola propiedad y ahorrándonos utilizar las propiedades concretas:


```css
.parent {
  width: 200px;
  border: 2px solid;

  display: flex;
  /* 
  flex-direction: row;
  flex-wrap: wrap; 
  */
  flex-flow: row wrap; /* atajo */
}
```

![](../img/flex%20flex-wrap%201.png)


### Gap

Los gap permiten establecer el tamaño de un «hueco» entre ítems desde el elemento padre contenedor, y que eliminan la necesidad de estar utilizando padding o margin en los elementos hijos


| Propiedad     | Valor   | Descripción                                                        |
|---------------|---------|--------------------------------------------------------------------|
| `row-gap`     |  normal \ `size`| Espacio entre filas (sólo funciona con `flex-direction: column`).  |
| `column-gap`  |  normal \ `size`| Espacio entre columnas (sólo funciona con `flex-direction: row`). |

> **Importante:** Ten en cuenta que los huecos sólo se aplican entre elementos, y no entre un elemento hijo y su contenedor padre.

#### Atajo: Propiedad `gap`

En Flex CSS existe una propiedad de atajo para los huecos, denominada gap. Con esta propiedad podemos indicar de una sola vez valores para las propiedades `row-gap` y `column-gap`, de forma que escribimos menos y es más cómodo en ciertas situaciones:

| Propiedad     | Valor   | Descripción                                                       |
|---------------|---------|-------------------------------------------------------------------|
| `gap`         | 0 \ `size`     | Aplica el tamaño indicado para el hueco en ambos ejes.           |
| `gap`         | 0 \ `size size`   | Aplica los tamaños indicados para el hueco del eje X y el eje Y. |


```css
.parent {
  width: 200px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
  flex-flow: row wrap;
  gap: 10px;
}
```

![](../img/flex%20gap.png)


### Elementos flexibles

A excepción de la propiedad `align-self` vista en temas anteriores, todas las propiedades que hemos visto hasta ahora se aplican sobre el elemento contenedor. Las siguientes propiedades, sin embargo, se aplican sobre los elementos `hijos`.

#### Propiedades de flexibilidad

Las siguientes propiedades nos permiten dotar de flexibilidad a los elementos hijos de un contenedor flex:


| Propiedad      | Valor     | Descripción                                                       |
|----------------|-----------|-------------------------------------------------------------------|
| `flex-grow`    | 0 \ `number`       | Número que indica el factor de crecimiento de los elementos. (`0`: no crece, `1`: crece). |
| `flex-shrink`  | 1 \ `number`       | Los elementos pueden reducir su tamaño a un tamaño más pequeño que se flex-basic. (`0`: no  se encoge, `1`: se encoge).|
| `flex-basis`   | `size` \ content | Tamaño base de los elementos antes de aplicar una variación. (`auto`: usa el `width` del elemento, `0`: )      |

Veamos un ejemplo para saber como funciona: Establecemos una medidas fija al contenedor padre.

```css
.parent {
  width: 200px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
  flex-flow: row nowrap;
}
```

En los elementos hijos establecemos las propiedades de flexibilidad, las cuales permitiran a dichos elementos estirarse o no.


```css
.item {
  border: 1px solid;
  opacity: .9;
  height: 100px;
  background: #09f;

  /* valores por defecto */
  flex-grow: 0;  /* los elementos NO crecen */
  flex-shrink: 1;  /* los elementos pueden reducir su tamaño*/
  flex-basis: auto;  /* tamaño base de los elementos */
}
```

![](../img/flex%20flex%201.png)

Ahora modifiquemos le `width` del 1er elemento para que ocupe más espacio que los demás. 

```css
.item:first-child {
  background: yellow;
  width: 50px;
}
```

![](../img/flex%20flex%202.png)

Cambiamos los valores por defecto de la propiedades de flexibilidad para que los elementos ocupen el espacio restante del contenedor padre.


```css
.item {
  border: 1px solid;
  opacity: .9;
  height: 100px;
  background: #09f;

  flex-grow: 1;  /* los elementos crecen */
  flex-shrink: 1;  /* los elementos pueden reducir su tamaño*/
  flex-basis: auto;  /* tamaño base de los elementos */
}
```

![](../img/flex%20flex%204.png)


Por último podemos hacer que los elementos independientemente de su tamaño personal ocupen por igual el espacio del contenedor padre.

```css
.item {
  border: 1px solid;
  opacity: .9;
  height: 100px;
  background: #09f;

  flex-grow: 1;  /* los elementos crecen */
  flex-shrink: 1;  /* los elementos pueden reducir su tamaño*/
  flex-basis: 0;  /* los elementos se ajustan todos al mismo tamaño */
}
```

![](../img/flex%20flex%203.png)


Podemos hacer que los elementos hijos ocupen el doble de sus compañeros. Separamos cada uno de los hijos y al primero le colocamos la propiedad `flex: 2`.


```css
.item {
  border: 1px solid;
  opacity: .9;
  height: 100px;

  flex: 1;  /* atajo */
}

.item:first-child {
  background: yellow;
  flex: 2;
}

.item:nth-child(2) {
  background: #09f;
}

.item:last-child {
  background: red;
}
```

![](../img/flex%20flex%204.png)


Podemos indicar el tamaño del creciemiento de cada uno de los elementos hijos.


```css
.item:first-child {
  background: yellow;
  flex: 1;
}

.item:nth-child(2) {
  background: #09f;
  flex: 2;
}

.item:last-child {
  background: red;
  flex: 1;
}
```

![](../img/flex%20flex%205.png)


### Atajo: Propiedad `flex`

Existe una propiedad denominada `flex` que sirve de atajo para estas tres propiedades indicadas en los ítems hijos. Veamos como funciona, ya que se trata de una propiedad muy versátil que soporta varios formatos:

| Propiedad         | Valor            | Descripción                                                       |
|-------------------|------------------|-------------------------------------------------------------------|
| `flex` (1 parámetro) | none \ `basis` `grow`  | Establece un tamaño base o un factor de crecimiento.              |
| `flex` (2 parámetros) | `grow` `shrink`       | Establece un factor de crecimiento y un factor de decrecimiento.  |
| `flex` (3 parámetros) | 0 1 auto \ `grow` `shrink` `basis`   | Establece el factor de crecimiento y decrecimiento y el tamaño base. |

**Orden del atajo:**

```css
flex: flex-grow  flex-shrink  flex-basis;
```


**Valores comunes y comportamiento**

1. `flex: 1`:
    - Equivale a `flex: 1 1 0`.

    - El elemento crece, se encoge, el tamaño de los elementos se distribuyan uniformemente en el contenedor.

2. `flex: auto`:
    - Equivale a `flex: 1 1 auto`.

    - El elemento crece, se encoge, usa el tamaño base de los elementos su `widht`.

3. `flex: none`:
    - Equivale a `flex: 0 0 auto`.

    - El elemento no crece, no se encoge, usa el tamaño base de los elementos su `widht`.

4. `flex: 100%`:
    - Equivale a flex: `1 1 100%`.
    - El elemento crece, se encoge, el tamaño inicial del elemento será el 100% del contenedor padre.
    - Este valor se utiliza cuando deseas que un elemento ocupe todo el espacio disponible en su contenedor flexible.

```css
  /*  flex: crecer  encogerce  tamañobase */
  /*  flex: 0 1 auto; */   /*<--  defecto*/
  /*  flex: 1 1 0;    */   /*<--  1*/
  /*  flex: 1 1 auto; */   /*<--  auto*/
  /*  flex: 0 0 auto; */   /*<--  none*/
  /*  flex: 1 1 100%; */   /*<--  100%*/
```

```css
.contenedor {
  display: flex;
}

.item1 {
  flex: 1; /* Crece y se encoge, tamaño base 0 */
}

.item2 {
  flex: auto; /* Crece y se encoge, tamaño de su width */
}

.item3 {
  flex: none; /* No crece ni se encoge, tamaño de su width */
}

.item4 {
  flex: 100%; /* Crece y se encoge, tamaño 100% del contenedor padre */
}

.item5 {
  flex: 2 1 100px; /* Crece más que item1, se encoge, tamaño base 100px */
}

.item6 {
  flex: 1 0 100px; /* Crece, no se encoge, tamaño base 100px */
}

```


### Propiedad `order`

Esta propiedad permite modificar el orden de los elementos hijos dependiendo de su posicionamiento.


```css
.item:first-child {
  background: yellow;
  order: 3;
}

.item:nth-child(2) {
  background: #09f;
  order: 1;
}

.item:last-child {
  background: red;
  order: 2;
}
```

![](../img/flex%20order%201.png)


### Alinear y centrar con Flex CSS

Cuestiones habituales en el mundo de CSS suelen ser «Cómo centrar con Flex», «cómo alinear verticalmente» o «cómo alinear horizontalmente». 

#### Propiedades de alineación

Ahora, tras el tema de Introducción a Flex, tenemos un control básico de un contenedor con ítems flexibles. Pero para alinear correctamente, necesitamos conocer las propiedades existentes dentro de `flex` para disponer los ítems dependiendo de nuestro objetivo.


Vamos a echar un vistazo a las siguientes propiedades, donde algunas actuan en el eje principal:


| Propiedad         | Valor                                                              | Actúa en eje  |
|-------------------|--------------------------------------------------------------------|---------------|
| `justify-content` | `start`, `end`, `center`, `space-between`, `space-around`, `space-evenly` | Horizontal           |
| `align-items`     | `start`, `end`, `center`, `stretch`, `baseline`                    | Vertical           |
| `align-content`   | `start`, `end`, `center`, `space-between`, `space-around`, `space-evenly`, `stretch` | Vertical           |


#### propiedad `justify-content`

La primera propiedad, `justify-content`, sirve para colocar los ítems de un contenedor mediante una disposición concreta a lo largo del eje principal (por defecto, en horizontal). Los valores que puede tomar esta propiedad son los siguientes:


| Valor          | Descripción                                                              |
|----------------|--------------------------------------------------------------------------|
| `start`        | Agrupa los ítems al inicio del eje principal.                            |
| `end`          | Agrupa los ítems al final del eje principal.                             |
| `center`       | Agrupa los ítems al centro del eje principal.                           |
| `space-between`| Distribuye los ítems dejando espacio entre ellos.                       |
| `space-around` | Distribuye los ítems dejando espacio alrededor de ellos.                |
| `space-evenly` | Distribuye como `space-around`, pero con un espacio exactamente igual alrededor de ellos. |


```html
<section class="parent">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</section>
```

```css
.parent {
  width: 300px;
  height: 500px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 10px;
}

.item {
  width: 50px;
  height: 50px;
  border: 1px solid;
  opacity: .9;
}

.item:first-child {
  background: yellow;
}

.item:nth-child(2) {
  background: #09f;
}

.item:last-child {
  background: red;
}
```

![](../img/flex%20justify-content%201.png)

![](../img/flex%20justify-content%202.png)


#### Propiedad `align-items`

Existe otra propiedad importante denominada `align-items`. Se encarga de alinear los ítems en el eje vertical del contenedor. Hay que tener cuidado de no confundir `align-items` con `align-content`, puesto que el segundo actúa sobre cada una de las líneas de un contenedor multilinea (no tiene efecto si no usamos flex-wrap), mientras que `align-items` lo hace sobre la única línea que tiene un contenedor flex sin wrap.

Los valores que puede tomar `align-items` son los siguientes:


| Valor     | Descripción                                                               |
|-----------|---------------------------------------------------------------------------|
| `start`   | Alinea los ítems al inicio del eje secundario.                            |
| `end`     | Alinea los ítems al final del eje secundario.                             |
| `center`  | Alinea los ítems al centro del eje secundario.                            |
| `stretch` | Alinea los ítems estirándolos de modo que cubran desde el inicio hasta el final del contenedor. |
| `baseline`| Alinea los ítems en el contenedor según la base del contenido de los ítems del contenedor. |

Antes de pasar al ejemplo explicativo, recordemos que cuando hacemos un elemento padre `flex`, y sus elementos hijos **NO** tiene un `height` defino los elementos se estiran hasta ocupar todo el espacio del contenedor padre.

```css
.parent {
  width: 300px;
  height: 500px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
}

.item {
  width: 50px;
  border: 1px solid;
  opacity: .9;
}
```

![](../img/flex%20align-items%200.png)

Ahora si, pasemos el ejemplo:

```css
.parent {
  width: 300px;
  height: 500px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 10px;
}
```

![](../img/flex%20align-items%201.png)

![](../img/flex%20align-items%202.png)


### Alineacion multilinea

Una vez entendidos los casos anteriores, debemos atender a la propiedad `align-content`, que es un caso particular de `align-items`. Nos servirá cuando estemos tratando con un contenedor `flex` multilinea creado mediante `flex-wrap`. Los contenedores multilinea son un tipo de contenedor en el que, cuando los ítems no caben en el ancho disponible, el eje principal se divide en múltiples líneas.

#### Propiedad `align-content`

De esta forma, `align-content` servirá para alinear cada una de las líneas del contenedor multilinea. Los valores que puede tomar la propiedad `align-content` son los siguientes:


| Valor          | Descripción                                                              |
|----------------|--------------------------------------------------------------------------|
| `start`        | Agrupa los ítems al inicio del eje principal.                            |
| `end`          | Agrupa los ítems al final del eje principal.                             |
| `center`       | Agrupa los ítems al centro del eje principal.                           |
| `space-between`| Distribuye los ítems desde el inicio hasta el final.                     |
| `space-around` | Distribuye los ítems dejando el mismo espacio a los lados de cada uno.   |
| `stretch`      | Estira los ítems para ocupar de forma equitativa todo el espacio.        |


```html
<section class="parent">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</section>
```

```css
.parent {
  width: 300px;
  height: 500px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  align-content: center;
  gap: 10px;
}
```

![](../img/flex%20align-content%201.png)

![](../img/flex%20align-content%202.png)


**Notas importantes:**
- `align-content` solo funciona cuando hay más de una línea (en Flexbox, por ejemplo, cuando usas `flex-wrap: wrap`) o fila/columna (en Grid). Si todos los elementos están en una sola línea, esta propiedad no tiene efecto.

- En Flexbox, si los ítems tienen una altura fija (por ejemplo, `height: 50px`), el valor de `stretch` no los estirará más allá de ese valor.



### Alineaciones especificas

Por otro lado, la propiedad `align-self` actúa exactamente igual que align-items, sin embargo es la primera propiedad de flex que vemos que se utiliza sobre un elemento hijo específico y no sobre el elemento padre contenedor. Salvo por este detalle, funciona exactamente igual que align-items.

#### Propiedad `align-self`

Observa los valores que puede tomar la propiedad `align-self`:


`align-self` nos permite cambiar el comportamiento de `align-items` y sobreescribirlo con comportamientos específicos para ítems concretos que no queremos que se comporten igual que el resto.


| Valor     | Descripción                                                               |
|-----------|---------------------------------------------------------------------------|
| `start`   | Alinea los ítems al inicio del contenedor.                                 |
| `end`     | Alinea los ítems al final del contenedor.                                  |
| `center`  | Alinea los ítems al centro del contenedor.                                |
| `stretch` | Alinea los ítems estirándolos al tamaño del contenedor.                   |
| `baseline`| Alinea los ítems en el contenedor según la base de los ítems.            |
| `auto`    | Hereda el valor de align-items del padre (si no se ha definido, es `stretch`).|


```html
<section class="parent">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</section>
```

```css
.parent {
  width: 300px;
  height: 500px;
  border: 2px solid;
  background: #e0dddd;

  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.item {
  width: 50px;
  height: 50px;
  border: 1px solid;
  opacity: .9;
}

.item:first-child {
  background: yellow;
  align-self: self-end; /* propiedad en el elemento específico */
}

.item:nth-child(2) {
  background: #09f;
}

.item:last-child {
  background: red;
}
```

![](../img/flex%20align-self%201.png)

![](../img/flex%20align-self%202.png)

### Resumen de todas las propiedades de flex

![](https://preview.redd.it/vd9dc7wfk9471.png?auto=webp&s=f6c78331f2c9fb2f8a13837e480a572d7c266752)


### Ejemplo de un contenedor flexible

```html
<div class="container">
  <div class="item">Elemento 1</div>
  <div class="item">Elemento 2</div>
  <div class="item">Elemento 3</div>
  <div class="item">Elemento 4</div>
  <div class="item">Elemento 5</div>
  <div class="item">Elemento 6</div>
</div>
```

```css
/* Estilo del contenedor */
.container {
    display: flex;
    flex-wrap: wrap;  /* Permite que los elementos se envuelvan cuando el contenedor se encoja */
    justify-content: space-between;  /* Distribuye los elementos de manera uniforme */
    gap: 10px;  /* Espacio entre los elementos */
    width: 100%;  /* El contenedor ocupará el 100% del ancho disponible */
    border: 2px solid #ccc;  /* Solo para visualizar el contenedor */
    padding: 10px;
    box-sizing: border-box;
}

/* Estilo de los elementos dentro del contenedor */
.item {
    flex: 1 1 150px;  /* El elemento puede crecer, reducirse y tiene un tamaño base de 150px */
    background-color: lightblue;
    border: 1px solid #aaa;
    padding: 20px;
    text-align: center;
    box-sizing: border-box;
}

/* Estilo opcional para mejorar la visualización */
.item:nth-child(even) {
    background-color: lightgreen;
}
```

![](../img/Flex%20ejemplo%20contenedor%20flexible.png)

---

Regresar al [README](../README.md)