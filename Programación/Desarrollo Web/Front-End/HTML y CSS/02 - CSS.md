## Propiedades CSS

---

## Propiedades de Texto

### Espaciado y Alineación

- `letter-spacing` - Define el **espaciado entre caracteres**
- `line-height` - Establece la **altura de la línea**, distancia entre líneas de texto
- `text-align` - **Alineación** del texto dentro de un contenedor (`left`, `center`, `right`, `justify`)
- `text-indent` - Define la **sangría** de la primera línea de un párrafo
- `word-spacing` - Define el **espaciado entre palabras**

---

### Color y Decoración

- `color` - Define el **color del texto**
- `text-decoration` - Controla la **decoración** del texto (`underline`, `overline`, `line-through`)
- `text-shadow` - Aplica **sombra** al texto

---

### Transformación y Overflow

- `text-transform` - Controla la **transformación** del texto (`uppercase`, `lowercase`, `capitalize`)
- `text-overflow` - Especifica cómo manejar el **desbordamiento** de texto (`clip`, `ellipsis`)

---

### Dirección y Espacios

- `direction` - Controla la **dirección** del texto (`ltr`, `rtl`)
- `white-space` - Controla el manejo de los **espacios en blanco** en el texto (`normal`, `nowrap`, `pre`)
- `word-break` - Controla cómo se **rompen las palabras** al final de línea (`normal`, `break-all`, `keep-all`)
- `word-wrap` - Define si las palabras largas pueden **romperse** (`normal`, `break-word`)

---

### Alineación y Escritura

- `vertical-align` - **Alineación vertical** de un elemento inline
- `writing-mode` - Establece la **dirección de flujo** del texto (horizontal o vertical)
- `unicode-bidi` - Controla la dirección del texto **bidireccional**

---

## Propiedades de Fuentes

- `font` - Propiedad **abreviada** para familia, tamaño, estilo, peso y variante
- `font-family` - Define la(s) **familia(s) tipográfica(s)** para el texto
- `font-size` - Especifica el **tamaño** de la fuente
- `font-style` - Define el **estilo** de la fuente (`normal`, `italic`, `oblique`)
- `font-variant` - Controla las **variantes** de la fuente
- `font-weight` - Controla el **grosor** de la fuente (`normal`, `bold`, `lighter`, valores numéricos)
- `font-display` - Controla cómo se muestran las fuentes durante su **carga** (`auto`, `block`, `swap`)
- `font-stretch` - Controla la **anchura** de los caracteres (`normal`, `condensed`, `expanded`)

---

## Propiedades de Fondo

### Básicas

- `background` - Propiedad **abreviada** para todas las configuraciones de fondo
- `background-color` - Establece el **color de fondo**
- `background-image` - Define la **imagen de fondo** de un elemento

---

### Posicionamiento y Repetición

- `background-attachment` - Define si el fondo se **desplaza** con el contenido (`scroll`, `fixed`)
- `background-position` - Controla la **posición** de la imagen de fondo
- `background-repeat` - Controla si la imagen de fondo se **repite** (`repeat`, `no-repeat`, `repeat-x`, `repeat-y`)
- `background-size` - Establece el **tamaño** de la imagen de fondo (`cover`, `contain`, valores específicos)

---

### Avanzadas

- `background-clip` - Define el **área** donde se pinta el fondo (`border-box`, `padding-box`, `content-box`)
- `background-origin` - Establece el **área de posicionamiento** del fondo
- `background-blend-mode` - Define cómo se **mezcla** el fondo con el contenido debajo

---

## Propiedades de Bordes

### Básicas

- `border` - Propiedad **abreviada** para definir los bordes (ancho, estilo y color)
- `border-width` - Controla el **grosor** del borde
- `border-style` - Establece el **estilo** del borde (`solid`, `dashed`, `dotted`)
- `border-color` - Define el **color** del borde
- `border-radius` - **Redondea** las esquinas de un elemento

---

### Por Lado

- `border-top` - Define el **borde superior**
- `border-right` - Define el **borde derecho**
- `border-bottom` - Define el **borde inferior**
- `border-left` - Define el **borde izquierdo**

---

### Avanzadas

- `border-image` - Permite usar una **imagen** como borde
- `border-collapse` - Controla si los bordes de tabla se **colapsan** (`separate`, `collapse`)
- `border-spacing` - Define el **espacio** entre bordes de celdas en tablas

---

## Propiedades de Espaciado

### Margin (Espacio Externo)

- `margin` - Propiedad **abreviada** para los márgenes
- `margin-top` - Define el **margen superior**
- `margin-right` - Define el **margen derecho**
- `margin-bottom` - Define el **margen inferior**
- `margin-left` - Define el **margen izquierdo**

---

### Padding (Espacio Interno)

- `padding` - Propiedad **abreviada** para el relleno interno
- `padding-top` - Define el **relleno superior**
- `padding-right` - Define el **relleno derecho**
- `padding-bottom` - Define el **relleno inferior**
- `padding-left` - Define el **relleno izquierdo**

---

## Propiedades de Dimensión

