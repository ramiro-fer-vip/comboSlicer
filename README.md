# comboSlicer

Hierarchical dropdown slicer for Power BI. Version **1.0.0.31**.

## 1. Mini user manual

### Install
1. Take the `.pbiviz` package from `dist/`.
2. In Power BI Desktop: `...` (more visuals) > **Import a visual from a file** and select the package.
3. The `comboSlicer` visual appears in the Visualizations pane.

### Assign data
Drag fields to the visual data roles:
- **Hierarchy Fields** (1–15 columns): the drill-down levels, e.g. Country > State > City, or Year > Month.
- **Filter Measure** (optional, 0–1): hides members with zero/blank values and shows the value next to each item, e.g. `(9,267.38)`.
- **Tooltips** (optional, 0–10): extra measures shown on hover.

### Interact
- Click the header to expand/collapse. Click a row to check/uncheck it; checking a parent checks all its children.
- Header states: `(All)` = no filter, a single value name, `Multiple (n)`, or the common ancestor name when everything selected shares one parent (e.g. `Colombia (3)`).
- Use the search icon to filter the list, the checkbox icon for Select All, and `✕` to clear.
- Press `Enter` to accept the search, `Esc` to clear it.
- Right-click a row for the native menu (drill through).
- Selections filter every other visual in the report and are saved in the `.pbix` (including bookmarks and synced slicers).

### Format (Visual tab)
- **Dropdown**: placeholder text; control position (`Top`, `Bottom`, `Top-right`, `Bottom-right` — the `-right` variants dock the control to the right edge); search box; Select All; font size; fixed header width; close on mouse leave; close on selection; control height (default `36`); label spacing (default `4`).
- **Slicer header**: optional title above the control (defaults to the field name), with font, bold and italic.
- **Dropdown expanded**: expand-all by default; expanded width/height (`0` = automatic); list typography — font size (default `12`), font (`Segoe UI`), bold, italic; show measure values (default off).
- **Data Filtering**: hide zero/blank values, custom empty-state text.
- **Hierarchy & Prefixes**: per-level comma-separated prefixes to trim from display (e.g. `Univ., Universidad`), ignoring case.
- **Sorting**: `Alphabetical (A-Z)` by default; also `Z-A` and `Data model order` (respects the field's OrderBy), applied to all levels or a single level. Sorting from the visual header (`...` menu) takes precedence.
- **Colors & Style**: header/dropdown backgrounds, text colors, checkbox accent, selection border.

### Layout tips
- The expanded list cannot overflow the visual frame: size the frame tall enough to contain header + list.
- Keep slicers at the front in the **Selection** pane; the empty area is click-through, so visuals behind stay editable.
- `General` tab cards (Background, Effects, Padding, Title) belong to the host container and cannot be preset by the visual — use a report theme for uniform defaults.

## 2. Main characteristics
- Multi-level hierarchical slicer with dropdown UX.
- Filtering via JSON tuple filter (same channel as HierarchySlicer): reliable cross-filtering, persistence and no host selection errors.
- Prefix trimming per level, 5-language localization (`en-US`, `es-ES`, `it-IT`, `fr-FR`, `de-DE`).
- Measure-driven hiding of empty members with inline values and tooltips.

## 3. Recent changelog
- **1.0.0.21**: filtering migrated to JSON tuple (`applyJsonFilter`) + filter-state sync; selection restored from report filters.
- **1.0.0.22**: hardened against degenerate data views (visual switching scenarios).
- **1.0.0.23**: header shows the common ancestor name (`Colombia (3)`).
- **1.0.0.24**: data window preserves model order (no measure-based ordering).
- **1.0.0.25**: configurable control height (default 36) and top spacing (default 0); default sort back to A-Z.
- **1.0.0.26**: `Top-right` / `Bottom-right` positions (right-docked control).
- **1.0.0.27**: top spacing replaced by label spacing (default 4).
- **1.0.0.28**: header font family, bold and italic options.
- **1.0.0.29**: `Dropdown expanded` typography card; prefix examples in English; `;` separator for prefixes.
- **1.0.0.30**: width/height/expand-all moved to `Dropdown expanded`; concrete typography defaults (12, Segoe UI).
- **1.0.0.31**: English defaults (empty text, placeholders, tooltips); header font default Segoe UI; Show measure values moved to `Dropdown expanded`, off by default.
