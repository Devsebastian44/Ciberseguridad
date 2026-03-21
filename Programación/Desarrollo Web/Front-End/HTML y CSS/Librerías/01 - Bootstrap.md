##  y Utilidades

---

## Sistema de Grid

### Contenedores

- `.container` - Contenedor **centralizado** con padding horizontal
- `.container-fluid` - Contenedor con **ancho completo** sin importar el viewport
- `.container-{breakpoint}` - Contenedor con ancho específico para cada breakpoint (`sm`, `md`, `lg`, `xl`, `xxl`)

---

### Filas y Columnas

- `.row` - Fila para **alinear columnas**
- `.col` - Columna **flexible** que se adapta automáticamente
- `.col-{size}` - Columna con un **ancho fijo** de 1 a 12 (basado en la grid de 12 columnas)
- `.col-{breakpoint}-{size}` - Columna fija para un **tamaño de pantalla** específico

---

### Espaciado y Offset

- `.offset-{size}` - Añade un **espacio (offset)** antes de una columna
- `.g-{size}` - Controla el **espaciado** entre filas y columnas (gap)
- `.gx-{size}` - Controla el espaciado **horizontal** entre columnas
- `.gy-{size}` - Controla el espaciado **vertical** entre filas

---

## Tipografía

### Alineación de Texto

- `.text-start` - Alineación del texto a la **izquierda**
- `.text-center` - Alineación **centrada**
- `.text-end` - Alineación del texto a la **derecha**

---

### Estilos de Fuente

- `.fw-{weight}` - Controla el **grosor** de la fuente (`fw-light`, `fw-normal`, `fw-bold`)
- `.fst-{style}` - Define el **estilo** de fuente (`fst-italic`, `fst-normal`)
- `.text-{color}` - Cambia el **color** del texto (`text-primary`, `text-danger`, etc.)
- `.text-decoration-{value}` - Controla la **decoración** del texto (`none`, `underline`, `line-through`)

---

### Transformación de Texto

- `.text-uppercase` - Convierte el texto a **MAYÚSCULAS**
- `.text-lowercase` - Convierte el texto a **minúsculas**
- `.text-capitalize` - Convierte la **primera letra** de cada palabra a mayúsculas
- `.font-monospace` - Aplica una fuente **monoespaciada**

---

## Colores

- `.bg-{color}` - Cambia el **color de fondo** (`bg-primary`, `bg-success`, etc.)
- `.text-{color}` - Cambia el **color del texto**
- `.border-{color}` - Cambia el **color del borde**
- `.link-{color}` - Cambia el **color de los enlaces**

---

## Espaciado (Margin y Padding)

### Margin

- `.m-{size}` - Margen en **todos los lados** (`m-1`, `m-2`, ..., `m-5`, `m-auto`)
- `.mt-{size}` - Margen **superior**
- `.mb-{size}` - Margen **inferior**
- `.ms-{size}` - Margen **izquierdo**
- `.me-{size}` - Margen **derecho**

---

### Padding

- `.p-{size}` - Padding en **todos los lados**
- `.pt-{size}` - Padding **superior**
- `.pb-{size}` - Padding **inferior**
- `.ps-{size}` - Padding **izquierdo**
- `.pe-{size}` - Padding **derecho**

---

## Botones

- `.btn` - Clase **base** para botones
- `.btn-{variant}` - Aplica un **estilo específico** al botón (`btn-primary`, `btn-secondary`, `btn-success`, etc.)
- `.btn-outline-{variant}` - Botones con **borde** en lugar de color sólido
- `.btn-{size}` - **Tamaño** del botón (`btn-sm`, `btn-lg`)

---

## Bordes

### Aplicar Bordes

- `.border` - Aplica un **borde** a un elemento
- `.border-{side}` - Aplica un borde en un **lado específico** (`border-top`, `border-bottom`, etc.)
- `.border-{color}` - Cambia el **color del borde**

---

### Bordes Redondeados

- `.rounded` - Bordes con **esquinas redondeadas**
- `.rounded-{size}` - Nivel de **redondez** (`rounded-sm`, `rounded-lg`, `rounded-pill`, `rounded-circle`)

---

## Display y Visibilidad

- `.d-{value}` - Controla el **display** (`d-block`, `d-inline`, `d-flex`, `d-none`, etc.)
- `.d-{breakpoint}-{value}` - Controla el display según el **breakpoint** (`d-sm-none`, `d-md-block`, etc.)
- `.invisible` - **Oculta visualmente** un elemento sin eliminarlo del flujo del documento

---

## Flexbox

### Contenedor Flex

- `.d-flex` - Activa un **contenedor flex**
- `.flex-{direction}` - Controla la **dirección** del flujo flex (`flex-row`, `flex-column`, etc.)
- `.flex-{wrap}` - Controla el **comportamiento de las filas** flexibles (`flex-wrap`, `flex-nowrap`)

---

### Alineación Flex

