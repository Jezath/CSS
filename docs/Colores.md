# Colores

Uno de los primeros cambios de estilo que hacemos cuando aprendemos CSS es hacer variaciones en los colores de primer plano y de fondo de un documento HTML

### Propiedades de color

|Propiedad|Valor|Significado|
|---------|-----|-----------|
|`color`|color|Cambia el color del texto que está en el interior de un elemento.|
|`background-color`|color|	Cambia el color de fondo de un elemento.|

```html
<p class="element">hola</p>
```

```css
.element {
  width: 100px;
  height: 100px;
  background-color: indigo; /* Color de fondo */
  color: white; /* Color de texto */
}
```

![colores](../img/colores.png)

### Formas de aplicar colores

```css
h1 {
  color: rgba(red, green, blue, alpha);
  color: rgb(red, green, blue);
  color: hsl(hue, saturation, lightness);
  color: oklch(lightness chroma hue);
  color: #09f; /*hexadecimal*/
}
```

### Palabras clave de color

Otra forma de aplicar colores es usando la herencia con el valor `currentColor` que toma el color del contenedor padre.

```css
h2 {
  border: 3px solid currentColor;
}
```

Otro valor que podemos usar como palabra clave es la de `transparent` que establece un color completamente transparente (valor por defecto de `background-color`).

---

Regresar al [README](../README.md)