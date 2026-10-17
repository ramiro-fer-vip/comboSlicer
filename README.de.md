# comboSlicer

Hierarchischer Dropdown-Slicer für Power BI. Version **1.0.0.42**.

Ein Dropdown-Slicer, der aus mehreren Feldern eine mehrstufige Hierarchie aufbaut, den Bericht über das Standard-Filtermodell von Power BI filtert und Präfixkürzung, Sortierung, measuregesteuerte Filterung sowie Einzel-/Mehrfachauswahl unterstützt.

---

## 1. Mini-Benutzerhandbuch

### Installation
1. Nimm das `.pbiviz`-Paket aus dem Ordner `comboSilcer` unter https://github.com/ramiro-fer-vip/comboSlicer/.
2. In Power BI Desktop: `...` (weitere Visuals) > **Visuelles aus einer Datei importieren** und das Paket wählen.
3. Das Visual `comboSlicer` erscheint im Bereich „Visualisierungen“. Für die Wiederverwendung anheften.

### Daten zuweisen
| Rolle | Typ | Bereich | Zweck |
| --- | --- | --- | --- |
| **Hierarchy Fields** | Gruppierung | 1–15 | Hierarchieebenen, z. B. Land > Provinz > Stadt oder Jahr > Monat |
| **Filter Measure** | Measure | 0–1 | Blendet Mitglieder mit Null-/Leerwerten aus und zeigt den Wert neben jedem Eintrag, z. B. `(9.267,38)` |
| **Tooltips** | Measure | 0–10 | Zusätzliche Measures beim Darüberfahren |

Die Feldreihenfolge bestimmt die Hierarchie: das **erste Feld ist die Wurzelebene**, das letzte die Blattebene.

### Interaktion
- Klicke die Kopfzeile zum Erweitern/Reduzieren.
- Klicke eine Zeile zum Markieren/Entmarkieren. Ein markierter Elternknoten markiert alle Kinder; teilweise Auswahl zeigt einen unbestimmten Zustand.
- Kopfzeilenstatus: `(Alle)` (kein Filter), ein einzelner Wert, `Mehrfach (n)`, oder der Name des **gemeinsamen Vorfahren**, wenn die gesamte Auswahl einen Elternknoten teilt (z. B. `Colombia (3)`).
- Symbolleiste: Suche (filtert die Liste), Alle auswählen (Kästchen), Löschen (`✕`), Pfeil (erweitern/reduzieren) und, wenn vom Autor aktiviert, der Einzel/Mehrfach-Schalter.
- `Eingabe` im Suchfeld bestätigt, `Esc` löscht.
- Rechtsklick auf eine Zeile öffnet das native Power BI-Menü (Drillthrough).
- Auswahl filtert alle anderen Visuals und wird in der `.pbix` gespeichert, einschließlich Lesezeichen und synchronisierter Slicer.

---

## 2. Vollständige Eigenschaftenreferenz (Formatbereich > Visual)

### Dropdown
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Standardtext | *(leer)* | Text der Kopfzeile ohne Auswahl. Leer = lokalisiertes `(Alle)`. |
| Position des Steuerelements | `Oben` | `Oben` / `Unten` / `Oben-rechts` / `Unten-rechts`. `Oben*` erweitert nach unten, `Unten*` nach oben; die `-rechts`-Varianten docken Steuerelement und Liste rechts an. |
| Suchfeld anzeigen | `Ein` | Zeigt das Suchsymbol in der Kopfzeile. |
| „Alles auswählen“ anzeigen | `Ein` | Zeigt das Symbol „Alles auswählen“ (im Einzelmodus automatisch ausgeblendet). |
| Schriftgröße | `12` | Schriftgröße des Kopfzeilentexts. |
| Steuerelementbreite (px) | `0` | Feste Breite der Kopfzeile. `0` = füllt die Visualbreite. |
| Schließen beim Verlassen der Maus | `Ein` | Schließt die Liste, wenn der Zeiger das Steuerelement verlässt. |
| Schließen bei Auswahl | `Aus` | Schließt die Liste nach jeder Auswahl. |
| Steuerelementhöhe (px) | `36` | Höhe des Steuerelementkastens. |
| Beschriftungsabstand (px) | `2` | Abstand zwischen Beschriftung und Steuerelementkasten. |

