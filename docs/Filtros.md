# Filtros

Los filtros CSS son una característica muy atractiva de CSS que permite aplicar ciertos efectos de imagen, propios de aplicaciones de retoque fotográfico, como sepia, variaciones de brillo o contraste (u otros) al vuelo en el propio navegador, sin hacer cambios permanentes sobre una imagen.

Dichos filtros funcionan a través de la propiedad `filter`, a la cuál hay que especificarle una función concreta de las existentes, como por ejemplo la función de blanco y negro 


```html
<img src="manzdev-goose.png" alt="ManzDev Goose">
```


```css
img {
  filter: grayscale(100%);
  transition: filter 1s;
  width: 200px;
}

img:hover {
  filter: grayscale(0%);
}
```

![](../img/filter%201.png)


### Funciones de filtros

Los filtros de CSS nos proporcionan un amplio abanico de funciones, listas para utilizar mediante la propiedad filter y aplicarlas a los elementos que queramos de nuestra página. Estos filtros permiten alterar los colores, tonalidades o diferentes aspectos visuales, tal como se harían desde un programa de diseño gráfico:


| Función       | Significado                   | Valor de ejemplo              | Mínimo                   | Máximo                     | >100%        |
|---------------|-------------------------------|-------------------------------|---------------------------|-----------------------------|--------------|
| grayscale     | Escala de blanco y negro      | `grayscale(100%)`             | 0% (sin cambios)          | 100% = Grayscale completo   | = 100%       |
| blur          | Desenfoque Gaussiano          | `blur(5px)`                   | 0px (sin cambios)         | -                           | -            |
| sepia         | Grado de color sepia          | `sepia(100%)`                 | 0% (sin cambios)          | 100% = sepia completo       | = 100%       |
| saturate      | Grado de saturación           | `saturate(150%)`              | 0% = desaturado           | 100% (sin cambios)          | Sí           |
| opacity       | Grado de transparencia        | `opacity(50%)`                | 0% = invisible            | 100% (sin cambios)          | = 100%       |
| brightness    | Brillo                        | `brightness(120%)`            | 0% = negro                | 100% (sin cambios)          | Sí           |
| contrast      | Contraste                     | `contrast(200%)`              | 0% = gris                 | 100% (sin cambios)          | Sí           |
| hue-rotate    | Rotación de color (matiz)     | `hue-rotate(180deg)`          | 0deg (sin cambios)        | -                           | -            |
| invert        | Invertir colores              | `invert(100%)`                | 0% (sin cambios)          | 100% = totalmente invertido | = 100%       |
| drop-shadow   | Sombra proyectada             | `drop-shadow(4px 4px 10px black)` | -                     | -                           | Ver función  |


#### Porcentajes o numéros

Observa que las funciones de filtros `grayscale()`, `sepia()`, `saturate()`, `opacity()`, `brightness()`, `contrast()` e `invert()` toman un `percent` ó un `number` como valor, esto ocurre porque es posible proporcionar dicho valor de dos formas diferentes:

- `percent` Como valor porcentual: 0%, 50%, 100%, 150%...
- `number` Como valor numérico: 0, 0.5, 1, 1.5...

#### Rotación de colores

Cuando utilizamos la función `hue-rotate()`, proporcionaremos como parámetro una cantidad de ángulos. Esa cantidad realiza una rotación de colores (hue-rotate) que se puede ver facilmente si observamos una rueda de colores. El número de grados definido por parámetro especifica la rotación aplicada a los colores:


![](https://lenguajecss.com/css/efectos/filtros-css/hue.png)

---
