# Unidades CSS

---

- [Unidades absolutas](#unidades-absolutas)
- [Unidades relativas](#unidades-relativas)
- [Unidades del viewport](#unidades-del-viewport)
- [Uso de medidas relativas](#uso-de-medidas-relativas--vw-wh)

---

En CSS necesitaremos utilizar tamaños. Para indicarlo de una forma apropiada, necesitaremos conocer las unidades que podemos utilizar en CSS para definir dichos tamaños. Existen multitud de unidades. Quizás las más populares son unidades como px (píxels) o % (porcentajes), entre muchas otras.

### Tipos de unidades

|Tipo de unidad|Unidades|Descripción|
|--------------|--------|-----------|
|Unidades absolutas|px, cm, mm, Q, in, pt, pc|Unidades estáticas o de tamaño fijo.|
|Unidades relativas|%|Unidades basadas en el tamaño del padre inmediato.|
||em, rem|Unidades basadas en el tamaño de una tipografía.|
||lh, rlh|Unidades basadas en en el interlineado.|
|Relativas al viewport|vw, vh, vmin, vmax, vi, vb|Unidades basadas en la región visible del navegador.|
||	svw, svh, svmin, svmax, svi, svb|Idem, en pantallas pequeñas (small viewport)|
||	lvw, lvh, lvmin, lvmax, lvi, lvb|Idem, en pantallas grandes (large viewport).|
||dvw, dvh, dvmin, dvmax, dvi, dvb|	Idem, en pantallas dinámicas (dynamic viewport).|
|Relativas al grid|fr|Unidad basada en la fracción restante (sólo para grids).|
|Unidades de dirección|deg, grad, rad, turn|Unidades para indicar una dirección.|
|Unidades de duración|s, ms|Unidades para indicar un tiempo concreto.|
|Unidades de frecuencia|hz, khz|Unidades para indicar una frecuencia.|
|Unidades de resolución|dpi, dpcm, dppx|Unidades para indicar resoluciones.|

### Unidades absolutas

Las unidades absolutas son un tipo de medida fija que no cambia, que no depende de ningún otro factor. Son ideales en contextos donde las medidas no varían como pueden ser en medios impresos (documentos, impresiones, etc...), pero son unidades poco adecuadas para la web moderna, donde necesitamos adaptarnos a diferentes resoluciones o pantallas.

![pixel](https://lenguajecss.com/css/unidades-css/absolutas/densidad-pixeles.png)

### Unidades relativas

Las unidades relativas en CSS son más potentes y comunes que las absolutas, ya que se adaptan a factores como el tamaño del elemento padre o la tipografía. Aunque requieren más aprendizaje, son ideales para diseños flexibles en distintos dispositivos.


![](https://static.platzi.com/media/user_upload/35.%20Medidas%20REM-7142208d-9bc7-459d-8816-623ef9c34c91.jpg)

#### Em

Es una unidad relativa que depende del tamaño de fuente del elemento actual. Si usas `em` para definir una propiedad, se basa en el tamaño de la fuente del elemento en el que se encuentra.

```css
body {
  font-size: 16px;
}

p {
  font-size: 2em; /* El tamaño de fuente será 32px (16px * 2) */
}

.child {
  font-size: 1.5em; /* El tamaño será 48px (32px * 1.5) */
}
```

![em](https://www.dreamhost.com/blog/wp-content/uploads/2024/08/03-Tamanos-de-fuente-EM-1024x725.jpg)

#### Rem

`rem` significa **root em**, y está basado en el tamaño de fuente de la raíz `<html>`. Es más predecible y consistente porque siempre se calcula en función del tamaño de fuente del html, sin importar el contexto del elemento donde se usa.

```css
html {
  font-size: 16px;
}

body {
  font-size: 1rem; /* 1rem será 16px (el tamaño de fuente en <html>) */
}

p {
  font-size: 2rem; /* El tamaño de fuente será 32px (16px * 2) */
}
```

Tabla de valores comunes de `rem`:


| Propiedad                    | Valor en `rem` | Equivalente en `px` (con base 16px) |
|------------------------------|----------------|-------------------------------------|
| **Fuente base**               | 1rem           | 16px                                |
| **Título 1 (h1)**             | 2rem           | 32px                                |
| **Título 2 (h2)**             | 1.5rem         | 24px                                |
| **Título 3 (h3)**             | 1.25rem        | 20px                                |
| **Título 4 (h4)**             | 1.125rem       | 18px                                |
| **Párrafo (p)**               | 1rem           | 16px                                |
| **Márgenes pequeños**         | 0.5rem         | 8px                                 |
| **Márgenes medianos**         | 1rem           | 16px                                |
| **Márgenes grandes**          | 2rem           | 32px                                |
| **Espaciado pequeño (padding)** | 0.25rem       | 4px                                 |
| **Espaciado medio (padding)**  | 0.75rem        | 12px                                |
| **Espaciado grande (padding)** | 1.5rem         | 24px                                |
| **Botón pequeño**             | 0.875rem       | 14px                                |
| **Botón grande**              | 1.25rem        | 20px                                |
| **Espaciado entre líneas (line-height)** | 1.5rem | 24px                                |
| **Bordes pequeños**           | 0.125rem       | 2px                                 |
| **Bordes gruesos**            | 0.375rem       | 6px                                 |


![rem](https://www.dreamhost.com/blog/wp-content/uploads/2024/08/02-Tamano-de-fuente-en-REM-1024x725.jpg)


```css
/* variables para font-size */
:root {
  --fs-3xs: 0.5rem;     /*  8px */
  --fs-2xs: 0.625rem;   /* 10px */
  --fs-xs: 0.75rem;     /* 12px */
  --fs-sm: 0.875rem;    /* 14px */
  --fs-md: 1rem;        /* 16px */
  --fs-lg: 1.125rem;    /* 18px */
  --fs-xl: 1.25rem;     /* 20px */
  --fs-2xl: 1.375rem;   /* 22px */
  --fs-3xl: 1.5rem;     /* 24px */
}
```


#### Diferencias clave entre em y rem:

`em`: Se basa en el tamaño de fuente del elemento padre.

`rem`: Se basa en el tamaño de fuente de la raíz del documento `<html>`.

#### ¿Cuándo usar em y rem?

`em`: Es útil cuando deseas que el tamaño de los elementos se ajuste de manera jerárquica o relativa al contenedor donde se encuentran (por ejemplo, dentro de un componente específico).

`rem`: Es útil cuando quieres mantener una relación constante con el tamaño base del documento, lo cual es ideal para diseños más consistentes y accesibles.


### Unidades del viewport

Las unidades de nueva generación en CSS, basadas en el viewport, permiten asignar valores proporcionales al tamaño visible de la ventana del navegador. Al usar unidades precedidas por `v`, se hace referencia a un porcentaje del ancho o alto del viewport, facilitando diseños adaptables.

|Unidad|Significado|Medida aproximada|
|------|-----------|-----------------|
|`vw`|viewport width|1vw = 1% del ancho del navegador|
|`vh`|	viewport height|	1vh = 1% del alto del navegador|
|`vmin`|viewport minimum|1vmin = 1% del alto o ancho (el mínimo)|
|`vmax`|viewport maximum|1vmax = 1% del alto o ancho (el máximo)|

![medidasdelviewport](https://lenguajecss.com/css/unidades-css/relativas-viewport/svh-lvh-dvh.png)

#### Uso de medidas relativas `%` `vw, wh`

En los proximos ejemplos veremos como ajustar elementos con respecto al tamaño de la pantalla del navegador. 

#### Caso 1

Por si solo los elementos en bloques (veremos este tema más adelante) no tienen medidas de ancho o alto definimos más allá del que traen por defecto que suele ser el 100% de su ancho.

```html
<body> <!-- contenedor padre -->
  <main> <!-- contenedor hijo -->
    <p>hola</p>
  </main>
</body>
```

```css
body {
  background: violet;
}

main {
  color: whitesmoke;
  background: slateblue;
  /* width: 100%; */
  height: 50%;
}
```

Si comentamos el `width` del elemento `<main>` su ancho sigue siendo el mismo, es decir el `100%`. 

![medir](../img/medidas%20relativa%201.png)

Pero si cambiamos el porcentaje del `width` su tamaño cambiará. 

```css
main {
  color: whitesmoke;
  background: slateblue;
  width: 50%; /* Tamaño de ancho de un elemento. */
  height: 50%; /* Tamaño del alto de un elemento. */
}
```

Ahora el `width` ocupa el `50%` de su contenedor padre `<body>`.

![medir](../img/medidas%20relativa%202.png)

Por otra parte el `height` aunque tiene el `50%` y el pongamos otro porcentaje su tamaño **NO** cambia.

Esto se debe a que el `%` es una medida relativa al contenedor padre en este caso es el `<body>` el cual no tiene definido un `height`.

Para arreglar esto podemos usar la medida relativa del viewport: `vw` o `vh` que representa el ancho y el alto de la vista de la pantalla.

```css
main {
  color: whitesmoke;
  background: slateblue;
  width: 50vw; /* 50% del ancho de la vista de la pantalla */
  height: 50vh; /* 50% del alto de la vista de la pantalla */
}
```

![medir](../img/medidas%20relativa%203.png)

Si ponemos que el `height` tenga `100vh` notamos que nos genera scroll, esto se debe a que los elementos tienen ciertos estilos por defecto como el margen. 

Entonces `100vh` + `margin` = scroll.

Para solucionar esto tenemos que resetear algunos estilos que vienen por defecto.

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  outline: 1px solid red; /* esta propiedad nos permite hacer debugging; es opcional */
}
```

#### Caso 2

Podemos limitar el crecimiento de los elementos respecto al viewport tanto en su `width` y su `height`.

Para esto usamos las medidas de `max-width`, `min-width` / `max-height`, `min-height`.

```css
main {
  width: 70%;/*poner siempre un valor en % sí vamos a trabajar con mi-max widht/height */
  min-width: 300px; /* establece un min de anchura */
  max-width: 450px; /* establece un máximo de anchura */
  min-height: 500px; /* establece un min de altura, al altura puede crecer */
  margin: 0% auto; /* centra el contenedor */
  background-color: slateblue;
  color: whitesmoke;
}
```

![medir](../img/medidas%20relativa%204.png)

---
