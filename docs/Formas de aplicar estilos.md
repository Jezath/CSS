# Formas de aplicar estilos

### Archivo CSS externo

En la cabecera de nuestro documento HTML, más concretamente en el bloque `<head>`, podemos incluir la etiqueta `<link>`.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>CSS</title>
    <link rel="stylesheet" href="style.css">
  </head>
  ...
</html>
```

### Bloque de estilos

Otra de las formas que existen para incluir estilos CSS en nuestra página es añadirlos directamente en el documento HTML a través de una etiqueta `<style>` que contendrá el código CSS:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>CSS</title>
    <style>
      div {
        background: hotpink;
        color: white;
      }
    </style>
  </head>
  ...
</html>
```

### Estilos en linea

La tercera forma de aplicar estilos en un documento HTML es el conocido como estilos en línea. Se trata de hacerlo directamente, a través del atributo `style` de la propia etiqueta donde queramos aplicar el estilo, colocando ahí las propiedades CSS.

```html
<h2 style="color: rebeccapurple;">Hola</h2>
```

---
