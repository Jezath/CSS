# Visibilidad de elementos

Existen múltiples formas de modificar la visibilidad de ciertos elementos de una página, donde hay 3 formas principales que destacan sobre otras. Vamos a analizar dichas formas, atendiendo a ciertos matices importantes:

|Propiedad|Descripción|
|---------|-----------|
|`display`|Modifica como se muestra un elemento. Con `none`, lo oculta.|
|`visibility`|Modifica como se muestra un elemento. Con `hidden`, lo oculta, pero mantiene su espacio visual.|
|`opacity`|Modifica el nivel de transparencia del elemento con un valor de 0% a 100%.|

### Propiedad `display`

Quizás, la forma más habitual y conocida de ocultar un elemento es utilizar la propiedad display con el valor `none`. Esto hace que el navegador ignore por completo ese elemento, dejándolo de mostrar visualmente.

```html
<div class="container">
  <div class="item item-1">1</div>
  <div class="item item-2">2</div>
  <div class="item item-3">3</div>
</div>
```

```css
.container {
  display: flex;
}

.item {
  width: 150px;
  height: 150px;
  background: indigo;
  margin: 10px;
  font-size: 4rem;
  display: grid;
  place-items: center;
  color: white;
}

.item-2 {
  display: none;
}
```

![](../img/display%20none.png)

### Propiedad `visibility`

Existe una propiedad CSS llamada `visibility`, mediante la cuál podemos establecer el valor `hidden`. Esto realizará una acción muy similar a `display: none`, con la diferencia que en este caso, se mantiene el «hueco» que ocupaba el elemento cuando se mostraba, pero manteniendo dicho espacio vacío (elemento oculto).

Dicha propiedad visibility tiene los siguientes valores posibles:

|Valor|Significado|
|---------|-----------|
|`visible`|El elemento es visible. Valor por defecto.|
|`hidden`|El elemento no es visible (pero sigue ocupando su espacio y posición).|
|`collapse`|Sólo utilizado en tablas. El elemento se contrae para no ocupar espacio.|

```html
<div class="container">
  <div class="item item-1">1</div>
  <div class="item item-2">2</div>
  <div class="item item-3">3</div>
</div>
```

```css
.container {
  display: flex;
}

.item {
  width: 150px;
  height: 150px;
  background: indigo;
  margin: 10px;
  font-size: 4rem;
  display: grid;
  place-items: center;
  color: white;
}

.item-2 {
  visibility: hidden;
}
```

![](../img/visibility%20hidden.png)

### Propiedad `opacity`

Por otro lado, otra opción interesante y relacionada podría ser la posibilidad de utilizar la propiedad `opacity`, especialmente útil si se utiliza junto a transiciones o animaciones.

La sintaxis de la propiedad opacity es la siguiente:

|Propiedad|Valor|Significado|
|---------|---------|-----------|
|`opacity`|`number`|Establece una transparencia con un valor del 0 al 1 (permite decimales).|
|`opacity`|`porcent`|Establece una transparencia con un valor del 0% al 100%.|

```html
<div class="container">
  <div class="item item-1">1</div>
  <div class="item item-2">2</div>
  <div class="item item-3">3</div>
</div>
```

```css
.container {
  display: flex;
}

.item {
  width: 150px;
  height: 150px;
  background: indigo;
  margin: 10px;
  font-size: 4rem;
  display: grid;
  place-items: center;
  color: white;
}

.item-2 {
  opacity: 50%;
}
```

![](../img/opacity%2050.png)

Como se puede ver en la demo, el efecto de la propiedad opacity al 50% hace que parezca que ese elemento está con un color más claro, sin embargo, lo que ocurre es que está semitransparente, porque hemos reducido la opacidad a la mitad.

>**Nota:** Recuerda que la propiedad `opacity` afecta al elemento indicado y a todos sus hijos.

---
