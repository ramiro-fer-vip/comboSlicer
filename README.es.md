# comboSlicer

Segmentación desplegable jerárquica para Power BI. Versión **1.0.0.31**.

## 1. Mini manual de uso

### Instalación
1. Toma el paquete `.pbiviz` de `dist/`.
2. En Power BI Desktop: `...` (más objetos visuales) > **Importar un objeto visual desde un archivo** y selecciona el paquete.
3. El visual `comboSlicer` aparece en el panel de visualizaciones.

### Asignar datos
Arrastra campos a los roles del visual:
- **Hierarchy Fields** (1–15 columnas): los niveles de jerarquía, ej. País > Provincia > Ciudad, o Año > Mes.
- **Filter Measure** (opcional, 0–1): oculta miembros con valor cero/vacío y muestra el valor junto a cada elemento, ej. `(9.267,38)`.
- **Tooltips** (opcional, 0–10): medidas adicionales al pasar el cursor.

### Interactuar
- Pulsa el encabezado para expandir/contraer. Pulsa una fila para marcarla; marcar un padre marca todos sus hijos.
- Estados del encabezado: `(Todos)` = sin filtro, un valor único, `Múltiple (n)`, o el nombre del ancestro común cuando todo lo marcado comparte un padre (ej. `Colombia (3)`).
- Usa la lupa para buscar, el icono de casilla para Seleccionar todo y `✕` para limpiar.
- `Enter` acepta la búsqueda, `Esc` la limpia.
- Clic derecho en una fila para el menú nativo (drill through).
- Las selecciones filtran los demás visuales del informe y se guardan en el `.pbix` (incluidos marcadores y segmentadores sincronizados).

### Formato (pestaña Visual)
- **Dropdown**: texto de marcador; posición (`Top`, `Bottom`, `Top-right`, `Bottom-right` — las variantes `-right` anclan el control al borde derecho); buscador; Seleccionar todo; tamaño de fuente; ancho fijo del encabezado; cerrar al salir el ratón; cerrar al seleccionar; altura del control (defecto `36`); espacio de etiqueta (defecto `4`).
- **Slicer header**: título opcional sobre el control (por defecto el nombre del campo), con fuente, negrita y cursiva.
- **Dropdown expanded**: expandir todo por defecto; ancho/alto expandidos (`0` = automático); tipografía de la lista — tamaño (defecto `12`), fuente (`Segoe UI`), negrita, cursiva; mostrar valores de medida (defecto apagado).
- **Data Filtering**: ocultar ceros/vacíos, texto de estado vacío.
- **Hierarchy & Prefixes**: prefijos por nivel (separados por comas) a recortar del texto (ej. `Univ., Universidad`), ignorando mayúsculas.
- **Sorting**: `Alfabético (A-Z)` por defecto; también `Z-A` y `Orden del modelo` (respeta el OrderBy del campo), para todos los niveles o uno solo. El orden del encabezado del visual (menú `...`) tiene prioridad.
- **Colors & Style**: fondos de encabezado/desplegable, colores de texto, acento de casillas, borde de selección.

### Consejos de diseño
- La lista expandida no puede salirse del marco del visual: dimensiona el marco con alto suficiente (encabezado + lista).
- Mantén los filtros al frente en el panel **Selección**; el área vacía deja pasar los clics y lo de atrás sigue editable.
- Las tarjetas de la pestaña **General** (fondo, efectos, relleno, título) pertenecen al contenedor del host y el visual no puede predefinirlas — usa un tema de informe para valores uniformes.

## 2. Características principales
- Segmentador jerárquico multinivel con UX de desplegable.
- Filtrado por filtro JSON tuple (mismo canal que HierarchySlicer): filtrado cruzado fiable, persistencia y sin errores de selección del host.
- Recorte de prefijos por nivel, localización en 5 idiomas (`en-US`, `es-ES`, `it-IT`, `fr-FR`, `de-DE`).
- Ocultación de miembros sin datos guiada por medida, con valores en línea y tooltips.

## 3. Cambios recientes
- **1.0.0.21**: filtrado migrado a JSON tuple (`applyJsonFilter`) + sincronización de filtros; selección restaurada desde los filtros del informe.
- **1.0.0.22**: robustez ante vistas de datos degeneradas (cambios de visual).
- **1.0.0.23**: el encabezado muestra el ancestro común (`Colombia (3)`).
- **1.0.0.24**: ventana de datos en orden del modelo (sin orden por medida).
- **1.0.0.25**: altura del control (defecto 36) y espacio superior (defecto 0); defecto de orden de vuelta a A-Z.
- **1.0.0.26**: posiciones `Top-right` / `Bottom-right` (control anclado a la derecha).
- **1.0.0.27**: espacio superior reemplazado por espacio de etiqueta (defecto 4).
- **1.0.0.28**: fuente, negrita y cursiva en el encabezado.
- **1.0.0.29**: tarjeta de tipografía `Dropdown expanded`; ejemplos de prefijos en inglés; separador `;` en prefijos.
- **1.0.0.30**: ancho/alto/expandir-todo movidos a `Dropdown expanded`; valores tipográficos concretos (12, Segoe UI).
- **1.0.0.31**: textos por defecto en inglés; fuente del encabezado Segoe UI; Mostrar valores movido a `Dropdown expanded`, apagado por defecto.
