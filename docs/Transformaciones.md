# Transformaciones

---

- [Translaciones 2D](#translaciones-2d)
- [Rotaciones 2D](#rotaciones-2d)
- [Escalado 2D](#escalado-2d)
- [Transformaciones 3D](#transformaciones-3d)
- [Perspectivas CSS](#perspectivas-css)

---

Las transformaciones son una de las características de CSS más interesantes y potentes que se introducen en el lenguaje para convertir las hojas de estilo en un sistema capaz de realizar efectos visuales 2D y 3D. Con ellas podemos hacer cosas como mover elementos, rotarlos, aumentarlos o disminuirlos y otras transformaciones relacionadas o combinadas.

### Propiedad `transform`

Las transformaciones se pueden efectuar en CSS mediante la propiedad `transform` que permite recibir una función de transformación determinada, la cuál será aplicada en el elemento HTML en cuestión seleccionado mediante CSS. Dicho elemento HTML se verá transformado visualmente.

```html
<div class="element"></div>
```

```css
.element {
  width: 100px;
  height: 100px;
  background: indigo;
  transform: rotate(45deg);
}
```

![](../img/transform%201.png)


En este ejemplo, se aplica una función de transformación, concretamente `rotate()`, con un valor específico en grados.


### Funciones 2D

![](https://lenguajecss.com/css/transformaciones/transform/transform-css.png)


| Tipo de transformación | Descripción                                                                 |
|------------------------|------------------------------------------------------------------------------|
| Translación 2D         | Desplaza un elemento en el eje X (izquierda, derecha) y/o en el eje Y (arriba, abajo) |
| Escalado 2D            | Escala el elemento una determinada cantidad más grande o más pequeña. También se puede voltear. |
| Rotación 2D            | Gira el elemento sobre su eje X o sobre su eje Y. También se puede girar sobre sí mismo. |
| Deformación 2D         | Inclina el elemento sobre su eje X o sobre su eje Y.                        |


#### Transformaciones múltiples

Recuerda que si estableces varias propiedades transform en el mismo elemento con diferentes funciones de transformación, siguiendo la herencia y cascada que se aplica siempre en cualquier propiedad CSS, la segunda propiedad transform sobreescribirá a la anterior propiedad transform, perdiendo el valor de la primera y aplicando sólo el de la segunda:


```css
.element {
  transform: rotate(5deg);  /* No hace efecto */
  transform: scale(2);      /* Sobreescribe la anterior */
}
```

Para evitar este comportamiento, se pueden emplear múltiples transformaciones separándolas mediante espacio. En el siguiente ejemplo, aplicamos una función de rotación, una función de escalado y una función de traslación de forma simultánea:


```css
.element {
  transform: rotate(5deg) scale(2) translate(25px, 150px);
}
```

Recuerda que también es posible usar propiedades personalizadas de CSS (variables CSS), permitiendo ser más flexibles a la hora de cambiar transformaciones:


```css
.element {
  --rotate-z: rotate(5deg);
  --scale: scale(2);
  --x: 25px;
  --y: 150px;

  transform: var(--rotate-z) var(--scale) translate(var(--x), var(--y));
}
```

#### Orden de transformación

Otro detalle que conviene tener en cuenta a la hora de aplicar múltiples transformaciones es que el orden de transformación importa. No es lo mismo realizar una rotación y luego una translación, que la misma translación primero y luego la misma rotación. Veámoslo en un ejemplo:


```html
<div class="element"></div>
```

```css
.element {
  width: 50px;
  height: 50px;
  background: grey;
  transform: translate(150px, 100px) rotate(25deg);
}
```

![](../img/transform%202.png)

En este primer ejemplo, trasladamos el elemento 150 píxels a la derecha y 100 píxels hacia abajo. Posteriormente, rotamos 50 grados el elemento sobre sí mismo.

Veamos que ocurre si alternamos el orden:

```css
.element {
  width: 50px;
  height: 50px;
  background: grey;
  transform: rotate(50deg) translate(150px, 100px);
}
```

![](../img/transform%203.png)

#### Punto de origen

La propiedad transform-origin nos permite cambiar el punto de origen de una transformación, cosa que en algunos casos puede resultar bastante útil. Dicha función recibe por parámetro la posición de origen de cada eje (X e Y), que podemos indicar, por ejemplo, con porcentajes, y que por defecto, está establecida a 50% 50%:


```html
<div class="element"></div>
<div class="element rotate"></div>
```

```css
.element {
  width: 50px;
  height: 150px;
  background: grey;
}

.rotate {
  transform: translate(150px, 0) rotate(45deg);
  transform-origin: 0% 0%;
}
```

![](../img/transform%204.png)


### Translaciones 2D

En 2D, existen tres funciones para mover elementos: translateX(), translateY() y translate(), que combina ambas. Valores positivos en X mueven a la derecha y en Y hacia abajo; valores negativos, a la izquierda y hacia arriba respectivamente.

| Funciones         | Significado                                              |
|-------------------|----------------------------------------------------------|
| translateX(x)     | Traslada el elemento una distancia de x horizontalmente. |
| translateY(y)     | Traslada el elemento una distancia de y verticalmente.   |
| translate(x, y)   | Propiedad de atajo de las dos anteriores.                |
| translate(x)      | Equivalente a translate(x, 0)                            |
| translateZ(z)     | Ver en Transformaciones 3D                               |
| translate3d(x,y,z)| Ver en Transformaciones 3D                               |


Por ejemplo, la propiedad transform: translate(20px, -30px) traslada el elemento 20 píxeles a la derecha y 30 píxeles hacia arriba, que es equivalente a utilizar transform: translateX(20px) translateY(-30px).


```css
.element {
  transform: translateX(20px) translateY(-30px);
}

/* La transformación anterior es equivalente a esta (atajo) */
.element {
  transform: translate(20px, -30px);
}
```

#### Ppropiedad `translate`

En nuevas versiones de los navegadores, ya se soporta la propiedad individual translate, y no hace falta utilizarla dentro de la propiedad transform.

| Propiedad | Valor     | Significado                                                       |
|-----------|-----------|-------------------------------------------------------------------|
| translate | none      | No aplica desplazamiento. Valor por defecto.                     |
| translate | (x)       | Desplaza un elemento el tamaño especificado en el eje X.         |
| translate | (x, y)    | Desplaza un elemento una cierta cantidad en el eje X y eje Y.    |
| translate | (x, y, z) | Desplaza un elemento en el eje X, eje Y y eje Z.                 |


```css
.element {
  translate: 50px;              /* Equivalente a translateX(50px) */
  translate: 50px 150px;        /* Equivalente a translate(50px, 150px) */
  translate: 0 150px;           /* Equivalente a translateY(150px) */
  translate: 50px 150px 100px;  /* Equivalente a translate(50px, 150px, 100px) */
  translate: 0px 0px 30px;      /* Equivalente a translateZ(30px) */
}
```


### Rotaciones 2D

Las funciones de rotación simplemente giran el elemento una cierta cantidad respecto al eje involucrado. Disponemos de las siguientes funciones de rotación:

| Funciones            | Significado                                                        |
|----------------------|---------------------------------------------------------------------|
| rotateX(x)           | Establece una rotación 2D en `angle` x sólo para el eje horizontal X.       |
| rotateY(y)           | Establece una rotación 2D en `angle` y sólo para el eje vertical Y.         |
| rotateZ(z)           | Establece una rotación 2D en `angle` z sobre sí mismo.                      |
| rotate(z)            | Alias a la anterior.                                                |
| rotate3d(x, y, z, a) | Ver en Transformaciones 3D                                          |


Por ejemplo, con transform: rotate(5deg) realizamos una rotación de 5 grados del elemento sobre si mismo. Utilizando rotateX() y rotateY() podemos hacer lo mismo respecto al eje X o el eje Y respectivamente.


```css
.element {
  transform: rotateX(30deg) rotateY(20deg);
}

.element {
  transform: rotateZ(5deg);
}
```

#### Propiedad `rotate`

En nuevas versiones de los navegadores, ya se soporta la propiedad individual rotate, y no hace falta utilizarla dentro de la propiedad transform.

Como se puede ver, se puede indicar 1 parámetro, 2 parámetros o 4 parámetros, dependiendo de la modalidad a utilizar. Veamos algunos ejemplos:


```css
.element {
  rotate: 45deg;        /* Equivale a transform: rotateZ(45deg);  */

  rotate: x 45deg;      /* Equivale a transform: rotateX(45deg);  */
  rotate: y 120deg;     /* Equivale a transform: rotateY(120deg); */

  rotate: 0 0 1 45deg;  /* Equivale a transform: rotateZ(45deg);  */
  rotate: 1 0 0 15deg;  /* Equivale a transform: rotateX(15deg);  */
  rotate: 0 1 1 5deg;   /* Equivale a transform: rotateY(5deg) rotateZ(5deg);  */
}
```

### Escalado 2D

Las funciones de escalado son aquellas que realizan una transformación en la que aumentan o reducen el tamaño de un elemento. Para ello, las utilizaremos en el interior de la propiedad CSS transform y elegiremos una de las siguientes funciones de escalado.

Disponemos de las siguientes funciones de escalado:


| Funciones          | Significado                                                                |
|--------------------|-----------------------------------------------------------------------------|
| scaleX(fx)         | Reescala el elemento un número de fx veces (sólo en horizontal).           |
| scaleY(fy)         | Reescala el elemento un número de fy veces (sólo en vertical).             |
| scale(fx, fy)      | Propiedad de atajo de las dos anteriores (escalado simétrico).             |
| scale(fx)          | Equivalente al anterior: scale(fx, fx).                                    |
| scaleZ(fz)         | Ver en Transformaciones 3D                                                 |
| scale3D(fx, fy, fz)| Ver en Transformaciones 3D                                                 |


#### Efecto espejo con CSS

Con la función de escalado de CSS se puede hacer un efecto «mirror» y darle la vuelta a una imagen, por ejemplo, de forma muy sencilla. Basta con utilizar la función scale(-1) con valor negativo. Si 1 representa a la imagen tal cual está, -1 es la imagen invertida.


```css
.image {
  transform: scaleX(-1);    /* Imagen espejo en horizontal */
  transform: scaleY(-1);    /* Imagen espejo en vertical (boca abajo) */

  transform: scale(-1);     /* Equivalente a las dos anteriores a la vez */
}
```

#### Propiedad `scale`

La propiedad scale en CSS se usa para escalar elementos en 2D o 3D, haciendo que se vean más grandes o más pequeños. Es parte de las funciones de transformación (transform).


```css
transform: scale(factor);
transform: scale(x, y);

transform: scale(1.5);
transform: scale(2, 0.5);
```

### Transformaciones 3D

Estas funciones, en la mayoría de los casos, no son más que la incorporación del eje Z a las anteriores que ya habíamos visto, además de la adición de una función de atajo 3D para poder utilizarlas todas de una sola vez.

Antes de comenzar a verlas, recordar siempre que el eje X es el eje horizontal, el eje Y es el eje vertical y el eje Z es el eje de profundidad. Varios conceptos que se deben tener claros antes de comenzar con el 3D en CSS:

![](https://lenguajecss.com/css/transformaciones/transform-3d/transform-axis-x-y-z.png)

Para utilizar transformaciones 3D es necesario conocer algunas propiedades derivadas de transformaciones, como por ejemplo, las siguientes:


| Propiedades       | Formato               | Significado                                                   |
|-------------------|------------------------|----------------------------------------------------------------|
| transform-style   | flat \| preserve-3d    | Modifica el tratamiento 3D de los elementos hijos.            |
| transform-origin  | posX posY posZ  | Cambia el punto de origen del elemento en una transformación. |

Por defecto, la propiedad transform-style está establecida a flat, o lo que es lo mismo, trata los elementos como elementos 2D, por lo que no podemos usar 3D, salvo que lo indiquemos expresamente con el valor preserve-3d. De esta forma, todos los elementos hijos del elemento que tenga esa propiedad, se tratarán como elementos 3D:



```css
.container {
  transform-style: preserve-3d;
  transform: rotateX(2deg) rotateY(2deg) rotateZ(2deg);
  perspective: 300px;
}
```

En este ejemplo, se usa transform-style: preserve-3d en el elemento padre .container para permitir que los hijos .element se transformen en un espacio tridimensional. Además, se aplica una rotación en los tres ejes y una perspective para mejorar el efecto 3D (que se explicará más adelante).

Por otro lado, transform-origin se usa con tres valores para establecer el punto de origen también en el eje Z. En este eje, solo se pueden usar valores absolutos (como píxeles), no porcentajes.

### Perspectivas CSS

Cuando trabajamos con 3D en CSS, en muchas ocasiones es necesario dotar a nuestro trabajo de perspectiva. Con la propiedad perspective de CSS podemos establecer un punto de fuga con una cierta distancia:


| Propiedades         | Formato                | Significado                                         |
|---------------------|------------------------|-----------------------------------------------------|
| `perspective`         | none \| `size` distance       | Punto de fuga para los elementos hijos.            |
| `perspective-origin`  | 50% 50% \| `position` posX posY   | Punto de origen de la perspectiva.                 |


La propiedad `perspective` nos permite darle un determinado punto de fuga al elemento hijo de un contenedor (debemos utilizarlo desde el contenedor padre), y se le aplica una cierta distancia, por ejemplo 400px. Mediante la propiedad `perspective-origin` podemos cambiar el punto de origen de la perspectiva, y con backface-visibility, podemos ocultar la cara «trasera» de un elemento, como explicaremos más adelante.


#### Propiedad perspective

Por defecto, la propiedad `perspective-origin` tiene un valor de 50% 50%, pero podemos cambiar estos valores (eje x y eje y) que representan el desplazamiento del origen de la perspectiva desde el punto superior izquierda del contenedor de referencia.

Al margen de cantidades, por ejemplo, en píxeles, también podemos indicar  o valores como `top`, `bottom`, `left`, `right` o `center`.

Veamos un pequeño ejemplo donde se puede ir disminuyendo y ampliando el valor de perspective para ver como influye:


```html
<div class="container">
  <div class="element"></div>
</div>
```

```css
.container {
  width: 150px;
  height: 150px;
  transform-style: preserve-3d;
  perspective-origin: 50% 50%;
  perspective: 400px;
  border: 3px solid #888;
}

.element {
  width: 100%;
  height: 100%;
  background: red;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotateY(0);
  }
  100% {
    transform: rotateY(360deg);
  }
}
```

![](../img/perspective%201.png)


#### Propiedad backface-visibility

Es posible que cuando tengamos un espacio 3D con elementos HTML, perspectiva y transformaciones, queramos que el elemento gire y en un momento concreto se visualice la cara A de nuestro elemento (una imagen, un cubo, etc...) y cuando haya girado completamente se vea la cara B del elemento.

Por la forma en la que trabaja CSS, puede que eso no ocurra y se vea siempre la misma cara, ya que no estamos trabajando con objetos 3D reales. Para ello, podemos utilizar la propiedad backface-visibility.

| Propiedades           | Formato         | Significado                                           |
|-----------------------|-----------------|-------------------------------------------------------|
| backface-visibility   | visible \| hidden | Oculta la cara posterior de un elemento 3D.           |


```html
<div class="container">
  <img class="a-side" src="manzdev-a.gif" alt="A side">
  <img class="b-side" src="manzdev-b.png" alt="B side">
</div>
```


```css
.container {
  width: 180px;
  height: 180px;
  position: relative;
  animation: spin 2s linear infinite;
  transform-style: preserve-3d;
}

.container img {
  width: 100%;
  height: 100%;
  position: absolute;
}

@keyframes spin {
  0% {
    transform: rotateY(0);
  }
  100% {
    transform: rotateY(360deg);
  }
}
```

![](../img/backface-visibility%201.png)

Si nos fijamos en este ejemplo, hemos creado dos imágenes dentro de un contenedor. Ambas están posicionadas de forma que estarán superpuestas y si les aplicamos una animación que rote el contenedor en 360 grados sobre el eje Y, podremos comprobar que siempre veremos la imagen B, la última de ellas puesto que es la que tiene preferencia porque es la última que aparece en el orden de HTML.

Si ahora le añadimos la propiedad backface-visibility a hidden en la imagen B, entonces el navegador la ocultará cuando detecte que se encuentra en la cara posterior, simulando el 3D real:


```css
.container {
  width: 180px;
  height: 180px;
  position: relative;
  animation: spin 2s linear infinite;
  transform-style: preserve-3d;
}

.container img {
  width: 100%;
  height: 100%;
  position: absolute;
}

img.b-side {
  backface-visibility: hidden;
}

@keyframes spin {
  0% {
    transform: rotateY(0);
  }
  100% {
    transform: rotateY(360deg);
  }
}
```

![](../img/backface-visibility%202.png)

---
