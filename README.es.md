# comboSlicer

Segmentación desplegable jerárquica para Power BI. Versión **1.0.0.45**.

Segmentador tipo lista desplegable que construye una jerarquía multinivel a partir de varios campos, filtra el informe mediante el modelo de filtros estándar de Power BI y admite recorte de prefijos, ordenación, filtrado por medida y selección simple o múltiple.

---

## 1. Mini manual de uso

### Instalación
1. Obtén el paquete `.pbiviz` de la carpeta `comboSilcer` en https://github.com/ramiro-fer-vip/comboSlicer/.
2. En Power BI Desktop: `...` (más objetos visuales) > **Importar un objeto visual desde un archivo** y selecciona el paquete.
3. El visual `comboSlicer` aparece en el panel de visualizaciones. Fíjalo para reutilizarlo.

### Asignar datos
| Rol | Tipo | Rango | Uso |
| --- | --- | --- | --- |
| **Hierarchy Fields** | Agrupación | 1–15 | Niveles de la jerarquía, ej. País > Provincia > Ciudad, o Año > Mes |
| **Filter Measure** | Medida | 0–1 | Oculta miembros con valor cero/vacío y muestra el valor junto a cada elemento, ej. `(9.267,38)` |
| **Tooltips** | Medida | 0–10 | Medidas adicionales al pasar el cursor |

El orden de los campos define la jerarquía: el **primer campo es el nivel raíz** y el último, el nivel hoja.

### Interactuar
- Pulsa el encabezado para expandir o contraer.
- Pulsa una fila para marcarla o desmarcarla. Marcar un padre marca todos sus hijos; las selecciones parciales muestran estado indeterminado.
- Estados del encabezado: `(Todos)` (sin filtro), un valor único, `Múltiple (n)`, o el nombre del **ancestro común** cuando todo lo seleccionado comparte un padre (ej. `Colombia (3)`).
- Iconos de la barra: búsqueda (filtra la lista), Seleccionar todo (casilla), limpiar (`✕`), flecha (expandir/contraer) y, si el autor lo habilita, el interruptor simple/múltiple.
- `Enter` en el buscador acepta, `Esc` lo limpia.
- Clic derecho en una fila abre el menú nativo de Power BI (obtención de detalles).
- Las selecciones filtran los demás visuales y se guardan en el `.pbix`, incluidos marcadores y segmentadores sincronizados.

---

## 2. Referencia completa de propiedades (panel Formato > Visual)

### Menú desplegable
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Texto predeterminado | *(vacío)* | Texto del encabezado cuando no hay selección. Vacío = `(Todos)` localizado. |
| Posición del control | `Superior` | `Superior` / `Inferior` / `Superior derecha` / `Inferior derecha`. `Superior*` expande hacia abajo, `Inferior*` hacia arriba; las variantes `derecha` anclan el control y la lista al borde derecho. |
| Mostrar cuadro de búsqueda | `Sí` | Muestra el icono de búsqueda en el encabezado. |
| Mostrar Seleccionar todo | `Sí` | Muestra el icono Seleccionar todo (se oculta automáticamente en modo selección única). |
| Tamaño de fuente | `12` | Tamaño del texto del encabezado. |
| Ancho del control (px) | `0` | Ancho fijo del encabezado. `0` = ocupa el ancho del visual. |
| Cerrar al salir el mouse | `Sí` | Cierra la lista cuando el puntero sale del control. |
| Cerrar al seleccionar | `No` | Cierra la lista tras cada selección. |
| Altura del control (px) | `36` | Alto de la caja del control. |
| Espacio de etiqueta (px) | `2` | Espacio entre la etiqueta y la caja del control. |

### Desplegable expandido
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Tamaño de fuente | `12` | Tamaño del texto de los elementos. |
| Fuente | `Segoe UI` | Tipografía de los elementos. |
| Negrita | `No` | Elementos en negrita. |
| Cursiva | `No` | Elementos en cursiva. |
| Expandir todo por defecto | `Sí` | Expande todas las ramas al abrir la lista. |
| Ancho del control expandido (px) | `0` | Ancho fijo de la lista. `0` = igual al control. |
| Alto del control expandido (px) | `0` | Alto fijo de la lista. `0` = automático (ajustado al marco). |
| Mostrar valores de medida | `No` | Muestra el valor de la medida en línea junto a cada elemento. |