### Erweiterte Liste
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Schriftgröße | `12` | Schriftgröße der Einträge. |
| Schriftart | `Segoe UI` | Schriftart der Einträge. |
| Fett | `Aus` | Fette Einträge. |
| Kursiv | `Aus` | Kursive Einträge. |
| Standardmäßig alle erweitern | `Ein` | Erweitert beim Öffnen alle Zweige. |
| Erweiterte Breite (px) | `0` | Feste Listenbreite. `0` = wie das Steuerelement. |
| Erweiterte Höhe (px) | `0` | Feste Listenhöhe. `0` = automatisch (auf den Rahmen begrenzt). |
| Messwerte anzeigen | `Aus` | Zeigt den Wert des Filtermeasures inline neben jedem Eintrag. |

### Mehrfachauswahl
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Mehrfachauswahl zulassen | `Ein` | `Ein` = Mehrfachauswahl. `Aus` = nur ein Zweig/Knoten, „Alles auswählen“ ist ausgeblendet und die Anzeige wird zu einem gefüllten Quadrat. |
| Mehrfachauswahl anzeigen | `Aus` | Zeigt einen Schalter in der Kopfzeile, damit der Nutzer zur Laufzeit zwischen Einzel und Mehrfach wechseln kann (die Änderung wird gespeichert). |
| Farbe der Einzelauswahl | `#ef4444` | Füllung und Rahmen des gefüllten Quadrats im Einzelmodus. |
| Umschalterfarbe | `#990000` | Farbe des Kopfzeilenschalters (unterscheidet ihn von „Alles auswählen“). |

### Datenschnitt-Header
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Kopfzeile anzeigen | `Ein` | Zeigt den Titel über dem Steuerelement. |
| Kopfzeilentext | *(leer)* | Titeltext. Leer = Name des ersten Felds. |
| Schriftgröße der Kopfzeile | `12` | Größe des Titels. |
| Kopfzeilenfarbe | *(Design)* | Farbe des Titels. |
| Kopfzeilenschriftart | `Segoe UI` | Schriftart des Titels. |
| Fett / Kursiv | `Aus` | Stil des Titels. |

### Datenfilterung
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Nullwerte ausblenden | `Ein` | Entfernt Mitglieder, deren Filtermeasure `0` ist. |
| Leere Werte ausblenden | `Ein` | Entfernt Mitglieder, deren Filtermeasure leer ist. |
| Text für keine Datensätze | *(leer)* | Meldung in der Liste ohne Daten. Leer = lokalisiertes `- Keine Datensätze -`. |

### Hierarchie und Präfixe
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Groß-/Kleinschreibung ignorieren | `Ein` | Präfixvergleich ohne Beachtung der Groß-/Kleinschreibung. |
| Zu ignorierende Präfixe Ebene 1…5 | *(leer)* | Durch Komma oder Semikolon getrennte Präfixe, die vom angezeigten Text jeder Ebene entfernt werden, z. B. `Univ.; Universität`. Der Name bleibt nie leer. |

### Sortierung
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Sortierung Ebene 1 / 2 / 3 | `Alphabetisch (A-Z)` | Sortierung pro Ebene: `Alphabetisch (A-Z)`, `Alphabetisch (Z-A)` oder `Datenmodellreihenfolge` (beachtet **Sortieren nach Spalte / OrderBy** des Felds). |
| Sortierung weiterer Ebenen | `Alphabetisch (A-Z)` | Dieselben Optionen für Ebene 4 und tiefer. |
| Kopfzeilen-Sortierung ignorieren | `Aus` | `Ein` ignoriert die in der Kopfzeile gewählte Sortierung (`...` > Achse sortieren) und gibt die Kontrolle an diesen Bereich zurück (z. B. um die Modellreihenfolge wiederherzustellen). |

### Farben und Stil
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| Kopfzeilenhintergrund | *(Design)* | Hintergrund des Steuerelementkastens. |
| Kopfzeilentextfarbe | *(Design)* | Farbe des Kopfzeilentexts. |
| Dropdown-Hintergrund | *(Design)* | Hintergrund der erweiterten Liste. |
| Elementtextfarbe | *(Design)* | Farbe der Listeneinträge. |
| Kontrollkästchenfarbe | *(Akzent)* | Akzent der Mehrfachauswahl-Kästchen. |
| Auswahlrahmen | `Ein` | Zeichnet einen Rahmen um das Steuerelement bei aktiver Auswahl. |
| Farbe des Auswahlrahmens | `#2563eb` | Rahmenfarbe. |
| Breite des Auswahlrahmens | `1` | Rahmenbreite in px. |

