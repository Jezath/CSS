# Sombras

---

- [Sombras de texto](#sombras-de-texto)
- [Sombras de caja](#sombras-de-caja)
- [Sombas multiples](#sombas-multiples)
- [Sombras identicas](#sombras-identicas)

---

### Sombras de texto

Crear sombras en textos mediante CSS es muy útil, puesto que es una forma interesante de suavizar y hacer más legibles los textos, o simplemente hacerlos más atractivos para el usuario que está viendo la página. Para ello, utilizaremos la propiedad text-shadow. Esta propiedad permite los siguientes parámetros:


| Propiedad     | Valor         | Significado                                                                 |
|---------------|---------------|-----------------------------------------------------------------------------|
| `text-shadow`   | none          | No aplica ninguna sombra en el texto (o la quita si existía previamente).  |
| text-shadow   | desplazamiento horizontal y vertical | Aplica sombra color negro, desplazándola horizontal y verticalmente.          |
| text-shadow   | desplazamiento + desenfoque         | Igual a la anterior, pero establece un desenfoque a la sombra (0 sin desenfoque). |
| text-shadow   | desplazamiento + desenfoque + color | Igual a la anterior, pero indicando un color personalizado para la sombra.     |


```html
<p class="text">hola</p>
```


```css
.text {
  font-size: 2rem;

  text-shadow: 4px 4px;             /* Equivalente a 4px 4px 0 black */
  text-shadow: 4px 4px 2px;         /* Equivalente a 4px 4px 2px black */

  /* text-shadow: moverX moverY desenfoque color */
  text-shadow: 4px 4px 5px #0005;
}
```

![](../img/text-shadow%201.png)


### Sombras de caja

Se denominan sombras sobre cajas a las sombras en CSS que se pueden crear en una etiqueta o elemento HTML. Para ello, se utiliza la propiedad `box-shadow`, que funciona de forma muy similar a la que vimos en las sombras de texto, sólo que con algunos añadidos interesantes.


#### Propiedad `box-shadow`


```html
<div class="box"></div>
```

```css
.box {
  background: red;
  width: 100px;
  height: 100px;

  /* box-shadow: moverX moverY desenfoque color */
  box-shadow: 10px 10px 0 black;
}
```

![](../img/box-shadow%201.png)

Tenemos otro valor que se usa solo en casos particulares cuando no tenemos sombras ni en X ni en Y, y es le de factor de crecimiento. 

Este valor va entre el `desenfoque` y el `color`.


```css
.box {
  background: red;
  width: 100px;
  height: 100px;´

  /* box-shadow: moverX  moverY  desenfoque  factordecrecimiento  color */
  box-shadow: 0 0 10px 15px black;
}
```

![](../img/box-shadow%202.png)


Por último tenemos el valor `inset` que se posiciona al final de todos y sirve para que la sombra tambien se aplique dentro del elemento.


```css
.box {
  background: red;
  width: 100px;
  height: 100px;

  /* box-shadow: moverX  moverY  desenfoque  factordecrecimiento  color  inset */
  box-shadow: 0 0 10px 15px #0006 inset;
}
```

![](../img/box-shadow%203.png)


Podemos usar valores negativos para invertir la posición de las sombras, además si tenemos el valor `inset` esta sombra se aplica dentro del elemento


```css
.box {
  background: red;
  width: 100px;
  height: 100px;

  box-shadow: -10px -10px 15px #0006 inset;
}
```

![](../img/box-shadow%204.png)


#### Sombas multiples

Podemos aplica varias sombras a la vez.


```css
.box {
  background: red;
  width: 100px;
  height: 100px;

  /* sombras multiples */
  box-shadow: 
    0 0 20px 10px #0006 inset, /* sombras 1 */
    20px 20px 10px #0006,      /* sombras 2 */
    -10px -10px 10px indigo;   /* sombras 3 */
}
```

![](../img/box-shadow%205.png)


### Sombras identicas

Existe una función menos conocida denominada `drop-shadow()` que puede utilizarse mediante la propiedad `filter` y que permite crear las llamadas sombras idénticas.

#### La función drop-shadow()

Como hemos comentado, para crear sombras idénticas se debe utilizar la función `drop-shadow()` que es una función que puede utilizarse en la propiedad `filter` (no es una propiedad independiente) y que tiene la misma sintaxis exacta de text-shadow.


```html
<img class="bat"
src="https://lenguajecss.com/css/sombras/drop-shadow/batmanz.png" >
```


```css
.bat {
  border: 1px solid;

  /* drop-shadow(moverX  moverY  desenfoque  color) */
  filter: drop-shadow(20px 20px 5px #0006);
}
```

![](../img/filter%20drop-shadow%201.png)

---
