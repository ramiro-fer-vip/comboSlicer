# comboSlicer

Hierarchischer Dropdown-Slicer für Power BI. Version **1.0.0.31**.

## 1. Mini-Benutzerhandbuch

### Installation
1. Nimm das `.pbiviz`-Paket aus `dist/`.
2. In Power BI Desktop: `...` (weitere Visuals) > **Visuelles aus einer Datei importieren** und wähle das Paket.
3. Das Visual `comboSlicer` erscheint im Bereich „Visualisierungen“.

### Daten zuweisen
Ziehe Felder auf die Datenrollen des Visuals:
- **Hierarchy Fields** (1–15 Spalten): die Hierarchieebenen, z. B. Land > Provinz > Stadt oder Jahr > Monat.
- **Filter Measure** (optional, 0–1): blendet Mitglieder mit Null-/Leerwerten aus und zeigt den Wert neben jedem Eintrag, z. B. `(9.267,38)`.
- **Tooltips** (optional, 0–10): zusätzliche Measures beim Darüberfahren.

### Interaktion
- Klicke die Kopfzeile zum Erweitern/Reduzieren. Klicke eine Zeile zum Markieren; ein markierter übergeordneter Knoten markiert alle Kinder.
- Kopfzeilenstatus: `(Alle)` = kein Filter, ein einzelner Wert, `Mehrfach (n)`, oder der Name des gemeinsamen Vorfahren, wenn die gesamte Auswahl einen Elternknoten teilt (z. B. `Colombia (3)`).
- Nutze die Lupe zur Suche, das Kästchensymbol für Alle auswählen und `✕` zum Löschen.
- `Eingabe` bestätigt die Suche, `Esc` löscht sie.
- Rechtsklick auf eine Zeile für das native Menü (Drillthrough).
- Auswahl filtert alle anderen Visuals des Berichts und wird in der `.pbix` gespeichert (einschließlich Lesezeichen und synchronisierter Slicer).

### Formatierung (Registerkarte Visual)
- **Dropdown**: Platzhaltertext; Steuerelementposition (`Top`, `Bottom`, `Top-right`, `Bottom-right` — die `-right`-Varianten docken das Steuerelement rechts an); Suchfeld; Alle auswählen; Schriftgröße; feste Kopfbreite; bei Mausverlassen schließen; bei Auswahl schließen; Steuerelementhöhe (Standard `36`); Beschriftungsabstand (Standard `4`).
- **Slicer header**: optionale Überschrift über dem Steuerelement (Standard: Feldname), mit Schriftart, Fett und Kursiv.
- **Dropdown expanded**: standardmäßig alles erweitern; erweiterte Breite/Höhe (`0` = automatisch); Listentypografie — Größe (Standard `12`), Schriftart (`Segoe UI`), Fett, Kursiv; Messwerte anzeigen (standardmäßig aus).
- **Data Filtering**: Null-/Leerwerte ausblenden, Text für leeren Zustand.
- **Hierarchy & Prefixes**: Präfixe pro Ebene (kommagetrennt) aus der Anzeige entfernen (z. B. `Univ., Universität`), Groß-/Kleinschreibung egal.
- **Sorting**: Standard `Alphabetisch (A-Z)`; auch `Z-A` und `Modellreihenfolge` (beachtet das OrderBy des Felds), für alle Ebenen oder eine einzelne. Die Sortierung über die Visual-Kopfzeile (Menü `...`) hat Vorrang.
- **Colors & Style**: Kopf-/Listenhintergründe, Textfarben, Checkbox-Akzent, Auswahlrahmen.

### Layout-Tipps
- Die erweiterte Liste kann den Visual-Rahmen nicht verlassen: dimensioniere den Rahmen hoch genug (Kopf + Liste).
- Halte Slicer im Bereich **Auswahl** im Vordergrund; der leere Bereich lässt Klicks durch, dahinterliegende Visuals bleiben bearbeitbar.
- Die Karten der Registerkarte **Allgemein** (Hintergrund, Effekte, Abstand, Titel) gehören zum Host-Container und können vom Visual nicht voreingestellt werden — nutze ein Berichtdesign für einheitliche Werte.

## 2. Hauptmerkmale
- Mehrstufiger hierarchischer Slicer mit Dropdown-UX.
- Filterung per JSON-Tupel-Filter (gleicher Kanal wie HierarchySlicer): zuverlässiges Cross-Filtering, Persistenz und keine Host-Auswahlfehler.
- Präfixkürzung pro Ebene, Lokalisierung in 5 Sprachen (`en-US`, `es-ES`, `it-IT`, `fr-FR`, `de-DE`).
- Measure-gesteuertes Ausblenden leerer Mitglieder, mit Inline-Werten und Tooltips.

## 3. Letzte Änderungen
- **1.0.0.21**: Filterung auf JSON-Tupel (`applyJsonFilter`) umgestellt + Filtersynchronisierung; Auswahl aus Berichtsfiltern wiederhergestellt.
- **1.0.0.22**: Robustheit gegen degenerierte Datenansichten (Visual-Wechsel).
- **1.0.0.23**: Kopfzeile zeigt gemeinsamen Vorfahren (`Colombia (3)`).
- **1.0.0.24**: Datenfenster in Modellreihenfolge (keine Measure-Sortierung).
- **1.0.0.25**: Steuerelementhöhe (Standard 36) und oberer Abstand (Standard 0); Standardsortierung zurück auf A-Z.
- **1.0.0.26**: Positionen `Top-right` / `Bottom-right` (rechts angedocktes Steuerelement).
- **1.0.0.27**: oberer Abstand durch Beschriftungsabstand ersetzt (Standard 4).
- **1.0.0.28**: Schriftart, Fett und Kursiv in der Kopfzeile.
- **1.0.0.29**: Typografie-Karte `Dropdown expanded`; Präfix-Beispiele auf Englisch; Trennzeichen `;` für Präfixe.
- **1.0.0.30**: Breite/Höhe/Alles-erweitern nach `Dropdown expanded` verschoben; konkrete Typografiewerte (12, Segoe UI).
- **1.0.0.31**: Standardtexte auf Englisch; Kopfzeilen-Schriftart Segoe UI; Messwerte nach `Dropdown expanded` verschoben, standardmäßig aus.