- `width` - Controla la **anchura** de un elemento
- `height` - Controla la **altura** de un elemento
- `max-width` - Establece la **anchura máxima** de un elemento
- `min-width` - Establece la **anchura mínima** de un elemento
- `max-height` - Establece la **altura máxima** de un elemento
- `min-height` - Establece la **altura mínima** de un elemento

---

## Propiedades de Posicionamiento

### Tipo de Posición

- `position` - Define el **tipo de posicionamiento** (`static`, `relative`, `absolute`, `fixed`, `sticky`)

---

### Desplazamiento

- `top` - Controla la distancia desde el **borde superior**
- `right` - Controla la distancia desde el **borde derecho**
- `bottom` - Controla la distancia desde el **borde inferior**
- `left` - Controla la distancia desde el **borde izquierdo**
- `inset` - Propiedad **abreviada** para `top`, `right`, `bottom`, y `left`

---

### Apilamiento

- `z-index` - Controla el **orden de apilamiento** de los elementos posicionados

---

## Propiedades del Modelo de Caja

- `box-shadow` - Añade una **sombra** a un elemento
- `box-sizing` - Controla cómo se calculan las **dimensiones** (`content-box`, `border-box`)
- `overflow` - Controla cómo se maneja el contenido que **desborda** (`visible`, `hidden`, `scroll`, `auto`)
- `overflow-x` - Controla el desbordamiento **horizontal**
- `overflow-y` - Controla el desbordamiento **vertical**
- `outline` - Define un **contorno** alrededor del elemento (no afecta el layout)
- `outline-offset` - Establece la **distancia** entre el elemento y su contorno

---

## Propiedades de Visualización

- `display` - Define **cómo se muestra** un elemento (`block`, `inline`, `inline-block`, `none`, `flex`, `grid`)
- `visibility` - Controla la **visibilidad** de un elemento (`visible`, `hidden`, `collapse`)
- `opacity` - Establece la **opacidad** de un elemento (0 = transparente, 1 = opaco)

---

## Propiedades de Flexbox

### Contenedor Flex

- `flex-direction` - Define la **dirección** de los elementos flexibles (`row`, `column`)
- `flex-wrap` - Controla si los elementos se **envuelven** (`nowrap`, `wrap`)
- `justify-content` - Controla la alineación en el **eje principal**
- `align-items` - **Alineación** de los elementos dentro del contenedor flex
- `align-content` - **Alineación de las filas** de un contenedor flex

---

### Elementos Flex

- `flex` - Propiedad **abreviada** que controla crecimiento, encogimiento y tamaño base
- `flex-grow` - Controla cuánto puede **crecer** un elemento
- `flex-shrink` - Controla cuánto puede **encogerse** un elemento
- `flex-basis` - Define el **tamaño inicial** de un elemento flex
- `align-self` - **Alineación** de un solo elemento dentro de un contenedor flex

---

## Propiedades de Grid

### Definición del Grid

- `grid` - Propiedad **abreviada** para definir todos los aspectos del grid
- `grid-template-columns` - Define las **columnas** del grid
- `grid-template-rows` - Define las **filas** del grid
- `grid-template-areas` - Define **áreas nombradas** en el grid

---

### Espaciado

- `gap` - Establece el **espacio** entre filas y columnas
- `row-gap` - Define el espacio entre **filas**
- `column-gap` - Define el espacio entre **columnas**

---

### Colocación de Elementos

- `grid-area` - Define el **área** de un elemento dentro del grid
- `grid-column` - Controla la colocación en las **columnas**
- `grid-row` - Controla la colocación en las **filas**

---

### Generación Automática

- `grid-auto-columns` - Define el tamaño de las **columnas automáticas**
- `grid-auto-rows` - Define el tamaño de las **filas automáticas**
- `grid-auto-flow` - Controla cómo se colocan los elementos **automáticamente**

---

### Alineación

- `justify-items` - Alineación **horizontal** de los elementos en sus celdas
- `align-items` - Alineación **vertical** de los elementos en sus celdas
- `justify-self` - Alineación **horizontal** de un elemento individual
- `align-self` - Alineación **vertical** de un elemento individual

---

## Animaciones y Transiciones

### Transiciones

- `transition` - Propiedad **abreviada** para definir transiciones
- `transition-property` - Especifica las **propiedades** que se van a animar
- `transition-duration` - Define la **duración** de la transición
- `transition-timing-function` - Establece la **curva de aceleración**
- `transition-delay` - Define el **retraso** antes de que comience

---

### Animaciones

- `animation` - Propiedad **abreviada** para configurar animaciones
- `animation-name` - Define el **nombre** de la animación
- `animation-duration` - Establece la **duración** de la animación
- `animation-timing-function` - Define el **comportamiento** de la animación
- `animation-iteration-count` - Controla cuántas veces se **repite**
- `animation-direction` - Define la **dirección** (`normal`, `reverse`, `alternate`)
- `animation-fill-mode` - Establece qué valores se aplican **antes y después**
- `animation-play-state` - Controla si está **corriendo o pausada**
- `animation-delay` - Define el **retraso** antes de que comience

---

