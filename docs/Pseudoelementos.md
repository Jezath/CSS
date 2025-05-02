# Pseudoelementos

---

- [Pseudoelemento ::marker](#pseudoelemento-marker)
- [Pseudoelemento ::backdrop](#pseudoelemento-backdrop)
- [Pseudoelemento ::placeholder](#pseudoelemento-placeholder)
- [Pseudoelemento ::file-selector-button](#pseudoelemento-file-selector-button)
- [Contenido generado en CSS](#contenido-generado-en-css)
- [Pseudoelementos tipograficos](#pseudoelementos-tipograficos)
- [Pseudoelementos de resaltado](#pseudoelementos-de-resaltado)

---

Los pseudoelementos son una característica de CSS que permite hacer referencias a «comportamientos virtuales no tangibles».

¿Qué significa esto? Dicho de otra forma: Los pseudoelementos permiten seleccionar y dar estilo a elementos que no existen en el HTML, o que no son un simple elemento en sí. La sintaxis de los pseudoelementos está precedida de dos puntos dobles (`::`) para diferenciarlos de las pseudoclases, las cuales sólo tienen dos puntos (`:`).

![](https://lenguajecss.com/css/pseudoelementos/que-son/sintaxis-pseudoelementos.png)


### Tipos de pseudoelementos
Existen varios tipos de pseudoelementos, que se encuentran organizados en categorías. Puedes encontrarlos en la siguiente tabla:

| **Pseudoelementos**                                      | **Significado**                                                       |
|----------------------------------------------------------|-----------------------------------------------------------------------|
| Contenido generado                                       | Información generada desde CSS, sin existir en el HTML.               |
| ::before, ::after                                        |                                                                       |
| Contenido tipográfico                                    | Pseudoelementos relacionados con temas de tipografías.                |
| ::first-line, ::first-letter                             |                                                                       |
| Contenido destacado                                      | Pseudoelementos para remarcar o destacar información.                 |
| ::selection, ::target-text, ::spelling-error, ::grammar-error |                                                                  |
| WebComponents                                            | Pseudoelementos relacionados con WebComponents                        |
| ::part, ::slotted                                         |                                                                      |
| View Transition API                                      | Pseudoelementos de transición de cambio de página.                    |
| ::view-transition, ::view-transition-group, ::view-transition-image-pair |                                                       |
| ::view-transition-new, ::view-transition-old             |                                                                       |
| Otros pseudoelementos                                    | Pseudoelementos de otras categorías variadas                          |
| ::marker, ::placeholder, ::file-selector-button          |                                                                       |


### Otros pseudoelementos

Al margen de los pseudoelementos anteriores, explicados en su respectiva sección, nos quedan algunos pseudoelementos sin catalogar.


| **Pseudoelemento**               | **Descripción**                                                              |
|-----------------------------------|------------------------------------------------------------------------------|
| ::marker                          | Aplica estilos a las marcas o símbolos de cada ítem de una lista.            |
| ::backdrop                        | Aplica estilos al fondo exterior de un elemento en primer plano (sin que afecte a este). |
| ::placeholder                     | Aplica estilos a los textos de sugerencia de los campos `<input>`.           |
| ::file-selector-button            | Aplica estilos a los botones de campo `<input>` de subir archivos.           |


### Pseudoelemento `::marker`
El pseudoelemento `::marker` sirve para hacer referencias a los signos o marcas de la listas (`<ol> o <ul>`), en el caso de que queramos que tengan un estilo diferente al del texto de la lista.

En este ejemplo se aplica el estilo a los elementos `<li>` de los ítems de una lista `<ul>`:

```html
<ul>
  <li>Opción número 1.</li>
  <li>Opción número 2.</li>
  <li>Opción número 3.</li>
  <li>Opción número 4.</li>
  <li>Opción número 5.</li>
</ul>
```

```css
ul li::marker {
  content: "⮞ ";
  color: red;
}
```

![](../img/Pseudoelemento%20marker%201.png)

Solo se admite un pequeño subconjunto de propiedades CSS para `::marker`:

- color
- content
- white-space
- font propiedades
- Propiedades animation y transition

Puedes cambiar el símbolo del marcador con la propiedad content. Puedes usar esto para establecer un símbolo más y menos para los estados cerrado y vacío de un elemento `<summary>`, por ejemplo:

```html
<ul>
  <li>Donec ullamcorper nulla non metus auctor fringilla.</li>
  <li>Morbi leo risus, porta ac consectetur ac, vestibulum at eros.</li>
  <li>Curabitur blandit tempus porttitor.</li>
</ul>

<ol>
  <li>Donec ullamcorper nulla non metus auctor fringilla.</li>
  <li>Morbi leo risus, porta ac consectetur ac, vestibulum at eros.</li>
  <li>Curabitur blandit tempus porttitor.</li>
</ol>

<details>
  <summary>Open for some more content</summary>
  <p>
    Maecenas sed diam eget risus varius blandit sit amet non magna. Sed posuere
    consectetur est at lobortis. Aenean eu leo quam. Pellentesque ornare sem
  </p>
</details>
```

```css
::marker {
  color: hotpink;
}

ul ::marker {
  font-size: 1.5em;
}

ol ::marker {
  font-size: 1.1em;
}

summary::marker {
  content: '\002B'' '; /* Plus symbol with space */
}

details[open] summary::marker {
  content: '\2212'' '; /* Minus symbol with space */
}

/* Presentational styles */
li + li {
  margin-top: 0.25em;
}

ol {
  padding: 0 0 0 1.1em;
}
```

![](../img/Pseudoelemento%20marker%202.png)


### Pseudoelemento `::backdrop`
Si tienes un elemento que se presenta en el modo de pantalla completa, como un `<dialog>` o un `<video>`, puedes aplicarle diseño al fondo (el espacio entre el elemento y el resto de la página) con el pseudoelemento ::backdrop:

```html
<video src="https://storage.com" controls></video>
```

```css
video::backdrop {
  background-color: goldenrod;
}

video {
  min-width: 20rem;
  max-width: 100%;
}
```

### Pseudoelemento `::placeholder`

Mediante el pseudoelemento `::placeholder` podemos dar estilos particulares a los elementos `<input>` que tienen el atributo placeholder definido. El atributo placeholder sirve para indicar una sugerencia o mensaje de ayuda o de información con la finalidad de ese campo de texto, normalmente una ayuda de lo que deben escribir o similar.

```html
<input type="text" placeholder="Sugerencia de texto">
```

```css
input::placeholder {
  background: darkred;
  color: white;
  padding: 5px;
}
```

![](../img/Pseudoelemento%20placeholder.png)


### Pseudoelemento `::file-selector-button`

El pseudoelemento `::file-selector-button` hace referencia al `<button>` que se incluye dentro de un elemento `<input type="file">`, o lo que es lo mismo, un botón para enviar ficheros a través de un formulario. De esta forma, podemos personalizar la apariciencia del botón del formulario.

```html
<input type="file" value="Enviar archivo">
```

```css
input::file-selector-button {
  background: indigo;
  color: white;
  padding: 0.5rem 1rem;
  border: 2px solid black;
}
```

![](../img/Pseudoelemento%20file-selector-button.png)


### Contenido generado en CSS

Dentro de la categoría de los pseudoelementos CSS, y quizás uno de los más conocidos, se encuentra la propiedad content. Esta propiedad se utiliza en selectores que incluyen los pseudoelementos `::before` o `::after` (que explicaremos un poco más adelante), y su objetivo es indicar que vamos a crear contenido antes o después del elemento indicado en cuestión.


#### Propiedad `content`

La propiedad content admite parámetros de diverso tipo, incluso concatenando información mediante espacios. Podemos utilizar varios tipos de contenido:


| **Valor**                     | **Descripción**                                             | **Ejemplo**                        |
|-------------------------------|-------------------------------------------------------------|------------------------------------|
| `string` "..."                         | Añade el texto indicado.                                    | content: "Contenido:";             |
| attr(atributo)                 | Añade el valor del atributo HTML indicado.                   | content: attr(href);               |
| `image` url("...")                     | Añade la imagen indicada en la URL.                          | content: url("icon.png");         |
| `gradient`                    | Añade un gradiente del tamaño indicado.                      | content: linear-gradient(red, blue); |
| `counter`                   | Define un contador CSS para mostrar.                        | content: counter(item);           |


#### Pseudoelemento `::before`

Los pseudoelementos `::before` y ::after permiten hacer referencia a «justo antes del elemento» y «justo después del elemento», respectivamente. Además de selectores básicos como clase o id, combinadores, atributos o pseudoclases, puedes añadir un pseudoelemento, precedido por ::.

En el caso del pseudoelemento `::before`, el navegador se encargará de añadir contenido antes del inicio de la etiqueta de apertura del elemento que has seleccionado con el resto del selector:

```html
<p>Y dije <q>Hola, ¿qué tal?</q>, entre susurros.</p>
```

```css
q::before {
  content: "«";
  color: red;
}
```

![](../img/pseudoelemento%20before.png)


#### Pseudoelemento `::after`

De la misma forma, tenemos el pseudoelemento `::after`, que permitirá añadir contenido después de la etiqueta de cierre en cuestión. Vamos a completar el código anterior, utilizando también un `::after` y añadiendole más estilos a la propia etiqueta:


```html
<p>Y dije <q>Hola, ¿qué tal?</q>, entre susurros.</p>
```

```css
q::before {
  content: "«";
  color: red;
}

q::after {
  content: "»";
  color: red;
}

q {
  color: darkred;
  font-style: italic;
}
```

![](../img/Pseudoelemento%20after.png)


### Pseudoelementos tipograficos

Dentro de una categoría de pseudoelementos tipográficos, podemos encontrar los pseudoelementos `::first-letter` o `::first-line`:


#### pseudoelemento `::first-letter`

El pseudoelemento `::first-letter`, como su propio nombre indica, permite seleccionar y dar estilo a la primera letra del texto indicado. Así podremos recrear el efecto clásico de cuentos infantiles o algunas otras obras, donde la primera letra se establece mucho más grande que el resto del texto y con una tipografía decorativa mucho más llamativa.

```html
<p>
  En un lugar de la Mancha, cuyo nombre no logro acordarme...
</p>
```

```css
p {
  font-family: 'Open Sans', sans-serif;
  font-size: 1.5rem;
}

p::first-letter {
  font-family: 'Cinzel Decorative', serif;
  font-size: 5rem;
}
```

![](../img/pseudoelemento%20first-letter.png)


#### pseudoelemento `::first-line`

Por otro lado, el pseudoelemento `::first-line` es muy útil para aplicar un estilo solamente a la primera línea del texto indicado. Puede ser interesante si queremos cambiar algún detalle, pero que afecte exclusivamente a la primera línea, independientemente del tamaño que tenga

![](https://lenguajecss.com/css/pseudoelementos/tipograficos/first-letter-first-line.png)


### Pseudoelementos de resaltado

Existe una serie de pseudoelementos orientados a la selección o resaltado de texto en un documento HTML mostrado a través de un navegador. Veamos que pseudoelementos tenemos a nuestra disposición:

| **Pseudoelemento**   | **Descripción**                                                           |
|----------------------|---------------------------------------------------------------------------|
| ::selection          | Aplica estilos al fragmento de texto seleccionado por el usuario.         |
| ::target-text        | Aplica estilos al fragmento de texto enlazado tras el ancla de la URL.    |
| ::spelling-error     | Aplica estilos al fragmento de texto resaltado por un error ortográfico.  |
| ::grammar-error      | Aplica estilos al fragmento de texto resaltado por un error gramatical.   |

#### pseudoelemento `::selection`

Cuando seleccionamos un fragmento de texto, el navegador suele aplicar un color de fondo que depende del sistema operativo, del tema, o similar. Al igual que ocurre con la propiedad accent-color, es posible que queramos aprovechar esto para definir un color que tengan sentido con los colores corporativos de la marca o web, por lo que podríamos cambiarlo haciendo uso del pseudoelemento `::selection`:


```html
<p>Selecciona este texto para ver el color.</p>
```

```css
::selection {
  background: indigo;
  color: white;
}
```

![](../img/pseudoelemento%20selection.png)


#### pseudoelemento `::target-text`

En algunos casos, al crear un enlace a una página, tras el ancla de la URL definida con el carácter #, se puede añadir el fragmento de texto :~:text= seguido del texto, palabra o frase a buscar en la propia página. Al hacer esto, el navegador resaltará esa parte para que sea más sencillo encontrarla.

Esta página suele estar destacada con color de fondo amarillo sobre letras negras, pero podemos personalizarlo a través del pseudoelemento `::target-text`:

#### pseudoelemento `::spelling-error`

El pseudoelemento `::spelling-error` nos permite modificar los estilos que se aplican a como se muestra un error ortográfico en el navegador, que normalmente se visualiza con un subrayado ondulado rojo en la palabra o texto afectado.


```html
<p>
  Pulsa en el interior del campo de texto
  para que revise la ortografía:
</p>

<textarea spellcheck="true">Vamos a cometer un herror hortográfico para ver el resaltado de sintaxis.</textarea>
```


```css
textarea {
  min-width: 400px;
  min-height: 100px;
  font-size: 1.25rem;
}

::spelling-error {
  background: darkred;
  color: white;
}
```

![](../img/pseudoelemento%20spelling-error.png)

### Pseudoelemento `::grammar-error`

Por su parte, el pseudoelemento `::grammar-error` es exactamente igual al anterior, sólo que se encarga de señalar los errores gramaticales del texto, y no los ortográficos.

---

Regresar al [README](../README.md)