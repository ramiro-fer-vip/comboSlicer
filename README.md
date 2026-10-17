# comboSlicer

Hierarchical dropdown slicer for Power BI. Version **1.0.0.42**.

A dropdown slicer that builds a multi-level hierarchy from several fields, filters the report through the standard Power BI filter model, and supports prefix trimming, sorting, measure-driven filtering and single/multi selection.

---

## 1. Mini user manual

### Install
1. Get the `.pbiviz` package from the `comboSilcer` folder at https://github.com/ramiro-fer-vip/comboSlicer/.
2. In Power BI Desktop: `...` (more visuals) > **Import a visual from a file** and select the package.
3. The `comboSlicer` visual appears in the Visualizations pane. Pin it for quick reuse.

### Assign data
| Role | Kind | Range | Purpose |
| --- | --- | --- | --- |
| **Hierarchy Fields** | Grouping | 1–15 | Drill-down levels, e.g. Country > State > City, or Year > Month |
| **Filter Measure** | Measure | 0–1 | Hides members with zero/blank values and shows the value next to each item, e.g. `(9,267.38)` |
| **Tooltips** | Measure | 0–10 | Extra measures available on hover |

Field order defines the hierarchy: the **first field is the root level** and the last one is the leaf level.

### Interact
- Click the header to expand/collapse.
- Click a row to check/uncheck it. Checking a parent checks all its children; partial selections show an indeterminate state.
- Header states: `(All)` (no filter), a single value name, `Multiple (n)`, or the **common ancestor** name when everything selected shares one parent (e.g. `Colombia (3)`).
- Toolbar icons: search (filters the list), Select All (checkbox), clear (`✕`), caret (expand/collapse), and, when enabled by the author, the single/multiple toggle.
- Press `Enter` in the search box to accept, `Esc` to clear it.
- Right-click a row for the native Power BI menu (drill through).
- Selections filter every other visual and are persisted in the `.pbix`, including bookmarks and synchronized slicers.

---

## 2. Complete property reference (Format pane > Visual)

### Dropdown
| Property | Default | Description |
| --- | --- | --- |
| Default placeholder | *(empty)* | Text shown in the header when there is no selection. Empty = localized `(All)`. |
| Control position | `Top` | `Top` / `Bottom` / `Top-right` / `Bottom-right`. `Top*` expands downwards, `Bottom*` upwards; the `-right` variants dock the control and list to the right edge. |
| Show search box | `On` | Shows the search icon in the header. |
| Show Select All | `On` | Shows the Select All icon (hidden automatically in single-select mode). |
| Font size | `12` | Font size of the header text. |
| Original control width (px) | `0` | Fixed header width. `0` = fill the visual width. |
| Close on mouse leave | `On` | Closes the list when the pointer leaves the control. |
| Close on selection | `Off` | Closes the list after each selection. |
| Control height (px) | `36` | Height of the control box. |
| Label spacing (px) | `2` | Space between the header label and the control box. |

### Dropdown expanded
| Property | Default | Description |
| --- | --- | --- |
| Font size | `12` | Item font size. |
| Font | `Segoe UI` | Item font family. |
| Bold | `Off` | Bold items. |
| Italic | `Off` | Italic items. |
| Expand all by default | `On` | Expands every branch when the list opens. |
| Expanded width (px) | `0` | Fixed list width. `0` = same width as the control. |
| Expanded height (px) | `0` | Fixed list height. `0` = automatic (clamped to the frame). |
| Show measure values | `Off` | Shows the Filter Measure value inline next to each item. |

### Multiple Select
| Property | Default | Description |
| --- | --- | --- |
| Allow multiple | `On` | `On` = multi-select. `Off` = only one branch/node can be selected, Select All is hidden and the indicator becomes a filled square. |
| Show Multiple Selection | `Off` | Shows an end-user toggle in the header so the report consumer can switch single/multiple at runtime (the change is persisted). |
| Single-select color | `#ef4444` | Fill/border of the filled-square indicator used in single mode. |
| Toggle color | `#990000` | Color of the header toggle button (separates it from Select All). |

### Slicer header
| Property | Default | Description |
| --- | --- | --- |
| Show header | `On` | Shows the title above the control. |
| Header text | *(empty)* | Title text. Empty = the first field's name. |
| Header font size | `12` | Title font size. |
| Header font color | *(theme)* | Title color. |
| Header font | `Segoe UI` | Title font family. |
| Bold / Italic | `Off` | Title style. |

