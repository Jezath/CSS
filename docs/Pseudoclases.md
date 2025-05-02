# Pseudoclases

---

- [Tipos de pseudoclases CSS](#tipos-de-pseudoclases-css)
- [Pseudoclases de interaccion](#pseudoclases-de-interaccion)
- [Pseudoclases de ubicacion](#pseudoclases-de-ubicacion)
- [Pseudoclases de idiomas](#pseudoclases-de-idiomas)
- [Pseudoclases de estructura](#pseudoclases-de-estructura)
- [El primer y ultimo hijo](#el-primer-y-ultimo-hijo)
- [Hijos específicos](#hijos-especificos)
- [Hijos (del mismo tipo)](#hijos-del-mismo-tipo)
- [Hijos específicos (del mismo tipo)](#hijos-específicos-del-mismo-tipo)
- [Elementos unicos o sin hijos](#elementos-unicos-o-sin-hijos)
- [Pseudoclases de formularios](#pseudoclases-de-formularios)
- [pseudoclase :modal](#pseudoclase-modal)
- [Pseudoclases para buscar o excluir elementos](#pseudoclases-para-buscar-o-excluir-elementos)

---

Las pseudoclases se utilizan para hacer referencia a elementos HTML que tengan un cierto comportamiento concreto. Volvamos a recordar el esquema general de sintaxis de CSS, donde ahora añadiremos las pseudoclases, que se definen añadiendo dos puntos antes del nombre de la pseudoclase concreta, de la siguiente forma:

![](https://lenguajecss.com/css/pseudoclases/que-son/sintaxis-pseudoclases.png)


### Tipos de pseudoclases CSS

| **Pseudoclase**           | **Significado**                                                   |
|---------------------------|-------------------------------------------------------------------|
| **Interacción**            | Pseudoclases relacionadas con acciones de usuario.               |
| :hover, :active, :focus, :focus-within, :focus-visible |                                      |
| **Ubicación**              | Pseudoclases relacionadas con enlaces o ubicaciones.             |
| :any-link, :link, :visited, :target |                                                         |
| **Idioma**                 | Pseudoclases relacionadas con idiomas.                           |
| :lang(), :dir()            |                                                                  |
| **Estructura**             | Pseudoclases de estructura de documentos HTML.                   |
| :root, :host, :defined, :empty |                                                              |
| :first-child, :last-child, :only-child |                                                      |
| :first-of-type, :last-of-type, :only-of-type |                                                |
| :nth-child(), :nth-last-child(), :nth-of-type(), :nth-last-of-type() |                        |
| **Formulario**             | Pseudoclases de formularios HTML.                                |
| :checked, :indeterminate    |                                                                 |
| :enabled, :disabled, :read-only, :read-write, :placeholder-shown, :default |                  |
| :required, :optional, :valid, :invalid, :user-valid, :user-invalid |                          |
| :in-range, :out-of-range   |                                                                  |
| **Estado**                 | Pseudoclases relacionadas con el estado de modales o similares.  |
| :fullscreen, :modal        |                                                                  |
| **Paginado**               | Pseudoclases de paginado de documentos HTML.                     |
| :first, :left, :right, :blank |                                                               |

### Pseudoclases de interaccion

Las pseudoclases de interacción se pueden utilizar en cualquier elemento, aunque lo más frecuente es usarlo en elementos interactivos como enlaces, botones o similares, y pueden seleccionar elementos cuando ocurre una cierta interacción por parte del usuario en ellos. ¿Qué tipo de interacción es esa? Pueden ser varias:

| Pseudoclase         | Descripción                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `:hover`              | Selecciona el elemento si el usuario pasa el ratón sobre dicho elemento.     |
| `:active`             | Selecciona el elemento si el usuario se encuentra pulsando dicho elemento.  |
| `:focus`              | Selecciona el elemento cuando tiene el foco (está en primer plano).         |
| `:focus-within`       | Selecciona el elemento si uno de sus miembros hijos ha ganado el foco.      |
| `:focus-visible`      | Selecciona el elemento cuando tiene el foco sólo de forma visible.          |


#### Pseudoclase `:hover`

`:hover` es muy útil e interesante, ya que permite aplicar estilos a un elemento justo cuando el usuario pasa el ratón (o más concretamente, un dispositivo apuntador) sobre él. Es una de las pseudoclases más utilizadas:

```css
/* Usuario mueve el ratón sobre un enlace, cambia su color */
a:hover {
  background-color: cyan;
  padding: 2px
}

/* Usuario mueve el ratón sobre un div y resalta todos los enlaces que contiene */
div:hover a {
  background-color: steelblue;
  color: white;
}
```

Observese que podemos realizar acciones un poco más específicas, como el segundo ejemplo anterior, donde al movernos sobre un elemento div (div:hover), aplicaremos los estilos a los enlaces (a) que están dentro del mencionado div.


#### Pseudoclase `:active`

Por otro lado, la segunda pseudoclase, :active, permite resaltar los elementos que se encuentran activos, o lo que es lo mismo, elementos que están siendo pulsados en ese instante con el ratón por el usuario:

```css
a:active {
  border: 2px solid #FF0000;
  padding: 2px
}
```

Ejemplo aplicando :active

```html
<div class="wrapper">
  <button class="button">Click and hold to see the active state</button>
</div>
```

```css
/* Cuando el usuario mantiene presionado el click el tamaño del botón se hace más pequeño */
.button:active {
  transform: scale(0.99);
  box-shadow: none;
}
```

> **Nota:** Aunque estas pseudoclases se inventaron para interactuar con un ratón en un sistema de escritorio, pueden llegar a funcionar en dispositivos táctiles. Aún así, ten en cuenta que el :hover no tiene demasiado sentido en el contexto de dispositivos móviles, ya que un usuario no navega por móvil arrastrando el dedo por la pantalla continuamente.

#### Pseudoclase `:focus`

Cuando estamos escribiendo en un campo de texto de un formulario de una página web, generalmente pulsamos `TAB` para cambiar al siguiente campo y `SHIFT` + `TAB` para volver al anterior. Cuando estamos posicionados en un elemento, se dice que ese elemento **tiene el foco**, mientras que al pulsar `TAB` y saltar a otro, solemos decir que **pierde el foco**. También es posible ganar o perder el foco pulsando con el ratón en un elemento.

```css
/* El campo ha ganado el foco */
input:focus {
  border: 2px dotted #444
}
```

Estas pseudoclases suelen utilizarse con elementos de formularios como `<input>`, `<textarea>` o similares, pero también pueden utilizarse con otros elementos, como por ejemplo enlaces `<a>`. Esta es una excelente oportunidad para personalizar el estilo de los campos de texto de un formulario (`<input>` y `<textarea>`) para que cambien cuando el usuario escribe y se mueve por ellos.

La pseudoclase :focus tiene dos variaciones concretas, las explicaremos a continuación.

#### Pseudoclase `:focus-within`

La pseudoclase `:focus-within` permite darle estilo no sólo al elemento que tiene el foco, sino también a los elementos contenedores relacionados con el elemento que gana el foco. En este ejemplo, `:focus-within` permite que cuando uno de los campos `<input>` del formulario gane el foco, podamos iluminar también el elemento label, que es su contenedor:

```html
<form>
  <label>Name: <input type="text"></label>
  <label>Email: <input type="text"></label>
</form>
```

```css
form :focus-within {
  background: yellow;
}
```

![](../img/pseudoclase%20focus-within.png)


#### Pseudoclase `:focus-visible`

En el caso de la pseudoclase `:focus-visible` es prácticamente idéntico a `:focus`, solo que podemos aplicar estilos al elemento que gana el foco, pero sólo cuando se ha ganado el foco exclusivamente de forma visible, como por ejemplo, pulsando la tecla `TAB` y accediendo al elemento. Esto puede resultar muy útil cuando quieres que el foco coincida con un tema visual para la página.

### Pseudoclases de ubicacion

Existen algunas pseudoclases orientadas a los enlaces o hipervínculos. En este caso, permiten cambiar los estilos dependiendo del comportamiento del enlace. Entre ellas, se encuentran las siguientes:

| Pseudoclase  | Descripción                                                              |
|--------------|--------------------------------------------------------------------------|
| `:any-link`    | Selecciona un elemento que es un enlace.                                 |
| `:link`        | Selecciona un elemento que es un enlace no visitado aún.                 |
| `:visited`     | Selecciona un elemento que es un enlace visitado anteriormente.         |
| `:target`      | Selecciona un elemento que coincide con el ancla de la URL actual.      |

#### Pseudoclase `:any-link`

Con la pseudoclase `:any-link` se puede hacer referencia, como dice su nombre, a elementos que sean cualquier tipo de enlaces. En este caso, y si no se delimitan de alguna forma, incluye etiquetas `<a>` y `<area>`, ya que ambas se consideran enlaces.

```css
:any-link {
  background: indigo;
  color: white;
  padding: 5px;
}
```

#### La pseudoclase `:link`
Por otro lado, la pseudoclase `:link` permite seleccionar enlaces a páginas que aún no han sido visitadas por el navegador del usuario, lo que puede ser interesante para personalizar el color de este tipo de enlaces. Por defecto, estos enlaces sin visitar suelen ser de color **azul**.

Veamos un ejemplo donde los cambiamos:

```css
a:link {
  color: green;
  font-weight: bold
}
```

#### La pseudoclase `:visited`
También tenemos la pseudoclase `:visited`, que se utiliza para seleccionar y dar estilo a los enlaces que **hayan sido visitados previamente** en el navegador del usuario. Por defecto, estos enlaces suelen ser de color **violeta**.

```css
a:visited {
  color: purple;
  font-weight: bold;
}
```

#### La pseudoclase `:target`
Con la pseudoclase `:target` podemos seleccionar un elemento HTML donde su `id` (ancla) coincida con el ancla que tenemos actualmente en la URL de navegación. Es decir, si en nuestra URL tenemos el ancla `#section1`, entonces se seleccionará el elemento con `id="section1"`:

```css
:target {
  background: gold;
  color: #333;
  padding: 5px;
}
```

> **Nota:** El orden es importante.
Si defines un estilo :visited, una pseudoclase de vínculo con al menos la misma especificidad puede anularlo. Por este motivo, se recomienda que uses la regla LVHA para aplicar diseño a los vínculos con pseudoclases en un orden particular: `:link`, `:visited`, `:hover`, `:active`.

### Pseudoclases de idiomas

En CSS podemos encontrarnos con varias pseudoclases relacionadas con el idioma utilizado en la página o en los elementos HTML en cuestión.

| Pseudoclase    | Significado                                                          |
|----------------|----------------------------------------------------------------------|
| `:lang(es)`      | Selecciona elementos con el idioma español, es decir, atributo lang="es". |
| `:dir(value)`    | Selecciona elementos con la dirección indicada (ltr o rtl).           |

#### La pseudoclase `:lang()`

El atributo HTML **lang** permite indicar en una etiqueta HTML el idioma en el que está el contenido de sus elementos hijos. De esta forma, un atributo `lang="es"` indica que el contenido de esa etiqueta se encuentra generalmente en español.

La pseudoclase `:lang()` acepta por parámetro un idioma (o una lista de ellos separados por comas) para seleccionar el elemento HTML que coincida con uno de ellos:

```css
/* Selecciona el elemento que tenga el idioma español */
:lang(es) {
  /* ... */
}

/* Selecciona elementos que estén en español o inglés (*y relacionados*) */
:lang(es, es-*, en, en-*) {
  /* ... */
}
```

### Pseudoclases de estructura

Existe una amplia gama de pseudoclases que permiten seleccionar elementos de un documento HTML según su posición y/o estructura en el documento. Vamos a dividirlas en varias categorías y analizarlas detalladamente.

#### La pseudoclase `:root`

La pseudoclase `:root` hace referencia al elemento raíz del documento HTML, o lo que es lo mismo, la etiqueta `<html>`. Sin embargo, en muchas ocasiones veremos que en lugar de utilizar directamente la etiqueta, se utiliza la pseudoclase `:root`. Al ser una pseudoclase, tiene una especificidad CSS más alta (0,1,0) que el elemento html, el cuál, al ser una etiqueta HTML, tiene una especificidad más baja (0,0,1):

```css
:root {
  background: black;
}

html {
  background: red;
}
```

### El primer y ultimo hijo

#### Pseudoclase `:first-child`

Con la pseudoclase `:first-child` podemos seleccionar el primer elemento (o primeros elementos) de un grupo de elementos al mismo nivel.

```html
<ul>
  <li>Primero</li> /* elemento color rojo */
  <li>Segundo</li>
  <li>Tercero</li>
</ul>
```

```css
li:first-child {
  color: red;
}
```

#### Pseudoclase `:last-child`

De la misma forma, con la pseudoclase `:last-child` podemos seleccionar el último elemento (o últimos elementos). Funciona exactamente igual que :first-child pero haciendo referencia al último elemento en lugar del primero.

```html
<ul>
  <li>Primero</li>
  <li>Segundo</li>
  <li>Tercero</li> /* elemento color azúl */
</ul> 
```

```css
li:last-child {
  color: blue;
}
```

Veamos esto con un gráfico en forma de árbol que hará que el ejemplo sea más visual:

```css
strong:first-child {
  background-color: cyan;
}

strong:last-child {
  background-color: green;
}
```

![](https://lenguajecss.com/css/pseudoclases/estructura/first-last-child.png)

### Hijos especificos

Sin embargo, con las pseudoclases anteriores sólo podemos seleccionar los primeros y últimos elementos, y podríamos necesitar un elemento específico, como el tercero o el quinto, por ejemplo. Para ello, podemos utilizar pseudoclases funcionales como `:nth-child()` o `:nth-last-child()`.

#### Pseudoclase `:nth-child()`

La pseudoclase `:nth-child(A)` permite especificar el elemento hijo deseado, simplemente estableciendo su número en el parámetro **A**.

```html
<ul>
  <li>Primero</li>
  <li>Segundo</li> /* elemento color verde */
  <li>Último</li> 
</ul>
```

```css
li:nth-child(2) {
  color: green;
}
```

Veamos además un ejemplo gráfico:

![](https://lenguajecss.com/css/pseudoclases/estructura/nth-child.png)


#### Pseudoclase `:nth-last-child()`

La pseudoclase funcional `:nth-last-child(A)` funciona de forma muy similar a la anterior, permitiendo también indicarle un parámetro A donde específicar una expresión o número para indicar el hijo concreto.

La diferencia respecto a la anterior, es que comenzamos a contar desde el final, de modo que el elemento número 2, sería el segundo empezando a contar desde el final.

### Hijos (del mismo tipo)

En los casos anteriores, seleccionamos elementos independientemente de que tipo de elemento sea. Simplemente, hacemos caso a la posición donde está ubicado. Y en algún caso, si no coincide la posición con el tipo de elemento especificado en el selector, simplemente no lo selecciona.

Una forma de actuar, quizás, más predecible para nosotros, es que queramos hacer referencia sólo a elementos del mismo tipo, ignorando el resto. Para ello, utilizaremos los selectores siguientes, análogos a los que ya hemos visto, pero haciendo referencia sólo a elementos del mismo tipo:

#### Pseudoclase `:first-of-type`

Por ejemplo, la pseudoclase `:first-of-type` es la análoga a :first-child, sólo que tendrá en cuenta sólo elementos de su mismo tipo. Observa el siguiente ejemplo donde no sólo tenemos `<div>`, sino que también tenemos un `<p>`:

```html
<div class="container">
  <div class="element">Element 1</div>
  <div class="element">Element 2</div>
  <p class="element">Element 3</p>
  <div class="element">Element 4</div>
</div>
```

```css
/* Selecciona "Element 1" */
.container div:first-of-type {
  background: gold;
}

/* Selecciona "Element 3" */
.container p:first-of-type {
  background: lime;
}

/* Selecciona los dos anteriores */
.container :first-of-type {
  border: 2px solid black;
}
```

![](../img/pseudoclase%20first-of-type.png)

#### Pseudoclase `:last-of-type`

De la misma forma, la pseudoclase `:last-of-type` es la análoga a :last-child, que selecciona el último elemento, pero igual que :first-of-type sólo teniendo en cuenta elementos del mismo tipo.

```html
<div>
  <p>Primer párrafo</p>
  <p>Segundo párrafo</p>
  <span>Un span</span>
  <p>Último párrafo</p> <!-- Este es el elemento modificado -->
</div>
```

```css
p:last-of-type {
  color: orange;
}
```

### Hijos específicos (del mismo tipo)

Ahora que estamos en la categoría en la que queremos seleccionar elementos del mismo tipo, también nos puede interesar seleccionar elementos específicos. Para ello, tenemos también dos pseudoclases análogas a las anteriores:

#### Pseudoclase `:nth-of-type()`

La pseudoclase `:nth-of-type(A)` es la análoga a :nth-child(A). Se trata de una pseudoclase funcional que admite pasar parámetros, donde le podemos indicar un número (o cierta expresión) para ser mucho más específicos a la hora de seleccionar elementos del mismo tipo.

```html
<div class="container">
  <div class="element">Element 1</div>
  <div class="element">Element 2</div>
  <p class="element">Element 3</p>
  <div class="element">Element 4</div>
</div>
```

```css
/* Seleccionamos sólo el "Element 2", ya que no hay un segundo <p> */
.container :nth-of-type(2) {
  background: gold;
}
```

![](../img/pseudoclase%20nth-of-type().png)


#### Pseudoclase `:nth-last-of-type()`

La pseudoclase `:nth-last-of-type(A)` es la análoga a :nth-last-child(A). Veamos un nuevo ejemplo sobre el ejercicio anterior, utilizando ahora estas últimas pseudoclases que hemos visto:

![](https://lenguajecss.com/css/pseudoclases/estructura/nth-of-type.png)

En este gráfico, se puede ver como strong:nth-of-type(2) selecciona el segundo elemento strong en ambos casos, a pesar de que en el primero ocupa la tercera posición. En este caso se selecciona porque es el segundo elemento de su mismo tipo `<strong>`.

Por otro lado, strong:nth-last-of-type(1) hace una selección de forma inversa, empezando por el último elemento, por lo que elige el último elemento.

### Elementos unicos o sin hijos

Existen también varias pseudoclases para la gestión de hijos únicos. Son las siguientes:

#### Pseudoclase `:only-child`

La propiedad :only-child nos proporciona una forma de seleccionar los elementos que sean el único hijo de su elemento padre. Por lo tanto, si un contenedor tiene en su interior un sólo elemento hijo, podremos seleccionar y aplicar estilos.

```html
<div>
  <p>Un solo párrafo</p> <!-- Este es el elemento modificado -->
</div>
```

```css
p:only-child {
  color: blue;
}
```

En este caso, la pseudoclase :only-child selecciona el `<p>` solo si es el único hijo de su elemento padre.

El estilo color: blue; se aplica al `<p>` porque es el único hijo dentro del `<div>`. Si hubiera más elementos dentro de `<div>`, como otro `<p>` o cualquier otro tipo de elemento, la pseudoclase :only-child no aplicaría.

#### Pseudoclase `:only-of-type`

Además, como ha ocurrido anteriormente, también existe la pseudoclase `:only-of-type ` que es la análoga a la anterior, pero sólo para elementos del mismo tipo. En este caso, podríamos tener un contenedor que contiene varios elementos, pero todos son únicos en su tipo, por lo tanto podrían ser seleccionados.

```html
<div>
  <span>Un span</span>
  <p>Último párrafo</p> <!-- Este es el elemento modificado -->
</div>
```

```css
p:only-of-type {
  color: red;
}
```

#### Pseudoclase `:empty`

Selecciona los elementos que no tienen hijos, ni texto, ni otros nodos.

```html
<div>
  <p>Texto dentro del párrafo</p>
  <p></p> <!-- Este es el elemento modificado -->
</div>
```

```css
p:empty {
  background-color: yellow;
}
```

### Pseudoclases de formularios

Existe una serie de pseudoclases en CSS que pueden ser utilizadas para usar en formularios de una página web. Estas pseudoclases permiten seleccionar elementos para darle estilo dependiendo de temas relacionados con los formularios o los campos que están en el interior de un formulario.

- De **interacción en formularios**: Seleccionar elementos cuando cambia el estado de un elemento.
- De **estado en formularios**: Seleccionar elementos cuando se encuentran en un estado concreto.
- De **validación**: Seleccionar elementos si cumplen o no un cierto criterio de validación.

#### Pseudoclases de interacción

Las siguientes pseudoclases están orientadas a un estado específico de ciertos campos de un formulario que el usuario puede modificar. Estos campos pueden ser los siguientes elementos:

- Elementos de tipo radio `<input type="radio">`.
- Elementos de casilla de verificación `<input type="checkbox">`.

#### Pseudoclase `:checked`

La pseudoclase `:checked` permite seleccionar un elemento que ha sido marcado o seleccionado y entonces aplicarle estilo CSS. Por ejemplo, se podría utilizar el siguiente fragmento de código:

```html
<input type="checkbox" checked> <span>First option</span>
<input type="checkbox"> <span>Second option</span>
<input type="checkbox"> <span>Third option</span>
```

```css
input:checked + span {
  color: green;
}
```

![](../img/pseudoclase%20checked.png)

Este ejemplo está utilizando el combinador hermano adyacente + para darle formato al `<span>` que se encuentra a continuación de la casilla `<input>` seleccionada, ya sea de tipo radio o de tipo checkbox. De esta forma, los textos que acompañan al campo del formulario que hayan sido seleccionados, se mostrarán en verde.

Como detalle adicional, también pueden seleccionar los elementos de opción `<option>` de una lista seleccionable `<select>` que se encuentren seleccionados.

#### Pseudoclase `:indeterminate`

La pseudoclase :indeterminate se utiliza para seleccionar elementos que tienen un estado indeterminado donde no se sabe exactamente su estado. Hay tres situaciones donde esto puede ocurrir:

- Un `<input type="checkbox">` donde mediante Javascript se marca la propiedad .indeterminate a true.
- Varios `<input type="radio">` con el mismo atributo name y sin definir el atributo checked en ninguno de ellos.
- Un elemento `<progress>` donde no se define su valor y generalmente se muestra moviéndose de un lado a otro.

```html
<input type="checkbox"> <span>First option (Indeterminated)</span>
<input type="checkbox"> <span>Second option</span>
<input type="checkbox"> <span>Third option</span>
```

```css
:indeterminate + span {
  background: black;
  color: white;
  padding: 5px;
}
```

```javascript
const inputs = document.querySelectorAll("input");
inputs[0].indeterminate = true;
```

#### Pseudoclases de estado

Por norma general, los elementos de un formulario HTML están por defecto activados, aunque se pueden desactivar añadiendo el atributo disabled (es un atributo booleano, no lleva valor específico). Esto es una práctica muy utilizada para impedir al usuario escribir en cierta parte de un formulario porque, por ejemplo, no es aplicable.

| Pseudoclase          | Descripción                                                        |
|----------------------|--------------------------------------------------------------------|
| `:enabled`             | Selecciona cuando el campo del formulario está activado.           |
| `:disabled`            | Selecciona cuando el campo del formulario está desactivado.       |
| `:read-only`           | Selecciona cuando el campo es de sólo lectura.                     |
| `:read-write`          | Selecciona cuando el campo es editable por el usuario.            |
| `:placeholder-shown`   | Selecciona cuando el campo está mostrando un placeholder.         |
| `:default`             | Selecciona cuando el elemento tiene el valor por defecto.         |

#### Pseudoclase `:enabled`

Utilizando la autoexplicativa pseudoclase :enabled, podemos seleccionar elementos que se encuentren activados (comportamiento por defecto):

```html
<button>Botón activado</button>
<button disabled>Botón desactivado</button>
```

```css
button:enabled {
  background-color: green;
}
```

![](../img/pseudoclase%20enabled.png)


#### Pseudoclase `:disabled`

Sin embargo, lo más interesante de este tema viene al poder darle estilo a elementos desactivados con la pseudoclase `:disabled,` donde se seleccionan los elementos a los que se le ha añadido el atributo disabled:

```html
<button>Botón activado</button>
<button disabled>Botón desactivado</button>
```

```css
button:disabled {
  background-color: grey;
  cursor: not-allowed;
}
```

![](../img/pseudoclase%20disabled.png)

#### Pseudoclase `:read-only`

La pseudoclase `:read-only` selecciona aquellos elementos `<input>` de un formulario que están marcados con el atributo de sólo lectura **readonly**. La diferencia entre un campo con atributo **disabled** y un campo con atributo **readonly** es que la información del campo con **readonly** se enviará a través del formulario, mientras que la del campo con **disabled** no se enviará. Lo que tienen en común es que ambas están bloqueadas y no permiten modificar su valor, por lo que se suelen percibir como algo equivalente.

```css
input:read-only {
  background-color: darkred;
  color: white
}
```

#### Pseudoclase `:read-write`

Por otro lado, la pseudoclase :read-write es muy útil para dar estilos a todos aquellos elementos que son editables por el usuario, sean campos de texto `<input>` o `<textarea>`.

```css
input:read-write {
  background-color: green;
  color: white
}
```

De esta forma, todos los elementos `<input>` que sean de lectura y escritura (editables) se seleccionarán y será posible aplicarles estilo. Recuerda que la pseudoclase **read-write** también da estilos a elementos HTML que contengan el atributo **contenteditable**, como por ejemplo un párrafo editable por el usuario con dicho atributo:


```html
<p contenteditable>Mensaje editable</p>
```

```css
:read-write {
  background-color: cyan;
  color: black;
  padding: 5px;
}
```

![](../img/pseudoclase%20read-write.png)


#### Pseudoclase `:placeholder-shown`

Con la pseudoclase `:placeholder-shown` se nos permite seleccionar y dar estilo a los elementos que están actualmente mostrando un **placeholder**. Si no lo conoces, el término **placeholder** es un texto o imagen de muestra que se suele colocar para que el usuario conozca un ejemplo de la información que debe ir en esa zona.

En nuestro caso, se puede hacer con el atributo **placeholder** en elementos `<input>`:


```html
<input type="text" placeholder="usuario@gmail.com">
```

```css
input:placeholder-shown {
  background: #555;
  padding: 5px;
  border: 2px solid #000;
  color: white;
}
```

![](../img/pseudoclase%20placeholder-shown.png)

#### Pseudoclase `:default`

Con la pseudoclase `:default` podemos seleccionar los elementos de un formulario que se consideran que tienen, de alguna forma, un valor por defecto. Es decir:

- Elementos `<input type="checkbox">` o `<input type="radio">` que tienen el atributo checked.
- Elementos `<selected>` donde una de sus opciones tiene el atributo selected.
- Elementos `<button>` o `<input type="submit">` que son el botón por defecto del `<form>`.

Los elementos que coincidan con uno de estos casos, se podrían seleccionar con el siguiente código:

```css
:default {
  background: red;
  color: white;
  border: 3px solid red;
  accent-color: red;
}
```

#### Pseudoclases de validación

En HTML5 es posible dotar de capacidades de validación a los campos de un formulario, pudiendo interactuar con ellos desde Javascript o incluso desde CSS. Con estas validaciones podemos asegurarnos de que el usuario escribe en un campo de un formulario el valor esperado.

Existen algunas pseudoclases útiles para las validaciones, como por ejemplo las siguientes:

| Pseudoclase       | ¿Cuándo aplica estilos?                                              |
|-------------------|----------------------------------------------------------------------|
| `:required`         | Cuando el campo es obligatorio, o sea, tiene el atributo `required`. |
| `:optional`         | Cuando el campo es opcional (por defecto, todos los campos).        |
| `:valid`            | Cuando los campos cumplen la validación HTML5.                       |
| `:invalid`          | Cuando los campos no cumplen la validación HTML5.                    |
| `:user-valid`       | Idem a `:valid`, pero cuando el usuario ha interactuado.             |
| `:user-invalid`     | Idem a `:invalid`, pero cuando el usuario ha interactuado.           |
| `:in-range`         | Cuando los campos numéricos están dentro del rango.                  |
| `:out-of-range`     | Cuando los campos numéricos están fuera del rango.                  |


#### Pseudoclase `:required`

En un formulario HTML es posible establecer un campo obligatorio que será necesario rellenar para enviarlo. Por ejemplo, el DNI de una persona que va a matricularse en un curso, o el nombre de usuario de alta en una plataforma web para identificarse. Campos que son absolutamente necesarios.

Por lo general, los campos de un formulario son siempre opcionales. Para hacer obligatorio un campo, tenemos que indicar en el elemento HTML el atributo **required**, al cuál será posible darle estilo mediante la pseudoclase `:required`:


```html
Nombre: <input type="text" required>
Apellidos: <input type="text">
Nickname: <input type="text" required>
```

```css
input:required {
  border: 2px solid red;
}
```

![](../img/pseudoclase%20required.png)

#### Pseudoclase `:optional`

Por otra parte, los campos opcionales son todos aquellos que no tienen el atributo required. Pueden seleccionarse con la pseudoclase `:optional`:


```html
Nombre: <input type="text" required>
Apellidos: <input type="text">
Nickname: <input type="text" required>
```

```css
input:optional {
  border: 2px solid blue;
}
```

![](../img/pseudoclase%20optional.png)


#### Pseudoclase `:invalid`

De forma opuesta, se pueden seleccionar elementos y aplicar ciertos estilos si no se cumple el patrón de validación, utilizando la pseudoclase `:invalid`:

```css
input:invalid {
  background-color: darkred;
  color: white;
}
```

#### Pseudoclase `:user-valid`

La pseudoclase :user-valid es una versión particular de :valid, donde el elemento se selecciona si, además de comprobar que la validación es correcta y se cumple, el usuario ha interactuado con anterioridad con el campo en cuestión.

#### Pseudoclase `:user-invalid`

De la misma forma, :user-invalid es una versión particular correspondiente a la pseudoclase :invalid. Mientras que :invalid permite seleccionar los elementos que no cumplen la restricción de la validación, :user-invalid permite seleccionar los elementos que no cumplen la validación pero que además el usuario ha interactuado anteriormente con ellos.


#### Pseudoclase `:in-range`

Pero ten en cuenta que en una validación numérica, donde un usuario podría escribir **500** en el campo de edad, sería un resultado que no nos gustaría aceptar. En el patrón de validación del atributo **pattern** indicamos «una o más cifras del 0 al 9», pero no establecemos unos límites.

Lo ideal sería establecer un rango, algo que se suele hacer muy a menudo si tenemos campos numéricos de formulario mediante los atributos **min** y **max**:

```html
<input type="number" name="age" min="18" max="100" />
```

Este campo permite al usuario especificar su edad, utilizando los atributos de validación min y max, que sólo permiten valores entre 18 y 100 años. De esta forma, si escribimos la pseudoclase :in-range podremos seleccionar los elementos que indican un valor y cumplen la validación:

```css
input:in-range {
  background-color: green;
  color: white;
}
```

#### Pseudoclase `:out-of-range`
La pseudoclase `:out-of-range`, por otro lado, permite seleccionar y dar estilo a los elementos que tienen valores fuera del rango definido, y por lo tanto, no son válidos.

De la misma forma que antes, es posible aplicar estilos para los valores fuera de rango:

```css
input:out-of-range {
  background-color: darkred;
  color: white;
}
```

#### Pseudoclases de estado

Existen una serie de pseudoclases para comprobar el estado visual de un elemento que se considera modal, es decir, que «centran» la interacción del usuario en un elemento principal (y sus hijos) y no permiten la interacción con otros elementos hasta que se cierre ese elemento principal.

#### Pseudoclase `:fullscreen`

Mediante la pseudoclase :fullscreen podemos seleccionar elementos que se encuentren en modo pantalla completa, lo que habitualmente se realiza mediante la API FullScreen de Javascript.


```html
<div class="screen" open>
  <p>Has colocado esta ventana en pantalla completa.</p>
  <button class="close">Cerrar</button>
</div>

<button class="open">Abrir en FullScreen</button>
```

```css
.screen {
  display: none;
}

:fullscreen {
  display: block;
  background: linear-gradient(120deg, black, indigo);
  border: 3px solid red;
  color: white;
  padding: 1rem;
}
```

```javascript
const button = document.querySelector(".open");
const close = document.querySelector(".close");
const screen = document.querySelector(".screen");

button.addEventListener("click", () => screen.requestFullscreen());
close.addEventListener("click", () => document.exitFullscreen());
```

### Pseudoclase `:modal`

Mediante la pseudoclase `:modal` se puede seleccionar un elemento que está actuando como una ventana o elemento modal, o lo que es lo mismo, un elemento que centra la atención del usuario y no permite interacción con otros elementos que no son sus hijos.

En el ejemplo anterior, modificando `:fullscreen` por `:modal` continuaría siendo válido y funcionando porque un elemento a pantalla completa con `.requestFullscreen()` también es un elemento modal, ya que no permite interacción con otros elementos fuera de él hasta que se cierre el modo pantalla completa.

```html
<dialog class="screen">
  <p>Has abierto este diálogo.</p>
  <button class="close">Cerrar</button>
</dialog>

<button class="open">Abrir modal</button>
```

```css
:modal {
  display: block;
  background: linear-gradient(120deg, black, indigo);
  border: 3px solid red;
  color: white;
  padding: 1rem;
}
```

```javascript
const button = document.querySelector(".open");
const close = document.querySelector(".close");
const modal = document.querySelector(".screen");

button.addEventListener("click", () => modal.showModal());
close.addEventListener("click", () => modal.close());
```

![](../img/pseudoclase%20modal.png)

>**Nota:** En este ejemplo, hemos utilizado una etiqueta `<dialog>` para crear ventanas de diálogo, en este caso, una ventana modal. 


### Pseudoclases para buscar o excluir elementos

Esta pseudoclases vienen juntas con el concepto de combinadores lógicos que vimos anteriormente.

| Selector        | Descripción                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `div, button, p` | Agrupaciones. Seleccionamos varios elementos separándolos por comas.       |
| `:is()`         | Agrupaciones. Idem al anterior, pero permite combinar con otros selectores. | 
| `:where()`      | Agrupaciones. Idem al anterior, pero con menor especificidad CSS.           |
| `:not()`        | Permite seleccionar elementos que no cumplan ciertas características.       |
| `:has()`        | Permite seleccionar elementos padre que tengan ciertas características en sus hijos. | 


#### El combinador `:is()`

La pseudoclase funcional `:is()` es un reemplazo práctico de la agrupación de selectores mediante comas, que permite reescribir selectores complejos de una forma mucho más práctica y compacta, ya que permite combinar y acumular otros selectores con los pasados por parámetro a `:is()`.

Vamos con el primer ejemplo. El siguiente selector agrupa 3 partes diferentes:

```css
.container .list,
.container .menu,
.container ul {
  /* ... */
}
```

Si nos fijamos bien, la clase `.container` siempre aparece en cada uno de los tres casos, sin embargo, no hay forma de abreviarla, aunque sólo cambie la última parte.

Con la pseudoclase `:is() ` si que podemos abreviar la información repetida del ejemplo anterior, reescribiéndolo de la siguiente forma:

```css
.container :is(.list, .menu, ul) {
  /* ... */
}
```
Observa que hemos indicado los 3 casos iniciales en un sólo selector (que añade 3 posibilidades diferentes por parámetro). Esto nos permite crear código mucho más compacto y sencillo de leer y escribir.

Veamos un ejemplo simple del uso de `:is`.

Si deseas encontrar todos los elementos secundarios `h2`, `li` y `img` en un elemento `.post`, podrías escribir una lista de selectores como esta:

```css
.post h2,
.post li,
.post img {
    …
}
```

Con la seudoclase `:is()`, puedes escribir una versión más compacta:

```css
.post :is(h2, li, img) {
    …
}
```

Otro ejemplo:

```html
<div class="container">
  <p>Texto en un párrafo</p>
  <button>Botón 1</button>
  <button>Botón 2</button>
</div>
```

Si quieres aplicar estilos a los elementos `<p>` y `<button>`, puedes escribir lo siguiente:

```css
:is(p, button) {
  color: red;
  font-weight: bold;
}
```

#### Ventajas de usar la pseudoclase `:is`

- **Menor redundancia:** Puedes agrupar varios selectores, lo que reduce la necesidad de escribir múltiples reglas.

- **Mayor legibilidad:** Si tienes varios selectores que comparten estilos, el código se vuelve más limpio y fácil de entender.

- **Eficiencia:** En lugar de escribir reglas por separado para cada selector, :is() simplifica tu CSS.

#### ¿Qué pasa con la especificidad?

Una característica importante de `:is()` es que la especificidad de la regla CSS no se ve incrementada por el uso de `:is()`. La especificidad del selector más específico dentro de `:is()` prevalecerá.

Por ejemplo, si tienes un selector como este:

```css
div:is(.class1, .class2) {
  color: blue;
}
```

La especificidad de este selector será la misma que la de `div.class1` o `div.class2`, no la de `div:is(.class1, .class2)`.


#### El combinador `:where()`

El combinador lógico `:where()`, funciona exactamente igual que el combinador `:is()`. La única diferencia que tiene es en cuanto a la especificidad CSS. 

Mientras que con el combinador `:is()`, la especificidad es el valor más alto de la lista de parámetros de `:is()`, en el caso de `:where()` la especificidad CSS es siempre cero.

Veamos un ejemplo para clarificarlo:

```css
.container :is(.list, .element, .menu) {  /* Especificidad (0,2,0) */
  /* ... */
}

.container :where(.list, .element, .menu) {  /* Especificidad (0,1,0) */
  /* ... */
}
```


#### El combinador `:not()`

El combinador, selector o pseudoclase de negación `:not()` es muy útil, ya que permite seleccionar todos los elementos que no cumplan los criterios indicados en sus parámetros entre paréntesis.

Veamos un sencillo ejemplo:

```html
<p class="first">Hello, my first paragraph.</p>
<p class="main">Again, my main paragraph.</p>
<p class="last">Bye, my last paragraph.</p>
```

```css
p:not(.main) {
  border: 2px solid black;
  padding: 8px;
  color: white;
  background: indigo;
}
```

![](../img/pseudoclase%20not%201.png)

#### Selectores complejos en `:not()`

Antiguamente, sólo se permitían selectores simples en el combinador `:not()`. Sin embargo, actualmente los navegadores permiten indicar listas de selectores o selectores complejos.

Observa el siguiente ejemplo. Aunque no tiene demasiado sentido, se puede ver como los selectores complejos son aceptados por parámetro del combinador `:not()`:


```html
<p class="first">Hello, my first paragraph.</p>
<p class="main">Again, my main paragraph.</p>
<p class="last">Bye, my last paragraph.</p>
```

```css
p:not(:is(.first, .last)) {
  border: 2px solid black;
  padding: 8px;
  color: white;
  background: indigo;
}
```

![](../img/pseudoclase%20not%202.png)

En este caso, tenemos tres elementos y le hemos dicho que le de estilo a los elementos que:

- Sean párrafos `<p>`
- No tengan la clase `.first`
- No tengan la clase `.last`

Como resultado, se le da estilo sólo al elemento `<p>` con clase .main, que es la única que cumple la restricción.

### Selectores `:not()` encadenados

Otra forma de escribir selectores complejos utilizando combinadores `:not()` es encadenando uno con otro. De esta forma, podemos conseguir cosas similares a los casos anteriores. Veamos el ejemplo anterior, reescribiéndolo con `:not()` encadenados:


```html
<p class="first">Hello, my first paragraph.</p>
<p class="main">Again, my main paragraph.</p>
<p class="last">Bye, my last paragraph.</p>
```

```css
p:not(.first):not(.last) {
  border: 2px solid black;
  padding: 8px;
  color: white;
  background: indigo;
}
```

En este caso, estamos dando estilo a los elementos que:

- Sean párrafos `<p>`
- No tengan la clase `.first`
- No tengan la clase `.last`

Como puedes ver, equivalente al caso anterior.

![](../img/pseudoclase%20not%203.png)

#### Detalles importantes sobre `:not()`

Algunos detalles adicionales (e importantes) sobre la pseudoclase funcional `:not()`:

-  El combinador `:not()` se puede anidar dentro de otro `:not()`.
-  El combinador `:not()` no acepta pseudoelementos, como `::before` o `::after`, por parámetro.
-  Al igual que con :is(), la especificidad de `:not()` es el valor más alto de sus parámetros.


#### El combinador `:has()`

Probablemente, uno de los combinadores o selectores más potentes es `:has()`. En CSS, cuando damos estilo, el elemento objetivo al que se le aplica el estilo es siempre el último que se escribe en el selector.

Por ejemplo, en este caso el elemento a quién se le da estilo es a .element, siempre y cuando cumpla el resto de restricciones, que en este caso es que se encuentre dentro de un elemento .container:

```css
.container .element {
  background: red;
}
```

Sin embargo, con el combinador :has() esto se puede cambiar.

#### El combinador `:has()`

El combinador o pseudoclase `:has()` permite seleccionar un elemento contenedor, siempre y cuando sus elementos hijos (descendientes) cumplan los criterios indicados por los parámetros de `:has()`, lo que comunmente siempre se ha denominado el selector padre.


```css
a {
  /* ... */
}

a:has(> img) {
  /* ... */
}
```

1. En el primer caso, aplicamos estilos a TODOS los enlaces `<a>`.
2. En el segundo caso, aplicamos estilos a todos los enlaces `<a>` que contengan una imagen `<img>`.

#### Selector padre con `:has()`

Veamos un ejemplo real: tenemos 3 enlaces: los dos primeros contienen una imagen y el tercero y último, contiene un texto:

```html
<div class="container">
  <a href="https://manz.dev/"><img src="astronaut.png" alt="Astronauta ManzDev"></a>
  <a href="https://manz.dev/"><img src="batmanz.png" alt="BatManzDev"></a>
  <a href="https://manz.dev/">https://manz.dev/</a>
</div>
```

```css
img {
  width: 64px;
  height: 64px;
}

a {
  border: 3px solid black;
  padding: 5px;
}

a:hover {
  border-color: blue;
  color: blue;
}

a:hover:has(> img) {
  border-color: red;
}
```

![](../img/pseudoclase%20has%201.png)

Si nos fijamos en el CSS, en `a:hover` indicamos que cuando se mueva el ratón sobre el enlace:

- Se aplique un color azul en el borde.
- Se aplique color de texto azul.

Sin embargo, en el selector `a:hover:has(> img)` indicamos que cuando se mueva el ratón sobre un enlace que contenga una imagen:

- Se aplique un color rojo en el borde.

#### Selector de estados `:has()`

Quizás el detalle más interesante del combinador o selector `:has()` es que lo podemos utilizar para controlar estados de ciertos elementos de la página. Para ello, podemos utilizar pseudoclases como :checked o :hover, por ejemplo.

El siguiente ejemplo permite cambiar el diseño de un elemento, dependiendo de una casilla `<input>` que no tiene relación directa:


```html
<label>
  <input type="checkbox"> Marca esta casilla
</label>

<div class="container">
  <div class="item"></div>
</div>
```


```css
.item {
  width: 50px;
  height: 50px;
  background: grey;
}

html:has(input:checked) .item {
  background: indigo;
}
```

![](../img/pseudoclase%20has%202.png)


#### Detalles importantes sobre `:has()`
Algunos detalles interesantes sobre la pseudoclase funcional `:has()`:

- La pseudoclase `:has()` no se puede anidar dentro de otra `:has()`.
- Los pseudoelementos, como ::before o ::after, no funcionan dentro de `:has()`.
- La especificidad de `:has()` es el valor más alto de los selectores indicados por parámetro.

---

Regresar al [README](../README.md)