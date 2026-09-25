# comboSlicer

Filtro desplegabile gerarchico per Power BI. Versione **1.0.0.34**.

## 1. Mini manuale d'uso

### Installazione
1. Prendi il pacchetto `.pbiviz` dalla cartella `comboSilcer` in https://github.com/ramiro-fer-vip/comboSlicer/.
2. In Power BI Desktop: `...` (altri oggetti visivi) > **Importa un oggetto visivo da un file** e seleziona il pacchetto.
3. L'oggetto visivo `comboSlicer` appare nel riquadro delle visualizzazioni.

### Assegnazione dati
Trascina i campi nei ruoli del visivo:
- **Hierarchy Fields** (1–15 colonne): i livelli della gerarchia, es. Paese > Provincia > Città, oppure Anno > Mese.
- **Filter Measure** (facoltativa, 0–1): nasconde i membri con valore zero/vuoto e mostra il valore accanto a ogni voce, es. `(9.267,38)`.
- **Tooltips** (facoltativi, 0–10): misure aggiuntive al passaggio del mouse.

### Interazione
- Fai clic sull'intestazione per espandere/comprimere. Fai clic su una riga per selezionarla; selezionando un padre si selezionano tutti i figli.
- Stati dell'intestazione: `(Tutti)` = nessun filtro, singolo valore, `Multiplo (n)`, oppure il nome dell'antenato comune quando tutto il selezionato condivide un padre (es. `Colombia (3)`).
- Usa la lente per cercare, l'icona della casella per Seleziona tutto e `✕` per cancellare.
- `Invio` conferma la ricerca, `Esc` la cancella.
- Clic destro su una riga per il menu nativo (drill through).
- Le selezioni filtrano gli altri oggetti visivi del report e vengono salvate nel `.pbix` (inclusi segnalibri e filtri sincronizzati).

### Formattazione (scheda Visual)
- **Dropdown**: testo segnaposto; posizione (`Top`, `Bottom`, `Top-right`, `Bottom-right` — le varianti `-right` ancorano il controllo al bordo destro); casella di ricerca; Seleziona tutto; dimensione carattere; larghezza fissa dell'intestazione; chiudi all'uscita del mouse; chiudi alla selezione; altezza controllo (predefinita `36`); spaziatura etichetta (predefinita `4`).
- **Slicer header**: titolo facoltativo sopra il controllo (predefinito: nome del campo), con carattere, grassetto e corsivo.
- **Dropdown expanded**: espandi tutto per impostazione predefinita; larghezza/altezza espanse (`0` = automatico); tipografia dell'elenco — dimensione (predefinita `12`), carattere (`Segoe UI`), grassetto, corsivo; mostra valori misura (predefinito spento).
- **Data Filtering**: nascondi zeri/vuoti, testo per stato vuoto.
- **Hierarchy & Prefixes**: prefissi per livello (separati da virgole) da rimuovere dal testo (es. `Univ., Università`), ignorando maiuscole/minuscole.
- **Sorting**: ordine per livelli 1–3 (`A-Z` predefinito; anche `Z-A` e `Ordine del modello`, che rispetta l'OrderBy); `Sort order` ora si chiama `Other levels order` e vale per i livelli più profondi. L'ordinamento dall'intestazione (`...`) ha priorità salvo `Ignora ordinamento intestazione`.
- **Colors & Style**: sfondi intestazione/elenco, colori testo, accento caselle, bordo di selezione.

### Suggerimenti di layout
- L'elenco espanso non può uscire dal riquadro del visivo: dimensiona il riquadro in altezza (intestazione + elenco).
- Tieni i filtri in primo piano nel riquadro **Selezione**; l'area vuota lascia passare i clic e gli oggetti dietro restano modificabili.
- Le schede della scheda **Generale** (sfondo, effetti, spaziatura, titolo) appartengono al contenitore host e il visivo non può predefinirle — usa un tema del report per valori uniformi.

## 2. Caratteristiche principali
- Filtro gerarchico multilivello con UX a discesa.
- Filtraggio con filtro JSON tuple (stesso canale di HierarchySlicer): cross-filtering affidabile, persistenza e nessun errore di selezione dell'host.
- Rimozione prefissi per livello, localizzazione in 5 lingue (`en-US`, `es-ES`, `it-IT`, `fr-FR`, `de-DE`).
- Nascondimento dei membri senza dati guidato dalla misura, con valori in linea e tooltip.

## 3. Modifiche recenti
- **1.0.0.21**: filtraggio migrato a JSON tuple (`applyJsonFilter`) + sincronizzazione filtri; selezione ripristinata dai filtri del report.
- **1.0.0.22**: robustezza contro viste dati degeneri (cambio di visivo).
- **1.0.0.23**: l'intestazione mostra l'antenato comune (`Colombia (3)`).
- **1.0.0.24**: finestra dati in ordine del modello (nessun ordinamento per misura).
- **1.0.0.25**: altezza controllo (predefinita 36) e spaziatura superiore (predefinita 0); ordinamento predefinito di nuovo A-Z.
- **1.0.0.26**: posizioni `Top-right` / `Bottom-right` (controllo ancorato a destra).
- **1.0.0.27**: spaziatura superiore sostituita da spaziatura etichetta (predefinita 4).
- **1.0.0.28**: carattere, grassetto e corsivo nell'intestazione.
- **1.0.0.29**: scheda tipografica `Dropdown expanded`; esempi prefissi in inglese; separatore `;` per i prefissi.
- **1.0.0.30**: larghezza/altezza/espandi-tutto spostati in `Dropdown expanded`; valori tipografici concreti (12, Segoe UI).
- **1.0.0.31**: testi predefiniti in inglese; carattere intestazione Segoe UI; Mostra valori spostato in `Dropdown expanded`, spento per impostazione predefinita.
- **1.0.0.32**: ordinamento per livello (1–3) + `Ignora ordinamento intestazione`.
- **1.0.0.33**: selezionare tutto conserva le selezioni (filtro completo esplicito); resilienza al cambio di origine (reset sessione, pulizia filtri obsoleti, misura disallineata ignorata).
- **1.0.0.34**: revisione tecnica della localizzazione (terminologia di piattaforma per lingua).
