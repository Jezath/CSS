# Nesting

CSS es un lenguaje maravilloso, expresivo y muy fácil de entender y aprender. Sin embargo, a la misma vez, es un lenguaje díficil de dominar y muy complejo de organizar. Si llevas algo de tiempo escribiendo código CSS, te habrás dado cuenta que es muy fácil que el código de CSS crezca mucho y muy rápidamente.

![](https://lenguajecss.com/css/calidad-de-codigo/css-nesting/css-nesting.png)

Veamos un ejemplo muy sencillo. Con CSS tradicional, utilizando selectores CSS nuestro código se vería así:

```css
.container {
  width: 800px;
  height: 300px;
  background: grey;
}

.container .item {
  height: 150px;
  background: orangered;
}
```

Utilizando CSS Nesting, sin embargo, conseguimos que sólo mirando el código se haga evidente cuando un elemento está dentro de otro, aislando código, haciendo mucho más fácil de mantener y modularizar nuestros estilos:

```css
.container {
  width: 800px;
  height: 300px;
  background: grey;

  .item {
    height: 150px;
    background: orangered;
  }
}
```

### Sintaxis simple (relaxed)

La sintaxis más sencilla que podemos utilizar es la que mostramos en el ejemplo anterior. Simplemente, dentro de un elemento, podemos volver a mencionar otro. Sin embargo, aunque es más sencilla y sirve para casos simples, esta sintaxis puede tener ciertas limitaciones.

```css
.container {
  background: grey;

  .item {
    background: indigo;
  }
}
```

El anidamiento de `.item` corresponde al selector `.container .item.` Sin embargo, hay varios casos donde este anidamiento no funcionaría y tendríamos que utilizar el selector `&`.

### Sintaxis avanzada

Dentro del CSS Nesting tenemos el operador `&`, que nos permite hacer referencia al selector inmediatamente padre dentro del anidamiento. Esto puede resultarnos muy útil en algunos casos diferentes al anterior. Observa el siguiente ejemplo, donde en lugar de la clase `.item` seleccionamos cualquier elemento `div` que esté dentro de `.container`:

```css
.container {
  background: grey;

  & div {
    background: indigo;
  }
}
```

>**Nota:** El ejemplo anterior, sin el selector `&` es imposible de realizar con CSS Nesting, puesto que la sintaxis simple no permite colocar elementos directos que no sean clases, id, combinadores, etc.

Otra situación problemática podría ser el caso en el que queramos darle estilo a la clase .container cuando tenemos el ratón encima de ella. Observa el siguiente fragmento de código donde conseguimos un selector equivalente a .container:hover:

```css
.container {
  background: grey;

  &:hover {
    background: indigo;
  }
}
```

>**Nota:** Si omitimos el selector `&` en este ejemplo anterior, el código CSS será válido, pero no equivalente. Omitiendo el selector `&` estaríamos obteniendo el selector equivalente `.container` `:hover` en lugar de `.container:hover`. Es decir, estaríamos aplicando estilos `:hover` a los elementos dentro de .container en lugar de al propio `.container`.


### Anidamiento sobre el padre

En los casos anteriores siempre hemos colocado el selector `&` al principio. Sin embargo, puede darse el caso que queramos anidar de una forma diferente. En el siguiente ejemplo, el selector equivalente sería `.item` `.container`, es decir, elementos `.item` que contengan al padre:


```css
.container {
  width: 800px;
  height: 300px;
  background: grey;

  .item & {
    background: green;
    height: 100px;
  }
}
```

### Anidamiento de reglas

Es posible anidar reglas CSS en el interior de bloques de código CSS donde se aplica CSS Nesting. Concretamente, es posible hacerlo si se trata de reglas @media, @supports, @layer, @scope o @container. De esta forma, podemos organizar, por ejemplo, código responsive de un fragmento de código de forma muy compacta:


```css
.container {
  height: 200px;
  background: grey;

  @media (orientation: landscape) {
    height: 100vh;
  }
}
```

En este caso, el código del interior de la regla `@media` se le aplica al elemento `.container`, simplificando mucho la sintaxis y haciéndolo más fácil de organizar.

---

Regresar al [README](../README.md)