### Data Filtering
| Property | Default | Description |
| --- | --- | --- |
| Hide zero values | `On` | Removes members whose Filter Measure is `0`. |
| Hide blank values | `On` | Removes members whose Filter Measure is blank. |
| Empty state text | *(empty)* | Message shown in the list when there is no data. Empty = localized `- No records -`. |

### Hierarchy & Prefixes
| Property | Default | Description |
| --- | --- | --- |
| Ignore case in prefixes | `On` | Case-insensitive prefix matching. |
| Ignored prefixes Level 1…5 | *(empty)* | Comma or semicolon separated prefixes to trim from the displayed text of each level, e.g. `Univ.; Universidad`. The name is never left empty. |

### Sorting
| Property | Default | Description |
| --- | --- | --- |
| Level 1 / 2 / 3 order | `Alphabetical (A-Z)` | Per-level order: `Alphabetical (A-Z)`, `Alphabetical (Z-A)` or `Data model order` (respects the field's **Sort by column / OrderBy**). |
| Other levels order | `Alphabetical (A-Z)` | Same options, applied to levels 4 and deeper. |
| Ignore visual header sort | `Off` | `On` ignores the sort chosen from the visual header (`...` > Sort axis), returning control to this pane (e.g. to restore the data-model order). |

### Colors & Style
| Property | Default | Description |
| --- | --- | --- |
| Header background | *(theme)* | Background of the control box. |
| Header text color | *(theme)* | Color of the header text. |
| Dropdown background | *(theme)* | Background of the expanded list. |
| Item text color | *(theme)* | Color of the list items. |
| Checkbox accent color | *(accent)* | Accent of the multi-select checkboxes. |
| Selection border | `On` | Draws a border around the control when there is an active selection. |
| Selection border color | `#2563eb` | Border color. |
| Selection border width | `1` | Border width in px. |

### Tooltip
| Property | Default | Description |
| --- | --- | --- |
| Show tooltips | `Off` | Enables the native tooltip cards (including report tooltip pages). |

---

## 3. Behaviour notes

- **Filtering model**: selections are applied as a JSON tuple filter through `applyJsonFilter` (the same channel used by the reference HierarchySlicer). This gives reliable cross-filtering, avoids host data-point selection errors, and persists in the report.
- **Persistence**: the current selection is restored from the report filters on every update, so it survives save/reopen, bookmarks, and synchronized slicers.
- **Source changes**: if the bound fields change, the visual resets its session state (universes, caches, expansions) and clears stale filters automatically. A misaligned Filter Measure is ignored instead of hiding rows.
- **Prefix examples** are shown in English in the formatting pane (placeholders are not localizable in the current formatting model).
- **Data reduction** uses `window`, which preserves the model order (no measure-based top-N reordering).

---

## 4. Layout tips

- The expanded list **cannot overflow the visual frame**: size the frame tall enough to contain header + list. This is the only reliable approach in **Power BI Service**, where each visual runs in a cross-origin iframe and cannot reorder itself above other visuals.
- In Desktop the visual raises its host container while the list is open; in the Service the order is controlled from the report.
- Keep slicers at the front in the **Selection** pane (or enable *Maintain layer order*). Transparent areas are click-through, so visuals behind remain editable.
- `General` tab cards (Background, Effects, Padding, Title) belong to the host container and cannot be preset by the visual — use a report theme for uniform defaults.

---

## 5. Localization

The visual ships with full translations for `en-US`, `es-ES`, `it-IT`, `fr-FR` and `de-DE`.

---

## 6. Changelog (recent)

- **1.0.0.21**: filtering migrated to JSON tuple (`applyJsonFilter`) + filter-state sync.
- **1.0.0.22**: hardened against degenerate data views.
- **1.0.0.23**: header shows the common ancestor name.
- **1.0.0.24**: data window preserves model order.
- **1.0.0.25–1.0.0.27**: control height, label spacing, `Top-right` / `Bottom-right` positions.
- **1.0.0.28–1.0.0.31**: header font/bold/italic, `Dropdown expanded` typography, English defaults, measure values moved and off by default.
- **1.0.0.32**: per-level sort (1–3) and `Ignore visual header sort`.
- **1.0.0.33**: selecting everything keeps the checks; resilience to source changes.
- **1.0.0.34**: technical localization review.
- **1.0.0.35–1.0.0.36**: header title shown with no data, stable header driven by the own filter, consistent spacing.
- **1.0.0.37**: label spacing default 2px.
- **1.0.0.38–1.0.0.41**: single/multiple selection mode, filled-square indicator, header toggle, `Multiple Select` card (`Allow multiple` on by default).
- **1.0.0.42**: best-effort host-container raise while the list is open; documented platform limit in Service.
