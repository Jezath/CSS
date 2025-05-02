# Grid

---

- [Definir filas y columnas fijas](#definir-filas-y-columnas-fijas)
- [Unidad fracción restante fr](#unidad-fraccion-restante-fr)
- [Filas y columnas repetitivas](#filas-y-columnas-repetitivas)
- [Celdas irregulares](#celdas-irregulares)
- [Alinear con grid](#alinear-con-grid)
- [Alineacion de elementos (items)](#alineacion-de-elementos-items)
- [Alineacion de contenido (todo la cuadricula)](#alineacion-de-contenido-todo-la-cuadricula)
- [Alineaciones especificas](#alineaciones-especificas)
- [Grid areas](#grid-areas)

---

Para crear diseños basados en Grid CSS necesitaremos tener en cuenta una serie de conceptos que utilizaremos a partir de ahora y que definiremos a continuación:

![](https://lenguajecss.com/css/grid/que-es-grid/grid-css-conceptos.png)

- **Contenedor**: El elemento padre contenedor que definirá la cuadrícula o rejilla.
- **Ítem**: Cada uno de los hijos que contiene la cuadrícula (elemento contenedor).
- **Celda** (grid cell): Cada uno de los cuadritos (unidad mínima) de la cuadrícula.
- **Area** (grid area): Región o conjunto de celdas de la cuadrícula.
- **Banda** (grid track): Banda horizontal o vertical de celdas de la cuadrícula.
- **Línea** (grid line): Separador horizontal o vertical de las celdas de la cuadrícula.

Css grid es un sistema de cuadrículas conformadas por `filas` y `columnas`, la unión de las filas rows y columnas colunms dan lugar a las `celdas`.


![](../img/flex%20vs%20grid.png)


> **Importante:** La diferencia entre flex y grid es que `flex` es unidimensional (filas y columnas) y `grid` es bidimensional (filas y columas).


### Propiedad `display: grid`

![](../img/grid%20display-grid.png)

Antes de comenzar hacer una cuadrícula de grid, veamos como se comporta inicialmente grid.
Tenemos el típico ejemplo HTML que serán el contenedor y sus elementos hijos.

```html
<section class="container">
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
  <div class="box">4</div>
  <div class="box">5</div>
  <div class="box">7</div>
</section>
```

En el css estableemos los estilos básicos para notar la diferencia entre los elementos.

```css
.container {
  margin-top: 50px;
  background: #e0dddd;
  border: 1px solid;
  border-radius: 5px;
  box-sizing: border-box;
}

.container .box {
  background: lightblue;
  border: 1px solid;
  border-radius: 2px;
}
```

![](../img/grid%200.png)

Aplicamos el `display: grid` en el elemento padre `.container`. A simple vista no vemos un cambio notorio visual a diferencia de flex donde los elementos se colocaban uno a lado de otros por defecto.


```css
.container {
  margin-top: 50px;
  background: #e0dddd;
  border: 1px solid;
  border-radius: 5px;
  box-sizing: border-box;

  display: grid;
}
```

Si revisamos las herramientas del navegador podemos ver que el elemento `.container` tiene lineas punteadas con números (**que indican las filas y columnas**), esto indica que la propiedad `grid` se está aplicando correctamente y podemos empezar a manipular los elementos internos.

- En este ejemplo tenemos 1 columna y 6 filas.

![](../img/grid%201.png)


> **Nota:** Incluso si los elementos hijos tienen un `width` y un `height` establecidos, cuando recién aplicamos `display: grid` los elementos visualmente parecen comportarse como display: block.

![](../img/grid%202.png)


### Definir filas y columnas fijas

En Grid CSS, la forma principal de definir una cuadrícula es indicar el tamaño de sus filas y sus columnas de forma explícita. Para ello, sólo tenemos que usar las propiedades CSS grid-template-columns y grid-template-rows:


| Propiedad            | Valor                       | Descripción                                               |
|----------------------|-----------------------------|-----------------------------------------------------------|
| `grid-template-columns` | `col1` `col2` ...           | Establece el tamaño de cada columna (col 1, col 2...).    |
| `grid-template-rows `   | `fila1` `fila2` ...         | Establece el tamaño de cada fila (fila 1, fila 2...).     |


> **Nota:** Cada valor que le pongamos representa una fila o columna. Podemos usar diferentes tipos de valores (`auto` `30px` `1fr` `40%` `10vw`). 

> **Importante:** No es consejable mezclar diferentes tipos de medidas en grid. Usar 1 del mismo tipo.

```css
.grid {
  display: grid;
  grid-template-columns: 50px 300px; /* auto 30px 1fr -> 3 columnas*/
  grid-template-rows: 200px 75px;    /* 200px 75px    -> 2 filas */
}
```

Con la propiedad `display: grid` definimos que queremos crear un grid, y mediante las propiedades `grid-template-columns` y `grid-template-rows` definimos los tamaños de las columnas y las filas del mismo. Esto significa que, a priori, tendríamos una cuadricula o grid de 4 celdas en total:

![](https://lenguajecss.com/css/grid/que-es-grid/grid-template-columns.png)


Si definimos filas y columnas de más, y no tenemos elementos suficientes para rellenar la cuadrícula, grid dejará los espacios vacios.

```css
  display: grid;
  grid-template-columns: auto 100px 1fr;
  grid-template-rows: 20px 50px 30px; /* fila restante = 30px */
```

![](../img/grid%20grid-template-columns%201.png)


#### Propiedad `grid-auto-rows`

Permite darle un tamaño a las filas que se crean automáaticamente.

```css
.container {
  margin-top: 50px;
  background: #e0dddd;
  border: 1px solid;
  border-radius: 5px;
  box-sizing: border-box;

  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-auto-rows: 50px;
}
```

![](../img/grid%20grid-auto-rows%201.png)

Si tenemos definos las filas mediante el `grid-template-rows`, la propiedad `grid-auto-rows` generará el tamaño de las filas restantes.

```css
grid-template-columns: 1fr 2fr; /* 2 columnas */
grid-template-rows: 30px;       /* 1ra filaa */
grid-auto-rows: 50px;           /* filas restantes */
```

![](../img/grid%20grid-auto-rows%202.png)


#### Propiedad `grid-auto-flow`

La primera de ellas es `grid-auto-flow`, una propiedad que permite indicar cuál es el flujo del contenido de un Grid, es decir, si queremos que los elementos aparezcan de manera horizontal (row) o de manera vertical (column). También hay un valor dense, pero de él hablaremos más adelante.

Estos son los valores que podemos utilizar en la propiedad `grid-auto-flow`:


| Valor          | Descripción                                                                      |
|----------------|----------------------------------------------------------------------------------|
| `row`          | Los elementos se colocan en filas, completando la fila antes de pasar a la siguiente. |
| `column`       | Los elementos se colocan en columnas, completando la columna antes de pasar a la siguiente. |
| `row dense`    | Idem a row, pero rellenando los huecos si los hay.                              |
| `column dense` | Idem a column, pero rellenando los huecos si los hay.                           |

![](../img/grid%20grid-auto-flow%201.png)


### Unidad fraccion restante `fr`

`fr` es una unidad especial que  nos permite indicar el tamaño proporcional, proporcional al tamaño del contenedor padre.

```css
grid-template-columns: 1fr;         /* -> 100% */
grid-template-columns: 1fr 1fr;     /* -> 50% 50% */
grid-template-columns: 1fr 100px;   /* -> 100% - 100px = valor fr */
grid-template-columns: 1fr 1fr 1fr; /* -> 100 / 3 = 33.33% */
grid-template-columns: 1fr 1fr 1fr; /* -> 100 / 3 = 33.33% */
grid-template-columns: 2fr 4fr 1fr; /* -> 2fr = el doble */
```

Supongamos el siguiente fragmento de código, donde utilizamos las unidades fr:


```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 2fr 1fr;
}
```

Este nuevo ejemplo, también crea una cuadrícula de 2x2, donde el tamaño de la cuadrícula se divide en:

- **Dos columnas:** Mismo tamaño de ancho para cada una.
- **Dos filas:** La primera fila ocupará el doble (2fr) que la segunda fila (1fr).

![](https://lenguajecss.com/css/grid/que-es-grid/grid-unidad-fr.png)


De esta forma, es muy fácil predecir el espacio que va a ocupar la cuadrícula, ya que sólo tenemos que sumar todas las unidades para saber el tamaño total, y comparar con cada columna o fila para saber como de grande o pequeña es respecto al total. Así tendremos un mejor control del espacio restante de la cuadrícula, y resultará más intuitivo calcularlo.


```css
.container {
  margin-top: 50px;
  background: #e0dddd;
  border: 1px solid;
  border-radius: 5px;
  box-sizing: border-box;

  display: grid;
  grid-template-columns: 1fr 2fr;
}
```

![](../img/grid%20grid-template-columns%202.png)


### Filas y columnas repetitivas

En algunos casos, en las propiedades `grid-template-columns` y `grid-template-rows` podemos necesitar indicar las mismas cantidades un número alto de veces, resultando repetitivo y molesto escribirlas varias veces. 

La función `repeat()` podemos usarla para indicar la repetición de valores, señalando el número de veces que se repiten y el tamaño en cuestión.

La expresión a utilizar sería la siguiente: 
- repeat(número de veces `number`, tamaño `size`).


```css
.container {
  margin-top: 50px;
  background: #e0dddd;
  border: 1px solid;
  border-radius: 5px;
  box-sizing: border-box;

  display: grid;
  grid-template-columns: repeat(3, 1fr);  /* repite (1fr) 3 veces -> 1fr 1fr 1fr; */
  grid-template-rows: repeat(2, 50px);    /* repite (50px) 2 veces -> 50px 50px;   */
}
```

![](../img/grid%20repeat%201.png)

Podemos usar la función `repeat()` combinando los valores fijos. Pero siempre y cuando tengamos un patron de valores repetidos.


```css
  grid-template-columns: 40px repeat(2, 1fr); /* 40px 1fr 1fr */
  grid-template-rows: repeat(2, 50px);
```

![](../img/grid%20repeat%202.png)

Otro ejemplo usando `repeat()` con valores que siguen un patron: `25px 50px 25px 50px...`


```css
grid-template-columns: repeat(2, 25px 50px); /* repite (25px 50px) dos veces */
```

![](../img/grid%20repeat%203.png)


La función `minmax()` se puede utilizar como valor para definir rangos flexibles de celda. 

Funciona de la siguiente forma:
- minmax(tamaño min, tamaño max)

Esta función se usa para hacer cuadrículas flexibles, o cuando queremos que una fila o columna tenga un tamaño mínimo.


```css
grid-template-columns: minmax(100px, 1fr) 1fr 1fr;
grid-template-rows: repeat(2, 50px);
```

Si encogemos la cuadrícula vemos como la 1ra columna conserva su tamaño mínimo de 100px y cuando puede estirarse lo hace,  mientras que las otras columnas se encogen.

![](../img/grid%20minmax%201.png)


#### Los valores `auto-fill` y `auto-fit`

En la función `repeat()` es posible utilizar las palabras claves `auto-fill` o `auto-fit` para indicar al navegador que queremos que rellene o ajuste el contenedor grid con múltiples elementos hijos dependiendo del tamaño del `viewport` (región visible del navegador).

- `auto-fill`: Deja espacios en la cuadrícula. Es la que se tiene que usar.
- `auto-fit`: Estira los elementos para cubrir todo el espacio del contenedor.


Veamos estos valores aplicado en uno de los ejemplos más usados en la maquetación web:

- Tenemos el siguiente HTML donde el `<div>` funciona de contenedor y dentro de el tenemos muchas imágenes.

```html
<div>
  <img src="https://geekzilla.tech/home/wp-content/uploads/2023/06/clean-666x1024.jpg">
  <img src="https://geekzilla.tech/home/wp-content/uploads/2023/06/clean-666x1024.jpg">
  <img src="https://geekzilla.tech/home/wp-content/uploads/2023/06/clean-666x1024.jpg">
  ...
</div>
```

- Vamos hacer que el contendor sea flexible con grid, usando las funciones de `repeat()`, `minmax()` y `auto-fill`.


```css
div {
  max-width: 800px;
  margin: 0 auto;

  display: grid;
  grid-template-columns: repeat(
    auto-fill,
    minmax(200px, 1fr)
  );
  gap: 30px 15px;
} 

img {
  width: 100%;
  height: auto;
}
```

Mientras hacemos más pequeña la vista de la pantalla los elementos se van ajustando automáticamente.

![](../img/grid%20ejemplo%201.webp)


### Propiedad `gap`

Al igul que en flex podemos usar la propiedad `gap` que de hecho es una propiedad exclusiva de grip.

|Propiedad|Significado|
|---------|-----------|
|`grid-column-gap`|Da espacion entre las columnas de la cuadrícula|
|`grid-row-gap`|Da espacion entre las filas de la cuadrícula|
|`gap`|Es la propiedad de atajo.|

```css
/* 
grid-column-gap: 15px;
grid-row-gap: 30px; 
*/
gap: 30px 15px; /* <- atajo 2 valores: filas columnas  */
gap: 20px;      /* <- atajo 1 valor: el espacio es el mismo para las filas y columnas  */
```


![](../img/grid%20resumen%201.png)


### Celdas irregulares

Las celdas irregulares en una cuadrícula son aquellas que ocupan el doble de tamaño que otras, este tipo de celdas se usan para hacer los famosos bentos de apple.

Salvo algunas excepciones como `justify-self`, `align-self `o `grid-area`, hemos visto propiedades CSS que se aplican solamente al contenedor padre de una cuadrícula. Las siguientes propiedades se aplican a los **ítems hijos** de una cuadrícula, para alterar o cambiar el comportamiento específico de dicho elemento.

| Propiedad          | Descripción                                                        |
|--------------------|--------------------------------------------------------------------|
| `grid-column-start`  | Indica en qué columna empezará el ítem de la cuadrícula.           |
| `grid-column-end `   | Indica en qué columna terminará el ítem de la cuadrícula.          |
| `Grid-column`   |  **Atajo** / Indica desde qué línea hasta que línea horizontal usaremos, ejemplo: 2 / 4 (línea 2 hasta línea 4)|
| `grid-row-start `    | Indica en qué fila empezará el ítem de la cuadrícula.              |
| `grid-row-end`       | Indica en qué fila terminará el ítem de la cuadrícula.             |
| `grid-row`       | Atajo / indica desde qué línea hasta que línea vertical usaremos, ejemplo: 2 / 4 (línea 2 hasta línea 4)|


Pasemos al ejemplo práctico. Tenemos la siguiente cuadrícula:


```html
<section class="container">
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
  <div class="box">4</div>
  <div class="box">5</div>
  <div class="box">7</div>
</section>
```


```css
.container {
  margin-top: 50px;
  background: #e0dddd;
  border: 1px solid;
  padding: 5px;
  border-radius: 6px;
  box-sizing: border-box;

  display: grid;
  grid-template-columns: minmax(100px, 1fr) 1fr 1fr;
  grid-auto-rows: 50px;
  gap: 10px;
}

.container .box {
  background: lightblue;
  border: 1px solid;
  border-radius: 3px;
}

.container .box:first-child { /* elementos el cual vamos a modificar para que abarque otros espacios */
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;
}
```


![](../img/grid%20celda%20irregular%201.png)


Vamos hacer que el elemento verde abarque otros espacios de la cuadrícula.


```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  grid-column-start: 1;
  grid-column-end: 3;
}
```

![](../img/grid%20celda%20irregular%202.png)


Podemos dejar espacios vacíos gracias que posicionamos el elemento donde estaba el 2do.

```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  grid-column-start: 2;
  grid-column-end: 3;
  /* atajo */
  grid-column: 1 / 3;
}
```

![](../img/grid%20celda%20irregular%203.png)


Como vemos, mientras le indicamos que el elemento ocupe cierto espacio va empujando a los demás

```css
grid-column-start: 2;
grid-column-end: 4;
```

![](../img/grid%20celda%20irregular%204.png)

- Ahora veamos como funcionan las filas.


```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  grid-row-start: 1;
  grid-row-end: 3;
  /* atajo */
  grid-row: 1 / 3;
}
```

![](../img/grid%20celda%20irregular%205.png)

Podemos usar el valor `span` para decirle cuantos espacios tiene que ocupar el elemento. Ejemplo span 2 = ocupa dos espacios

```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  grid-column-start: span 2;
  grid-row-start: span 2;
  /* atajo */
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
```

![](../img/grid%20celda%20irregular%206.png)


Gracias a que podemos posicionar los elementos con las propiedades tambien podemos cambiar la posición de los elementos.

```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  grid-column: 2 / 4;
  grid-row: 2 / 3;
}

.container .box:nth-child(2) {
  background: lightskyblue;
  border: 1px solid blue;
  border-radius: 3px;

  grid-column: 1 / 3; /* podemos usar valores negativos -> grid-column: 1 / -2, tener en cuenta el grid */
}
```

![](../img/grid%20celda%20irregular%207.png)


Podemos usar valores negativos, solo hay que tener en cuenta los valores que salen en la cuadrícula.

```css
.container .box:nth-child(2) {
  background: lightskyblue;
  border: 1px solid blue;
  border-radius: 3px;

  grid-column: 1 / -2;
}
```
![](../img/grid%20celda%20irregular%207.png)

Tambien podemos usar los valores negativos para indicarle a un elemento que ocupe todo el espacio horizontal o vertical.

```css
.container .box:nth-child(2) {
  background: lightskyblue;
  border: 1px solid blue;
  border-radius: 3px;

  grid-column: 1 / -1;
}
```

![](../img/grid%20celda%20irregular%208.png)


Podemos poner elementos encima de otros de forma controla colocando los mismos valores.


```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  grid-column: 1 / 3;
  grid-row: 1 / 3;
}

.container .box:nth-child(2) {
  background: lightskyblue;
  border: 1px solid blue;
  border-radius: 3px;
  opacity: .5;

  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
```

![](../img/grid%20celda%20irregular%209.png)

#### Atajo: Propiedad `grid-area`

Por si no nos resulta cómodo aún trabajar con las propiedades de atajo grid-column y grid-row, podemos utilizar la propiedad `grid-area` que vimos en el tema de Grid por áreas que permite resumir las cuatro propiedades `grid-column-start`, `grid-column-end`, `grid-row-start` y `grid-row-end` en una sola.

| Propiedad  | Descripción                                                        |
|------------|--------------------------------------------------------------------|
| `grid-area`  | Propiedad de atajo para utilizar grid-row y grid-column.          |

Ejemplo del atajo `grid-area` para replicar el ejercicio anterior.

```css
.container .box:first-child {
  background: lightgreen;
  border: 1px solid green;
  border-radius: 3px;

  /* <row-start> / <column-start> / <row-end> / <column-end>  */
  grid-area: 1 / 1 / 3 / 3;
}
```

![](../img/grid%20celda%20irregular%209.png)


![](../img/grid%20resumen%202.png)


### Alinear con grid

Al igual que con la maquetación **Flex CSS**, Grid incorpora un sistema para alinear elementos que se basa en Flex y es incluso más potente, ya que permite la alineación de elementos en dos dimensiones, así como centrar o colocar elementos hijos del contenedor Grid.

#### Propiedades de alineación

Existen una serie de propiedades que se pueden utilizar para colocar y ajustar nuestra cuadrícula grid o ajustar los ítems a lo largo de ella, de forma sencilla y cómoda. Algunas de estas propiedades probablemente ya las conocerás del módulo CSS flex, sin embargo, en grid pueden tener un comportamiento diferente.


| Propiedad          | Valores                                                                 | Afecta a...   |
|--------------------|-------------------------------------------------------------------------|---------------|
| `justify-items`      | start, end, center, stretch                                             | eje horizontal|
| `align-items`        | start, end, center, stretch                                             | eje vertical |
| `justify-content`    | start, end, center, stretch, space-around, space-between, space-evenly  | eje horizontal |
| `align-content`      | start, end, center, stretch, space-around, space-between, space-evenly  | eje vertical |


### Alineacion de elementos (items)

#### Propiedad `justify-items`

La primera propiedad, `justify-items` sirve para colocar los ítems de un contenedor grid a lo largo de sus celdas correspondientes, siempre en el eje principal (por defecto, en horizontal). Los valores que puede tomar esta propiedad son los siguientes:


| Valor     | Descripción                                                                 |
|-----------|------------------------------------------------------------------------------|
| `start`   | Coloca cada ítem al inicio de su celda en el eje principal.                |
| `end`     | Coloca cada ítem al final de su celda en el eje principal.                 |
| `center`  | Coloca cada ítem en el centro de su celda en el eje principal.             |
| `stretch` | Hace que cada ítem se estire y ocupe todo el espacio disponible de su celda en el eje principal. |


#### Propiedad `align-items`

De forma análoga, la propiedad `align-items` sirve para colocar los ítems de un contenedor grid a lo largo de sus celdas correspondientes, pero en lugar de el eje principal, las coloca en el eje secundario (por defecto, en vertical). Los valores que puede tomar son los mismos que la propiedad anterior.


### Alineacion de contenido (todo la cuadricula)

#### Propiedad `justify-content`

La propiedad `justify-content` permite modificar la distribución del contenido de la cuadrícula en su contenedor padre, a lo largo de su eje principal (por defecto, el horizontal). Los valores que puede tomar son los siguientes:


| Valor           | Descripción                                                                                                      |
|------------------|------------------------------------------------------------------------------------------------------------------|
| `start`          | Coloca la cuadrícula en su conjunto al inicio del contenedor padre en su eje principal (horizontal).            |
| `end`            | Coloca la cuadrícula en su conjunto al final del contenedor padre en su eje principal (horizontal).             |
| `center`         | Coloca la cuadrícula en su conjunto al centro del contenedor padre en su eje principal (horizontal).            |
| `stretch`        | Estira la cuadrícula ocupando todo el espacio disponible del contenedor padre en su eje principal (horizontal). |
| `space-between`  | Establece espacios sólo entre las celdas, en su eje principal (horizontal).                                     |
| `space-around`   | Establece espacios alrededor de las celdas, en su eje principal (horizontal).                                   |
| `space-evenly`   | Idem al anterior, pero solapando los espacios, de modo que sean todos de tamaño equivalente.                     |


#### Propiedad `align-content`

De forma análoga, la propiedad `align-content` sirve para colocar el contenido de la cuadrícula en su contenedor padre, pero a lo largo de su contenedor secundario (por defecto, el vertical). Los valores que puede tomar son exactamente los mismos que la propiedad anterior.

Vamos con un ejemplo, usaremos otros estilos diferentes a los anteriores ejemplos de grid.


```html
<div class="parent">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
</div>
```

```css
.parent {
  background: lightgrey;
  min-height: 300px;
  
  display: grid;

  /* alinear elementos hijos */
  justify-items: start;
  align-items: start;

  /* alinear toda la cuadrícula */
  justify-content: end;
  align-content: end;

  grid-template-columns: repeat(2, 100px);
  grid-template-rows: 70px 100px;
  gap: 20px;
}

.item {
  background: #6d2a9c;
  color: whitesmoke;
}
```

![](../img/grid%20alineacion%201.png)

Veamos como centrar un elemento dentro de una cuadrícula de grid.

```css
.parent {
  background: lightgrey;
  min-height: 300px;
  
  display: grid;

  /* alinear elementos hijos */
  justify-items: start;
  align-items: center;

  /* alinear toda la cuadrícula */
  justify-content: center;
  align-content: center;

  grid-template-columns: repeat(2, 100px);
  grid-template-rows: 70px 100px;
  gap: 20px;
}
```

![](../img/grid%20centrar%20elementos%201.png)

Otra forma de centrar más corta es usar la propiedad `place-content: center`.


```css
.parent {
  background: lightgrey;
  min-height: 300px;
  
  display: grid;

  /* alinear elementos hijos */
  justify-items: start;
  align-items: center;

  /* centrar toda la cuadrícula */
  place-content: center;

  grid-template-columns: repeat(2, 100px);
  grid-template-rows: 70px 100px;
  gap: 20px;
}
```

![](../img/grid%20centrar%20elementos%201.png)


>**Nota:** Para poder visualizar las propiedades de `justify-content` y `align-content` en contenedor padre tiene que ser más grande que la cuadrícula.

![](../img/grid%20alineacion%20resumen.png)

### Alineaciones especificas

En el caso de que queramos que uno de los ítems hijos tenga una distribución diferente al resto, podemos aplicar en el elemento hijo la propiedad `justify-self` (eje principal) o `align-self` (eje secundario) sobreescribiendo su distribución su general, y aplicando una específica.


| Propiedad       | Descripción                                                                 |
|------------------|------------------------------------------------------------------------------|
| `justify-self`   | Altera la alineación del ítem hijo en el eje horizontal y la sobreescribe con la indicada. |
| `align-self`     | Altera la alineación del ítem hijo en el eje vertical y la sobreescribe con la indicada.   |

Agregamos clasese para indentificar cada elemento hijo.

```html
<div class="parent">
  <div class="item item-1">1</div>
  <div class="item item-2">2</div>
  <div class="item item-3">3</div>
  <div class="item item-4">4</div>
</div>
```

```css
.parent {
  background: lightgrey;
  min-height: 300px;
  
  display: grid;

  /* alinear todos los elementos hijos */
  justify-items: stretch;
  align-items: stretch;

  /* centrar toda la cuadrícula */
  place-content: center;

  grid-template-columns: repeat(2, 100px);
  grid-template-rows: 70px 100px;
  gap: 20px;
}

.item {
  background: #6d2a9c;
  color: whitesmoke;
}

.item-2 {
  background: green;

  /* alinear elementos hijos específicos */
  justify-self: end;
  align-self: center;
}
```

![](../img/grid%20alinear%20hijos%201.png)

![](../img/grid%20alinear%20hijos%20resumen.png)


### Atajo: Alineaciones Grid

Si vamos a crear estructuras grid donde utilicemos los pares de propiedades `justify-items` y `align-items` por un lado, `justify-content` y `align-content` por otro, e incluso `justify-self` y `align-self` por otro, podemos utilizar las siguientes propiedades de atajo:


| Propiedad      | Valores                                 | Descripción                            |
|----------------|------------------------------------------|----------------------------------------|
| `place-items`  | [align-items] [justify-items]          | Propiedad de atajo para *-items        |
| `place-content`| [align-content] [justify-content]      | Propiedad de atajo para *-content      |
| `place-self`   | [align-self] [justify-self]            | Propiedad de atajo para *-self         |

### Grid areas

Con las propiedades de grid áreas podemos literalmente ponerle nombres a los espacios de nuestra cuadrícula separando su espacio, y luego posicionar cada elemento con el nombre del área donde queremos poner ese elemento.

| Propiedad          | Descripción                                                        |
|--------------------|--------------------------------------------------------------------|
| `grid-template-areas`| Indica la disposición de las áreas en el grid. Cada texto entre comillas simboliza una fila. |
| `grid-area `         | Indica el nombre del área. Se usa sobre ítems hijos del grid.      |

Veamos un ejemplo creando un layout.

```html
<section class="container">
  <header>Header</header>
  <aside>Aside</aside>
  <main>Main</main>
  <footer>Footer</footer>
</section>
```

>**Nota:** La cantidad de nombre de las áreas deben coincidir con el número de las filas y columnas que establescamos primero.


```css
body {
  margin: 0;
}

.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 columnas */
  grid-template-rows: 35px 1fr 100px; /* 3 filas */
  min-height: 100vh;

  /* grid areas, asignamos la áreas con cada nombre específico */
  /* 3 columnas */
  grid-template-areas: 
    "header header aside" /* 3 filas */
    "main main main"
    "footer footer footer" 
  ;
}

/* responsive */
@media (width > 400px) {
  .container {
    display: grid;

    /* con grid areas podemos cambiar de lugar a los elementos gracias a sus nombres */
    grid-template-areas: 
      "header header header"
      "aside main main"
      "footer footer footer"
  ;
}
}

/* a los elementos hijos le ponemos el nombre de las áreas que les corresponde */
.container header {
  background: #09f;
  grid-area: header;
}

.container aside {
  background: yellow;
  grid-area: aside;
}

.container main {
  background: red;
  grid-area: main;
}

.container footer {
  background: gray;
  grid-area: footer;
}
MKZ-019
```

![](../img/grid%20areas%201.png)

Podemos dejar espacios vacíos colocando un `.` en vez del nombre del área.


```css
@media (width > 400px) {
    .container {
      display: grid;
      grid-template-areas: 
        "header header ."
        "aside main main"
        "footer footer footer"
      ;
    }
}
```

### Resumen de las propiedades de grid

![](https://preview.redd.it/phlaefsgoeb71.png?auto=webp&s=6c245020cd1512a7327dc7904b459a0774c0991b)

---
