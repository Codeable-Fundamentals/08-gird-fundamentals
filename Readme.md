# Fundamentos de CSS Grid

CSS Grid es un sistema de diseño bidimensional potente que permite crear layouts complejos con filas y columnas. A diferencia de Flexbox (que es principalmente unidimensional), Grid facilita el control tanto horizontal como vertical de forma simultánea.

## Índice
- [Conceptos Básicos](#conceptos-básicos)
- [Propiedades del Contenedor Grid](#propiedades-del-contenedor-grid)
- [Grid Template Columns](#grid-template-columns)
- [Grid Template Rows](#grid-template-rows)
- [Gap (Espaciado)](#gap-espaciado)
- [Alineación en Grid](#alineación-en-grid)
- [Posicionamiento de Elementos](#posicionamiento-de-elementos)
- [Grid Areas](#grid-areas)
- [Grid Implícito vs Explícito](#grid-implícito-vs-explícito)
- [Ejemplos Prácticos](#ejemplos-prácticos)

## Conceptos Básicos

### Terminología de Grid

- **Contenedor Grid**: El elemento padre donde se aplica `display: grid`
- **Ítem Grid**: Cada hijo directo del contenedor grid
- **Línea Grid**: Las líneas divisorias horizontales y verticales
- **Celda Grid**: La unidad más pequeña del grid (intersección de fila y columna)
- **Área Grid**: Conjunto rectangular de celdas
- **Track**: Fila o columna en el grid

### Activando Grid

```css
.container {
  display: grid;  /* o display: inline-grid para que no ocupe todo el ancho */
}
```

## Propiedades del Contenedor Grid

### Grid Template Columns

Define el número y tamaño de las columnas.

```css
.container {
  display: grid;
  
  /* Diferentes formas de definir grid-template-columns */
  
  /* 1. Usando valores fijos */
  grid-template-columns: 200px 200px 200px;
  
  /* 2. Usando fracciones (fr) - distribuyen el espacio disponible */
  grid-template-columns: 1fr 1fr 1fr;  /* 3 columnas iguales */
  
  /* 3. Unidades mixtas */
  grid-template-columns: 200px 1fr 2fr;
  
  /* 4. Usando porcentajes */
  grid-template-columns: 25% 50% 25%;
  
  /* 5. Con la función repeat para patrones repetitivos */
  grid-template-columns: repeat(3, 1fr);  /* Equivalente a 1fr 1fr 1fr */
  grid-template-columns: repeat(2, 1fr 2fr);  /* Repite el patrón 1fr 2fr dos veces */
  
  /* 6. Con minmax() para tamaños responsivos */
  grid-template-columns: minmax(100px, 1fr) minmax(200px, 2fr) minmax(100px, 1fr);
  
  /* 7. Con auto-fill y auto-fit (responsive) */
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));  /* Crea tantas columnas como quepan */
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));  /* Similar a auto-fill pero colapsa columnas vacías */
  
  /* 8. Usando 'auto' para ajustarse al contenido */
  grid-template-columns: auto 1fr auto;
  
  /* 9. Nombres de líneas personalizados (line names) */
  grid-template-columns: [inicio] 40px [centro] 1fr [final] 40px;
}
```

### Grid Template Rows

Define el número y tamaño de las filas.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  
  /* Ejemplos de grid-template-rows */
  
  /* 1. Valores fijos */
  grid-template-rows: 50px 100px 50px;
  
  /* 2. Fracciones (fr) - requiere altura en el contenedor */
  height: 500px;
  grid-template-rows: 1fr 2fr 1fr;
  
  /* 3. Con la función repeat */
  grid-template-rows: repeat(3, 80px);
  
  /* 4. Combinando técnicas */
  grid-template-rows: 80px repeat(2, 1fr) 80px;
  
  /* 5. Con nombres de líneas */
  grid-template-rows: [header-start] 80px [header-end content-start] 1fr [content-end footer-start] 60px [footer-end];
}
```

### Gap (Espaciado)

Define el espacio entre filas y columnas.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 80px 1fr 80px;
  
  /* Espaciado entre filas y columnas */
  gap: 20px;  /* Aplica a filas y columnas */
  
  /* Espaciado específico */
  row-gap: 20px;
  column-gap: 10px;
}
```

## Alineación en Grid

Grid ofrece múltiples propiedades para alinear elementos:

### Alineación de tracks dentro del contenedor

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 100px);  /* 3 columnas de 100px */
  grid-template-rows: repeat(2, 100px);     /* 2 filas de 100px */
  
  /* El contenedor es más grande que el grid */
  width: 500px;
  height: 400px;
  
  /* Alineación horizontal de las columnas */
  justify-content: start | end | center | space-between | space-around | space-evenly;
  
  /* Alineación vertical de las filas */
  align-content: start | end | center | space-between | space-around | space-evenly;
}
```

### Alineación de elementos dentro de las celdas

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  
  /* Alineación horizontal de todos los elementos */
  justify-items: start | end | center | stretch;
  
  /* Alineación vertical de todos los elementos */
  align-items: start | end | center | stretch;
}

/* Para alinear un elemento específico */
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
```

## Posicionamiento de Elementos

Puedes posicionar elementos específicos usando las propiedades `grid-column` y `grid-row`:

```css
.item {
  /* Sintaxis: grid-column: línea-inicio / línea-fin; */
  grid-column: 1 / 3;  /* Ocupa desde la línea 1 hasta la 3 (2 columnas) */
  grid-row: 2 / 4;     /* Ocupa desde la línea 2 hasta la 4 (2 filas) */
  
  /* Métodos alternativos */
  grid-column: 1 / span 2;  /* Comienza en línea 1 y abarca 2 columnas */
  grid-row: 2 / -1;         /* Desde línea 2 hasta la última línea */
  
  /* Shorthand para ambas propiedades */
  grid-area: 2 / 1 / 4 / 3;  /* fila-inicio / columna-inicio / fila-fin / columna-fin */
}
```

## Grid Areas

Grid Areas te permite nombrar secciones del grid y posicionar elementos usando esos nombres:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 3fr 1fr;
  grid-template-rows: 80px 1fr 80px;
  grid-template-areas: 
    "header header header"
    "sidebar content aside"
    "footer footer footer";
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.aside { grid-area: aside; }
.footer { grid-area: footer; }
```

Para dejar una celda vacía, usa un punto (`.`):

```css
grid-template-areas: 
  "header header header"
  "sidebar content ."
  "footer footer footer";
```

## Grid Implícito vs Explícito

El grid explícito es el que defines con `grid-template-columns` y `grid-template-rows`. 

Si hay más elementos que celdas definidas, estos se colocan en el grid implícito (automático):

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;  /* Solo 2 columnas explícitas */
  grid-template-rows: 100px 100px;  /* Solo 2 filas explícitas */
  
  /* Controlar cómo se comporta el grid implícito */
  grid-auto-rows: 80px;  /* Filas automáticas de 80px */
  grid-auto-columns: 1fr;  /* Columnas automáticas de 1fr */
  grid-auto-flow: row | column | dense;  /* Dirección del flujo automático */
}
```

## Ejemplos Prácticos

### Layout Básico de Página

```css
.page {
  display: grid;
  height: 100vh;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

### Grid Responsivo

```css
.galeria {
  display: grid;
  gap: 20px;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
```

### Dashboard con Elementos de Diferentes Tamaños

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(100px, auto);
  gap: 20px;
}

.widget-grande {
  grid-column: span 2;
  grid-row: span 2;
}

.widget-ancho {
  grid-column: span 2;
}

.widget-alto {
  grid-row: span 2;
}
```

## Comparación Grid vs Flexbox

- **Grid**: Ideal para layouts bi-dimensionales (filas y columnas simultáneas)
- **Flexbox**: Ideal para layouts uni-dimensionales (filas O columnas)

Generalmente, es buena práctica:
- Usar Grid para el layout general de la página
- Usar Flexbox para componentes individuales y alineación en una dirección

## Recursos Adicionales

- [CSS Grid Garden](https://cssgridgarden.com/) - Juego para aprender Grid
- [Grid by Example](https://gridbyexample.com/) - Colección de ejemplos
- [MDN Grid Layout](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Grid_Layout) - Documentación completa

---

Para explorar más, revisa los ejemplos en las carpetas:
- `columns/`: Ejemplos con diferentes configuraciones de columnas
- `rows/`: Ejemplos con diferentes configuraciones de filas