### Selección múltiple
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Permitir múltiple | `Sí` | `Sí` = selección múltiple. `No` = solo una rama/nodo, se oculta Seleccionar todo y el indicador pasa a cuadrado relleno. |
| Mostrar selección múltiple | `No` | Muestra un interruptor en el encabezado para que el usuario cambie simple/múltiple en tiempo de uso (el cambio se persiste). |
| Color de selección única | `#ef4444` | Relleno y borde del cuadrado relleno usado en modo único. |
| Color del interruptor | `#990000` | Color del botón del encabezado (lo diferencia de Seleccionar todo). |

### Encabezado de segmentación
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Mostrar encabezado | `Sí` | Muestra el título sobre el control. |
| Texto del encabezado | *(vacío)* | Texto del título. Vacío = nombre del primer campo. |
| Tamaño de fuente del encabezado | `12` | Tamaño del título. |
| Color del encabezado | *(tema)* | Color del título. |
| Fuente del encabezado | `Segoe UI` | Tipografía del título. |
| Negrita / Cursiva | `No` | Estilo del título. |

### Filtrado de datos
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Ocultar valores en cero | `Sí` | Elimina miembros cuya medida de filtro sea `0`. |
| Ocultar valores en blanco | `Sí` | Elimina miembros cuya medida de filtro esté vacía. |
| Texto sin registros | *(vacío)* | Mensaje mostrado en la lista cuando no hay datos. Vacío = `- Sin registros -` localizado. |

### Jerarquía y prefijos
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Ignorar mayúsculas/minúsculas | `Sí` | Comparación de prefijos sin distinguir mayúsculas. |
| Prefijos a ignorar Nivel 1…5 | *(vacío)* | Prefijos separados por coma o punto y coma que se recortan del texto mostrado en cada nivel, ej. `Univ.; Universidad`. El nombre nunca queda vacío. |

### Ordenación
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Orden nivel 1 / 2 / 3 | `Alfabético (A-Z)` | Orden por nivel: `Alfabético (A-Z)`, `Alfabético (Z-A)` u `Orden del modelo de datos` (respeta el **Ordenar por columna / OrderBy** del campo). |
| Orden de otros niveles | `Alfabético (A-Z)` | Mismas opciones, aplicadas a los niveles 4 y posteriores. |
| Ignorar orden del objeto visual | `No` | `Sí` ignora el orden elegido en el encabezado (`...` > Ordenar eje) y devuelve el mando a este panel (p. ej. para restaurar el orden del modelo). |

### Colores y estilo
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Fondo del encabezado | *(tema)* | Fondo de la caja del control. |
| Color de texto del encabezado | *(tema)* | Color del texto del encabezado. |
| Fondo del menú desplegable | *(tema)* | Fondo de la lista expandida. |
| Color de texto de elementos | *(tema)* | Color de los elementos de la lista. |
| Color de casilla | *(acento)* | Acento de las casillas de selección múltiple. |
| Borde de selección | `Sí` | Dibuja un borde alrededor del control cuando hay selección activa. |
| Color del borde de selección | `#2563eb` | Color del borde. |
| Grosor del borde de selección | `1` | Grosor del borde en px. |

### Información sobre herramientas
| Propiedad | Defecto | Descripción |
| --- | --- | --- |
| Mostrar información sobre herramientas | `No` | Habilita las tarjetas de información sobre herramientas nativas (incluidas las páginas de información sobre herramientas del informe). |

---

## 3. Notas de comportamiento

- **Modelo de filtrado**: las selecciones se aplican como filtro JSON tuple mediante `applyJsonFilter` (el mismo canal que usa el HierarchySlicer de referencia). Esto da filtrado cruzado fiable, evita errores de selección de puntos de datos del host y persiste en el informe.
- **Persistencia**: la selección actual se restaura desde los filtros del informe en cada actualización, por lo que sobrevive a guardar/reabrir, marcadores y segmentadores sincronizados.
- **Cambio de origen**: si cambian los campos vinculados, el visual reinicia su estado de sesión (universos, cachés, expansiones) y limpia filtros obsoletos automáticamente. Una medida de filtro desalineada se ignora en lugar de ocultar filas.
- **Ejemplos de prefijos**: se muestran en inglés en el panel de formato (los marcadores de posición no son localizables en el modelo de formato actual).
- **Reducción de datos**: usa `window`, que conserva el orden del modelo (sin reordenación Top-N por medida).

---

## 4. Consejos de diseño