### QuickInfo
| Eigenschaft | Standard | Beschreibung |
| --- | --- | --- |
| QuickInfos anzeigen | `Aus` | Aktiviert die nativen QuickInfo-Karten (einschließlich QuickInfo-Seiten des Berichts). |

---

## 3. Verhaltenshinweise

- **Filtermodell**: Auswahlen werden als JSON-Tupel-Filter über `applyJsonFilter` angewendet (derselbe Kanal wie HierarchySlicer). Das ergibt zuverlässiges Cross-Filtering, vermeidet Auswahlfehler bei Datenpunkten des Hosts und bleibt im Bericht erhalten.
- **Persistenz**: Die aktuelle Auswahl wird bei jeder Aktualisierung aus den Berichtsfiltern wiederhergestellt und übersteht daher Speichern/Neuöffnen, Lesezeichen und synchronisierte Slicer.
- **Quellwechsel**: Ändern sich die gebundenen Felder, setzt das Visual seinen Sitzungszustand zurück (Universen, Caches, Erweiterungen) und bereinigt veraltete Filter automatisch. Ein fehlausgerichtetes Filtermeasure wird ignoriert, statt Zeilen auszublenden.
- **Präfixbeispiele**: im Formatbereich auf Englisch (Platzhalter sind im aktuellen Formatmodell nicht lokalisierbar).
- **Datenreduktion**: nutzt `window`, wodurch die Modellreihenfolge erhalten bleibt (keine messwertbasierte Top-N-Umsortierung).

---

## 4. Layout-Hinweise

- Die erweiterte Liste **kann den Visual-Rahmen nicht verlassen**: dimensioniere den Rahmen hoch genug (Kopf + Liste). Das ist im **Power BI Service** der einzig verlässliche Weg, da jedes Visual in einem Cross-Origin-iframe läuft und sich nicht über andere legen kann.
- In Desktop hebt das Visual beim Öffnen seinen Container an; im Service wird die Reihenfolge im Bericht gesteuert.
- Halte Slicer im Bereich **Auswahl** im Vordergrund (oder aktiviere *Ebenenreihenfolge beibehalten*). Transparente Bereiche sind klickdurchlässig, sodass dahinterliegende Visuals bearbeitbar bleiben.
- Die Karten der Registerkarte **Allgemein** (Hintergrund, Effekte, Abstand, Titel) gehören zum Host-Container und können vom Visual nicht voreingestellt werden — nutze ein Berichtdesign für einheitliche Werte.

---

## 5. Lokalisierung

Das Visual enthält vollständige Übersetzungen für `en-US`, `es-ES`, `it-IT`, `fr-FR` und `de-DE`.

---

## 6. Änderungsverlauf (aktuell)

- **1.0.0.21**: Filterung auf JSON-Tupel (`applyJsonFilter`) umgestellt + Filtersynchronisierung.
- **1.0.0.22**: Robustheit gegen degenerierte Datenansichten.
- **1.0.0.23**: Kopfzeile zeigt den gemeinsamen Vorfahren.
- **1.0.0.24**: Datenfenster behält die Modellreihenfolge.
- **1.0.0.25–1.0.0.27**: Steuerelementhöhe, Beschriftungsabstand, Positionen `Oben-rechts` / `Unten-rechts`.
- **1.0.0.28–1.0.0.31**: Schriftart/Fett/Kursiv der Kopfzeile, Typografie `Erweiterte Liste`, englische Standardtexte, Messwerte verschoben und standardmäßig aus.
- **1.0.0.32**: Sortierung pro Ebene (1–3) und `Kopfzeilen-Sortierung ignorieren`.
- **1.0.0.33**: Alles auswählen behält Markierungen; Resilienz bei Quellwechsel.
- **1.0.0.34**: technische Lokalisierungsprüfung.
- **1.0.0.35–1.0.0.36**: Titel auch ohne Daten sichtbar, stabile Kopfzeile über den eigenen Filter, konsistenter Abstand.
- **1.0.0.37**: Beschriftungsabstand Standard 2px.
- **1.0.0.38–1.0.0.41**: Einzel-/Mehrfachmodus, gefüllte Quadrat-Anzeige, Kopfzeilenumschalter, Karte `Mehrfachauswahl` (Standard: an).
- **1.0.0.42**: bestmögliche Anhebung des Host-Containers bei geöffneter Liste; Plattformgrenze im Service dokumentiert.
