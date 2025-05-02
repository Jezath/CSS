# Variables

Las variables nos permiten guardar valores para usarlas en diferentes partes y reducir el exceso de código en css.

### Definir o crear variables CSS

Para crear una custom property haremos uso de los dos guiones -- como prefijo al nombre que vamos a utilizar. En este caso, hemos creado una variable CSS llamada --background-color, al que le hemos asignado el valor black, que es un color:

```css
:root {
  --background-color: black; /* valor del color */
}
```

Observa que en este caso, hemos establecido la variable dentro del selector con pseudoclase **:root**. Esta pseudoclase **:root** hace referencia al elemento raíz del documento, es decir, al elemento `<html>`. La diferencia entre utilizar html o **:root** como selector es que este último tiene algo más de especificidad CSS. Mientras el selector html tiene **(0,0,1)**, **:root** tendría **(0,1,0)**.

### Utilizar una variable CSS

```css
:root {
  --background-color: indigo;
}

body {
  background: var(--background-color);
}
```

Otro ejemplo de como usar las variables:

```css
:root {
    --primary-color: #003476;
    --secundary-color: #b4d2f7;
    --header-size: 4rem;
    --font: 1.8rem;
}
```

---
