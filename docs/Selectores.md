# Selectores

En CSS tenemos varias formas de seleccionar elementos:

![selectores](https://lenguajecss.com/css/selectores/atributos/sintaxis-atributos.png)

### Selector directo por elemento `<p>`

Selecciona el elemento usando directamente la etiqueta HTML.

```html
<p>Hola</p>
```

```css
p {
  color: red;
}
```

### Selector por clases `.`

Usamos el atributo `class` en las etiquetas HTML, esta clase se puede repetir en los elementos que queramos y los estilos se aplicarán a todos los elementos que tengan esa clase.

```html
<p class="parrafo">Hola</p>
```

```css
.parrafo {
  color: blue;
}
```

### Selector por id `#`

Este selector se usa para identificar elementos únicos, es decir el atributo `id` del elemento NO puede repetirse en otro elemento HTML.

```html
<p id="texto">Hola</p>
```

```css
#texto {
    color: green;
}
```

### Selector por atributos `type`

Podemos buscar elementos que tengan un determinado atributo HTML. Puede indicarle a CSS que busque atributos si encierra el selector entre corchetes cuadrados ([ ]).

```html
<div data-type="primary"></div>
```

```css
[data-type='primary'] {
color: red;
}
```

También en lugar de buscar un valor específico de `data-type`, podemos buscar elementos que presenten el atributo, independientemente de su valor.

```html
<div data-type="primary"></div>
<div data-type="secondary"></div>
```

```css
[data-type] {
color: red;
}
```

Junto con los operadores de casos, tiene acceso a los operadores que buscan porciones coincidentes de cadenas dentro de los valores de los atributos.

```css
/* Un href que contiene "example.com" */
[href*='example.com'] {
  color: red;
}
/* Un href que comienza con https */
[href^='https'] {
  color: green;
}
/* Un href que termina con .com */
[href$='.com'] {
  color: blue;
}
```

### Selector universal `*`

El selector universal puede ser muy útil en algunos casos para resetear ciertas propiedades de todo un documento, como en el siguiente ejemplo, donde se eliminan los márgenes de todos los elementos del documento HTML, puesto que algunos navegadores ponen márgenes diferentes y esto puede producir ciertas inconsistencias en los diseños:

```css
/* Elimina márgenes y rellenos de todos los elementos de un documento HTML */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

---