## Transformaciones

### Básicas

- `transform` - Aplica **transformaciones** (rotación, escala, etc.)
- `transform-origin` - Establece el **punto de referencia** para las transformaciones

---

### 3D

- `transform-style` - Define si los elementos hijos se posicionan en **3D** (`flat`, `preserve-3d`)
- `perspective` - Establece la **perspectiva** para elementos 3D
- `perspective-origin` - Define el **punto de vista** para la perspectiva 3D
- `backface-visibility` - Define si la **cara trasera** es visible (`visible`, `hidden`)

---

### Funciones

- `rotate` - **Rota** un elemento
- `scale` - Cambia el **tamaño** de un elemento
- `translate` - **Desplaza** un elemento a lo largo de los ejes X e Y
- `skew` - Aplica una **inclinación** (sesgo) a un elemento

---

## Propiedades de Flujo y Float

- `float` - Define cómo un elemento debe **flotar** (`left`, `right`, `none`)
- `clear` - Especifica qué elementos pueden flotar junto a un elemento (`none`, `left`, `right`, `both`)

---

## Propiedades de Listas

- `list-style` - Propiedad **abreviada** para el estilo de listas
- `list-style-type` - Define el **tipo de marcador** (`disc`, `circle`, `square`, `decimal`)
- `list-style-position` - Controla la **posición del marcador** (`inside`, `outside`)
- `list-style-image` - Permite usar una **imagen** como marcador

---

## Propiedades de Tablas

- `table-layout` - Controla cómo se calcula el **ancho de las columnas** (`auto`, `fixed`)
- `border-collapse` - Controla si los **bordes** se colapsan (`separate`, `collapse`)
- `border-spacing` - Define el **espacio entre bordes** de celdas
- `caption-side` - Define la **posición del título** (`top`, `bottom`)
- `empty-cells` - Controla si se muestran bordes en **celdas vacías** (`show`, `hide`)

---

## Propiedades de Interacción del Usuario

- `cursor` - Define el **tipo de cursor** cuando pasa sobre un elemento
- `pointer-events` - Controla si un elemento puede ser **objetivo de eventos** del mouse (`auto`, `none`)
- `user-select` - Define si el texto puede ser **seleccionado** (`auto`, `none`, `text`)
- `resize` - Define si un elemento puede ser **redimensionado** (`none`, `both`, `horizontal`, `vertical`)

---

## Efectos Visuales Modernos

- `clip-path` - **Recorta** un elemento según una forma definida
- `filter` - Aplica **efectos visuales** como desenfoques, brillo
- `backdrop-filter` - Aplica efectos de filtro al **área detrás** de un elemento
- `mask` - **Oculta partes** de un elemento usando una máscara
- `mix-blend-mode` - Define cómo se **mezcla** el contenido del elemento con su fondo
- `isolation` - Crea un nuevo **contexto de apilamiento** para blend modes

---

## Contenido Generado

- `content` - Inserta **contenido generado** por CSS (pseudo-elementos `::before` y `::after`)
- `quotes` - Define las **comillas** que se usan con `content`
- `counter-reset` - **Reinicia** un contador CSS
- `counter-increment` - **Incrementa** un contador CSS

---

## Variables CSS (Custom Properties)

```css
:root {
  --color-primary: #007bff;
  --font-size-large: 1.5rem;
}

.element {
  color: var(--color-primary);
  font-size: var(--font-size-large);
}
```

---

## Media Queries y Responsividad

### Estructura de Media Queries

```css
@media screen and (max-width: 768px) {
  /* Propiedades CSS para dispositivos móviles */
}

@media screen and (min-width: 769px) and (max-width: 1024px) {
  /* Propiedades CSS para tablets */
}

@media screen and (min-width: 1025px) {
  /* Propiedades CSS para desktop */
}
```

---

### Unidades Responsivas

- `vw` - **Viewport width** (1vw = 1% del ancho del viewport)
- `vh` - **Viewport height** (1vh = 1% del alto del viewport)
- `vmin` - El **menor** entre vw y vh
- `vmax` - El **mayor** entre vw y vh
- `rem` - Relativo al **tamaño de fuente del elemento raíz**
- `em` - Relativo al **tamaño de fuente del elemento padre**
- `%` - **Porcentaje** relativo al elemento contenedor

---

## Otras Propiedades Importantes

### Optimización

- `will-change` - Indica qué propiedades van a **cambiar** para optimizar rendimiento
- `contain` - Optimiza el rendimiento **limitando el alcance** de los estilos (`layout`, `style`, `paint`, `size`)

---

### Scroll y Ajuste

- `scroll-behavior` - Define el **comportamiento del scroll** (`auto`, `smooth`)
- `scroll-snap-type` - Define el tipo de **snap** al hacer scroll
- `object-fit` - Controla cómo se ajusta el **contenido reemplazado** (`fill`, `contain`, `cover`, `scale-down`)
- `object-position` - Define la **posición** del contenido reemplazado dentro de su contenedor

---

### Decoración

- `box-decoration-break` - Controla cómo se aplica la **decoración de cajas** en contenido dividido

---