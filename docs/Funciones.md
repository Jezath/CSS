# Funciones

En CSS, las "funciones" no son funciones en el sentido clásico de la programación, pero sí hay funciones que se usan dentro de propiedades para modificar estilos de forma más avanzada. Aquí te dejo una lista con las funciones de CSS más usadas y para qué sirven:

### Funciones de color 🎨

- rgb() / rgba()
  - Define colores con valores rojo, verde, azul y opcionalmente alfa (transparencia).
Ejemplo: rgba(255, 0, 0, 0.5)

- hsl() / hsla()
  - Colores usando matiz, saturación y luminosidad. También puede incluir transparencia.
Ejemplo: hsl(120, 100%, 50%)

- color-mix() (más moderno)
  - Mezcla dos colores.
Ejemplo: color-mix(in srgb, red 50%, blue 50%)


### Funciones de tamaño y unidades
- calc()
  - Permite hacer cálculos con unidades.
Ejemplo: width: calc(100% - 50px)

- `min()` / `max()`
  - Escoge el menor o mayor valor entre los dados.
Ejemplo: width: min(100%, 600px)

- `clamp()`
  - Establece un valor con mínimo, ideal y máximo.
Ejemplo: font-size: clamp(1rem, 2.5vw, 2rem)

#### Funcíon min()

📌 ¿Para qué sirve?

Escoge el valor más pequeño entre varios valores. Si quieres que algo sea ancho, pero no demasiado en pantallas grandes. Esto evita que se extienda de más.

```css
width: 80%;
max-width: 800px;

/* si la pantalla es menor a 800px toma el valor de 80% esto le permite seguir encogiendose, crece hasta los 800px */
  
width: min(800px, 80%); /* <- reemplaza el max-width */
```

#### Funcíon max()

📌 ¿Para qué sirve?

Escoge el valor máximo entre dos o más expresiones. Se utiliza comúnmente para que un valor (como el ancho, alto, margen, padding, etc.) no sea menor que cierto límite mínimo, lo que es muy útil para diseños responsivos.

```css
width: 80%;
min-width: 400px;

/* si la patalla es mayor a 400px toma el valor del 80%, se encoge hasta los 400px */
  
width: max(400px, 80%); /* <- reemplaza el min-width */
```

#### Funcíon clamp()

📌 ¿Para qué sirve?

Establece un valor mínimo, preferido y máximo. Súper útil para hacer textos o medidas que se adapten automáticamente a la pantalla sin media queries.

```css
width: 80%;
min-width: 400px;
max-width: 800px;

/* clamp(valor-min, valor-preferido, valor-máx); */

width: clamp(400px, 80%, 1200px); 
```

### Funciones de transformación 📐
- translate()
  - Mueve un elemento.
Ejemplo: transform: translate(50px, 20px)

- rotate()
  - Rota un elemento.
Ejemplo: transform: rotate(45deg)

- scale()
  - Escala el tamaño.
Ejemplo: transform: scale(1.5)


### Funciones de gradientes 🌈
- linear-gradient()
  - Crea un degradado lineal.
Ejemplo: background: linear-gradient(to right, red, blue)

- radial-gradient()
  - Degradado radial (desde el centro).
Ejemplo: background: radial-gradient(circle, red, blue)

- conic-gradient()
  - Degradado cónico, como una rueda de colores.
Ejemplo: background: conic-gradient(red, yellow, green)


### Funciones de filtros 👁️
- blur()
  - Aplica desenfoque.
Ejemplo: filter: blur(5px)

- brightness(), contrast(), grayscale(), etc.
  - Ajustan el aspecto de las imágenes o fondos.
Ejemplo: filter: grayscale(100%)

---