- La lista expandida **no puede salirse del marco del visual**: dimensiona el marco con alto suficiente (encabezado + lista). Es la única vía fiable en **Power BI Service**, donde cada visual se ejecuta en un iframe cross-origin y no puede ordenarse por encima de otros.
- En Desktop el visual eleva su contenedor mientras la lista está abierta; en el Service el orden se controla desde el informe.
- Mantén los filtros al frente en el panel **Selección** (o activa *Mantener orden de capas*). Las zonas transparentes dejan pasar los clics, así que lo de atrás sigue siendo editable.
- Las tarjetas de la pestaña **General** (**Fondo**, **Borde del objeto visual**, **Sombra**, **Relleno**, **Título**) pertenecen al contenedor del host (`visualContainerObjects`), no al visual. `capabilities.json` no tiene opción para ellas, así que no pueden predefinirse — ver **sección 5**.

---

## 5. Ocultar el fondo y el borde del contenedor

El marco fino que se ve alrededor del control **no** lo dibuja el visual: es el **contenedor del host** (`visualContainerObjects`). No existe ninguna propiedad del visual para ello, así que debe desactivarse en el informe.

### Opción A — Por visual
1. Selecciona el objeto visual.
2. **Formato del objeto visual** (rodillo) > pestaña **General**.
3. Despliega **Efectos**:
   - **Fondo** → desactivar (o dejarlo activo con **Transparencia = 100%**).
   - **Borde del objeto visual** → desactivar.
   - **Sombra** → desactivar (opcional).
4. Si el visual queda ajustado, define **Propiedades > Relleno** explícitamente (ver nota).

### Opción B — Todo el informe
1. **Vista** > **Temas** > **Valores predeterminados de los objetos visuales** (o **Personalizar tema actual**).
2. Desactiva **Fondo** y **Borde**.
3. Todos los visuales que no estén personalizados individualmente heredan esos valores.

### Opción C — Tema JSON reutilizable
```json
{
  "name": "Sin marco de contenedor",
  "visualStyles": {
    "*": { "*": {
      "background": [{ "show": false }],
      "border": [{ "show": false }],
      "dropShadow": [{ "show": false }]
    }}
  }
}
```
Impórtalo desde **Vista** > **Temas** > **Buscar temas**.

> **Nota:** en cuanto un visual declara cualquier ajuste de contenedor (fondo, borde, título…), Power BI deja de heredar el **Relleno** por defecto del tema para ese visual y lo pone a `0`. Define **Propiedades > Relleno** explícitamente si necesitas espacio.

---

## 6. Localización

El visual incluye traducciones completas para `en-US`, `es-ES`, `it-IT`, `fr-FR` y `de-DE`.

---

## 7. Historial de cambios (reciente)

- **1.0.0.21**: filtrado migrado a JSON tuple (`applyJsonFilter`) + sincronización de filtros.
- **1.0.0.22**: robustez ante vistas de datos degeneradas.
- **1.0.0.23**: el encabezado muestra el ancestro común.
- **1.0.0.24**: la ventana de datos conserva el orden del modelo.
- **1.0.0.25–1.0.0.27**: altura del control, espacio de etiqueta, posiciones `Superior derecha` / `Inferior derecha`.
- **1.0.0.28–1.0.0.31**: fuente/negrita/cursiva del encabezado, tipografía de `Desplegable expandido`, textos por defecto en inglés, valores de medida movidos y apagados por defecto.
- **1.0.0.32**: orden por nivel (1–3) e `Ignorar orden del objeto visual`.
- **1.0.0.33**: seleccionar todo conserva las marcas; resiliencia ante cambios de origen.
- **1.0.0.34**: revisión técnica de localización.
- **1.0.0.35–1.0.0.36**: título visible sin datos, encabezado estable guiado por el filtro propio, espaciado coherente.
- **1.0.0.37**: espacio de etiqueta por defecto 2px.
- **1.0.0.38–1.0.0.41**: modo de selección simple/múltiple, indicador cuadrado relleno, interruptor en el encabezado, tarjeta `Selección múltiple` (`Permitir múltiple` activado por defecto).
- **1.0.0.42**: elevación del contenedor del host mientras la lista está abierta; limitación de plataforma documentada en Service.
- **1.0.0.43**: geometría del desplegable recalculada al abrir la búsqueda (mantiene la lista dentro del marco) y foco sin desplazamiento.
- **1.0.0.44**: el contenedor del host se vuelve a localizar en cada elevación (sobrevive a re-renderizados del host) y el apilado se reafirma poco después de abrir, para que la lista conserve su capa tras usar otros controles.
- **1.0.0.45**: los botones de acción de la cabecera (búsqueda, Seleccionar todo, limpiar, simple/múltiple) ya no detienen la propagación del evento, de modo que Power BI detecta el clic y eleva el visual — esto era lo que dejaba el cuadro de búsqueda detrás de otros controles. La cabecera ignora esos clics internamente y la elevación cubre ahora también el propio iframe y los contenedores `visual-container` / `-modern` / `-group`.