- `.align-items-{value}` - Alineación de los elementos en el **eje cruzado** (`align-items-start`, `align-items-center`)
- `.justify-content-{value}` - Alineación de los elementos en el **eje principal** (`justify-content-start`, `justify-content-center`, etc.)

---

## Posicionamiento

- `.position-{value}` - Define el **posicionamiento** (`static`, `relative`, `absolute`, `fixed`, `sticky`)
- `.top-{value}` - Controla la distancia desde el **borde superior**
- `.start-{value}` - Controla la distancia desde el **borde izquierdo**
- `.end-{value}` - Controla la distancia desde el **borde derecho**
- `.bottom-{value}` - Controla la distancia desde el **borde inferior**

---

## Tablas

- `.table` - Activa estilos de **tabla básicos**
- `.table-striped` - Añade un **patrón de rayas** a las filas
- `.table-bordered` - Añade **bordes** a las celdas
- `.table-hover` - **Resalta filas** al pasar el cursor
- `.table-dark` - Aplica un **tema oscuro**
- `.table-responsive` - Hace que la tabla sea **desplazable** en dispositivos pequeños

---

## Formularios

- `.form-control` - Clase **base** para inputs de formularios
- `.form-select` - Activa estilos para un **`<select>`**
- `.form-check` - Aplica estilos a **checkboxes y radios**
- `.form-check-input` - Estilo para el **input** de un checkbox o radio
- `.form-check-label` - Estilo para la **etiqueta** de un checkbox o radio

---

## Componentes Avanzados

- `.modal` - Clase para crear **modales** (ventanas emergentes)
- `.alert` - Estilo para **mensajes de alerta** (`alert-primary`, `alert-danger`, etc.)
- `.card` - Clase base para crear **tarjetas** con diseño limpio
- `.accordion` - Clase para crear secciones **colapsables**
- `.navbar` - Clase para crear una **barra de navegación**
- `.dropdown` - Activa un **menú desplegable**

---

## Utilidades Diversas

### Sombras

- `.shadow` - Añade una **sombra básica**
- `.shadow-{size}` - Controla la **intensidad** de la sombra (`shadow-sm`, `shadow-lg`)

---

### Desbordamiento y Dimensiones

- `.overflow-{value}` - Controla el comportamiento del **desbordamiento** (`overflow-auto`, `overflow-hidden`, etc.)
- `.text-truncate` - **Recorta el texto** con puntos suspensivos
- `.w-{size}` - Define el **ancho** del elemento (`w-25`, `w-50`, `w-100`)
- `.h-{size}` - Define la **altura** del elemento (`h-25`, `h-50`, `h-100`)

---

## Barra Lateral (Sidebar)

### Clases Básicas

- `.sidebar` - Clase **base** para la barra lateral
- `.sidebar-row` - Define una **fila** dentro de la barra lateral
- `.sidebar-item` - **Elementos** dentro de la barra lateral (como enlaces o menús)
- `.sidebar-header` - Estilo para **encabezados** en la barra lateral
- `.sidebar-footer` - Estilo para el **pie** de la barra lateral

---

### Estados de la Barra Lateral

- `.sidebar-collapsed` - Clase para **colapsar** la barra lateral (puede reducir su ancho)
- `.sidebar-expanded` - Clase para **expandir** la barra lateral

---

### Estilos de Fondo

- `.sidebar-bg-light` - Cambia el color de fondo de la barra lateral a **claro**
- `.sidebar-bg-dark` - Cambia el color de fondo de la barra lateral a **oscuro**
- `.sidebar-bg-primary` - Cambia el fondo de la barra lateral al **color primario**

---

### Estilos de Texto

- `.sidebar-text-light` - Cambia el color del texto a **claro**
- `.sidebar-text-dark` - Cambia el color del texto a **oscuro**

---

### Elementos Adicionales

- `.sidebar-divider` - Añade una **línea divisoria** entre secciones
- `.sidebar-link` - Estilo base para **enlaces** dentro de la barra lateral
- `.sidebar-link-active` - **Resalta** el enlace activo en la barra lateral
- `.sidebar-icon` - Clase para **iconos** en la barra lateral
- `.sidebar-toggle` - Clase para el **botón** de alternar la barra lateral
- `.sidebar-scrollable` - Habilita el **scroll** si el contenido excede la altura de la barra lateral

---

## Clase `clearfix`

### Descripción

La clase `.clearfix` se utiliza para aplicar un **"clearfix"** a un contenedor. Esto asegura que los elementos flotantes (`float`) dentro de un contenedor no causen problemas de diseño, permitiendo que el contenedor ajuste automáticamente su altura para abarcar dichos elementos.

---

### Uso

La clase `.clearfix` es especialmente útil cuando estás trabajando con elementos que tienen la propiedad **`float`** (por ejemplo, `.float-start`, `.float-end`) y deseas que el contenedor los incluya en su altura.

---

### Ejemplo de Código

```html
<div class="clearfix">
    <div class="float-start">Elemento flotante a la izquierda</div>
    <div class="float-end">Elemento flotante a la derecha</div>
</div>
```

---