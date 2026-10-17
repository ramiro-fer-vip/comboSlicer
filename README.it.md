# comboSlicer

Filtro desplegabile gerarchico per Power BI. Versione **1.0.0.45**.

Segmentatore a elenco a discesa che costruisce una gerarchia multilivello da più campi, filtra il report tramite il modello di filtri standard di Power BI e supporta rimozione dei prefissi, ordinamento, filtro guidato da misura e selezione singola/multipla.

---

## 1. Mini manuale d'uso

### Installazione
1. Ottieni il pacchetto `.pbiviz` dalla cartella `comboSilcer` in https://github.com/ramiro-fer-vip/comboSlicer/.
2. In Power BI Desktop: `...` (altri oggetti visivi) > **Importa un oggetto visivo da un file** e seleziona il pacchetto.
3. L'oggetto visivo `comboSlicer` appare nel riquadro delle visualizzazioni. Aggiungilo ai preferiti per riutilizzarlo.

### Assegnazione dati
| Ruolo | Tipo | Intervallo | Uso |
| --- | --- | --- | --- |
| **Hierarchy Fields** | Raggruppamento | 1–15 | Livelli della gerarchia, es. Paese > Provincia > Città, oppure Anno > Mese |
| **Filter Measure** | Misura | 0–1 | Nasconde i membri con valore zero/vuoto e mostra il valore accanto a ogni voce, es. `(9.267,38)` |
| **Tooltips** | Misura | 0–10 | Misure aggiuntive al passaggio del mouse |

L'ordine dei campi definisce la gerarchia: il **primo campo è il livello radice** e l'ultimo è il livello foglia.

### Interazione
- Fai clic sull'intestazione per espandere o comprimere.
- Fai clic su una riga per selezionarla o deselezionarla. Selezionando un padre si selezionano tutti i figli; le selezioni parziali mostrano lo stato indeterminato.
- Stati dell'intestazione: `(Tutti)` (nessun filtro), un singolo valore, `Multiplo (n)`, oppure il nome dell'**antenato comune** quando tutto il selezionato condivide un padre (es. `Colombia (3)`).
- Icone della barra: ricerca (filtra l'elenco), Seleziona tutto (casella), cancella (`✕`), freccia (espandi/comprimi) e, se abilitato dall'autore, l'interruttore singolo/multiplo.
- `Invio` nella ricerca conferma, `Esc` la cancella.
- Clic destro su una riga apre il menu nativo di Power BI (drill-through).
- Le selezioni filtrano gli altri oggetti visivi e vengono salvate nel `.pbix`, inclusi segnalibri e filtri sincronizzati.

---

## 2. Riferimento completo delle proprietà (riquadro Formato > Visual)

### Menu a discesa
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Testo predefinito | *(vuoto)* | Testo dell'intestazione quando non c'è selezione. Vuoto = `(Tutti)` localizzato. |
| Posizione del controllo | `Superiore` | `Superiore` / `Inferiore` / `Superiore-destra` / `Inferiore-destra`. `Superiore*` espande verso il basso, `Inferiore*` verso l'alto; le varianti `-destra` ancorano controllo ed elenco al bordo destro. |
| Mostra casella di ricerca | `Sì` | Mostra l'icona di ricerca nell'intestazione. |
| Mostra Seleziona tutto | `Sì` | Mostra l'icona Seleziona tutto (nascosta automaticamente in modalità singola). |
| Dimensione carattere | `12` | Dimensione del testo dell'intestazione. |
| Larghezza controllo (px) | `0` | Larghezza fissa dell'intestazione. `0` = occupa la larghezza dell'oggetto visivo. |
| Chiudi all'uscita del mouse | `Sì` | Chiude l'elenco quando il puntatore esce dal controllo. |
| Chiudi alla selezione | `No` | Chiude l'elenco dopo ogni selezione. |
| Altezza controllo (px) | `36` | Altezza della casella del controllo. |
| Spaziatura etichetta (px) | `2` | Spazio tra l'etichetta e la casella del controllo. |

### Elenco espanso
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Dimensione carattere | `12` | Dimensione del testo delle voci. |
| Carattere | `Segoe UI` | Carattere delle voci. |
| Grassetto | `No` | Voci in grassetto. |
| Corsivo | `No` | Voci in corsivo. |
| Espandi tutto per impostazione predefinita | `Sì` | Espande tutti i rami all'apertura dell'elenco. |
| Larghezza controllo espanso (px) | `0` | Larghezza fissa dell'elenco. `0` = come il controllo. |
| Altezza controllo espanso (px) | `0` | Altezza fissa dell'elenco. `0` = automatica (limitata al riquadro). |
| Mostra valori misura | `No` | Mostra il valore della misura in linea accanto a ogni voce. |

### Selezione multipla
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Consenti selezione multipla | `Sì` | `Sì` = selezione multipla. `No` = un solo ramo/nodo, Seleziona tutto è nascosto e l'indicatore diventa un quadrato pieno. |
| Mostra selezione multipla | `No` | Mostra un interruttore nell'intestazione per consentire all'utente di cambiare singolo/multiplo in esecuzione (la modifica viene salvata). |
| Colore selezione singola | `#ef4444` | Riempimento e bordo del quadrato pieno usato in modalità singola. |
| Colore interruttore | `#990000` | Colore del pulsante dell'intestazione (lo distingue da Seleziona tutto). |

### Intestazione filtro
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Mostra intestazione | `Sì` | Mostra il titolo sopra il controllo. |
| Testo intestazione | *(vuoto)* | Testo del titolo. Vuoto = nome del primo campo. |
| Dimensione carattere intestazione | `12` | Dimensione del titolo. |
| Colore intestazione | *(tema)* | Colore del titolo. |
| Carattere intestazione | `Segoe UI` | Carattere del titolo. |
| Grassetto / Corsivo | `No` | Stile del titolo. |

### Filtro dati
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Nascondi valori zero | `Sì` | Rimuove i membri la cui misura di filtro è `0`. |
| Nascondi valori vuoti | `Sì` | Rimuove i membri la cui misura di filtro è vuota. |
| Testo per nessun record | *(vuoto)* | Messaggio mostrato nell'elenco quando non ci sono dati. Vuoto = `- Nessun record -` localizzato. |

### Gerarchia e prefissi
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Ignora maiuscole/minuscole | `Sì` | Confronto dei prefissi senza distinzione di maiuscole. |
| Prefissi da ignorare Livello 1…5 | *(vuoto)* | Prefissi separati da virgola o punto e virgola, rimossi dal testo mostrato a ogni livello, es. `Univ.; Università`. Il nome non resta mai vuoto. |

### Ordinamento
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Ordine livello 1 / 2 / 3 | `Alfabetico (A-Z)` | Ordine per livello: `Alfabetico (A-Z)`, `Alfabetico (Z-A)` o `Ordine modello dati` (rispetta **Ordina per colonna / OrderBy** del campo). |
| Ordine altri livelli | `Alfabetico (A-Z)` | Stesse opzioni, applicate ai livelli 4 e successivi. |
| Ignora ordinamento dell'oggetto visivo | `No` | `Sì` ignora l'ordinamento scelto nell'intestazione (`...` > Ordina asse) e riporta il controllo a questo riquadro (es. per ripristinare l'ordine del modello). |

### Colori e stile
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Sfondo intestazione | *(tema)* | Sfondo della casella del controllo. |
| Colore testo intestazione | *(tema)* | Colore del testo dell'intestazione. |
| Sfondo menu a discesa | *(tema)* | Sfondo dell'elenco espanso. |
| Colore testo elementi | *(tema)* | Colore delle voci dell'elenco. |
| Colore casella di controllo | *(accento)* | Accento delle caselle di selezione multipla. |
| Bordo con selezione | `Sì` | Disegna un bordo attorno al controllo quando c'è una selezione attiva. |
| Colore bordo con selezione | `#2563eb` | Colore del bordo. |
| Spessore bordo con selezione | `1` | Spessore del bordo in px. |

### Descrizione comando
| Proprietà | Predefinito | Descrizione |
| --- | --- | --- |
| Mostra descrizioni comando | `No` | Abilita le schede descrizione comando native (incluse le pagine descrizione comando del report). |

---

## 3. Note di comportamento

- **Modello di filtro**: le selezioni sono applicate come filtro JSON tuple tramite `applyJsonFilter` (lo stesso canale usato da HierarchySlicer). Offre cross-filtering affidabile, evita errori di selezione dei punti dati dell'host e persiste nel report.
- **Persistenza**: la selezione corrente viene ripristinata dai filtri del report a ogni aggiornamento, quindi sopravvive a salvataggio/riapertura, segnalibri e filtri sincronizzati.
- **Cambio di origine**: se i campi associati cambiano, l'oggetto visivo reimposta lo stato di sessione (universi, cache, espansioni) e pulisce i filtri obsoleti automaticamente. Una misura di filtro disallineata viene ignorata invece di nascondere righe.
- **Esempi di prefissi**: mostrati in inglese nel riquadro di formattazione (i segnaposto non sono localizzabili nel modello di formattazione attuale).
- **Riduzione dati**: usa `window`, che conserva l'ordine del modello (nessun riordino Top-N per misura).

---

## 4. Suggerimenti di layout

- L'elenco espanso **non può uscire dal riquadro dell'oggetto visivo**: dimensiona il riquadro in altezza (intestazione + elenco). È l'unica via affidabile in **Power BI Service**, dove ogni oggetto visivo gira in un iframe cross-origin e non può portarsi sopra gli altri.
- In Desktop l'oggetto visivo eleva il proprio contenitore mentre l'elenco è aperto; nel Service l'ordine si controlla dal report.
- Tieni i filtri in primo piano nel riquadro **Selezione** (o attiva *Mantieni ordine livelli*). Le aree trasparenti lasciano passare i clic, quindi ciò che è dietro resta modificabile.
- Le schede della scheda **Generale** (**Sfondo**, **Bordo dell'oggetto visivo**, **Ombra**, **Spaziatura**, **Titolo**) appartengono al contenitore host (`visualContainerObjects`), non all'oggetto visivo. `capabilities.json` non ha opzioni per esse, quindi non possono essere predefinite — vedi **sezione 5**.

---

## 5. Nascondere sfondo e bordo del contenitore

La cornice sottile visibile attorno al controllo **non** è disegnata dall'oggetto visivo: è il **contenitore host** (`visualContainerObjects`). Non esiste una proprietà dell'oggetto visivo per questo, quindi va disattivata nel report.

### Opzione A — Per oggetto visivo
1. Seleziona l'oggetto visivo.
2. **Formato oggetto visivo** (rullo) > scheda **Generale**.
3. Espandi **Effetti**:
   - **Sfondo** → disattiva (oppure lascialo attivo con **Trasparenza = 100%**).
   - **Bordo dell'oggetto visivo** → disattiva.
   - **Ombra** → disattiva (facoltativo).
4. Se l'oggetto visivo risulta compresso, imposta **Proprietà > Spaziatura** esplicitamente (vedi nota).

### Opzione B — Tutto il report
1. **Visualizza** > **Temi** > **Impostazioni predefinite degli oggetti visivi** (o **Personalizza tema corrente**).
2. Disattiva **Sfondo** e **Bordo**.
3. Tutti gli oggetti visivi non personalizzati singolarmente ereditano questi valori.

### Opzione C — Tema JSON riutilizzabile
```json
{
  "name": "Senza cornice",
  "visualStyles": {
    "*": { "*": {
      "background": [{ "show": false }],
      "border": [{ "show": false }],
      "dropShadow": [{ "show": false }]
    }}
  }
}
```
Importalo da **Visualizza** > **Temi** > **Cerca temi**.

> **Nota:** non appena un oggetto visivo dichiara qualsiasi impostazione del contenitore (sfondo, bordo, titolo…), Power BI smette di ereditare la **Spaziatura** predefinita del tema per quell'oggetto e la imposta a `0`. Imposta **Proprietà > Spaziatura** esplicitamente se ti serve spazio.

---

## 6. Localizzazione

L'oggetto visivo include traduzioni complete per `en-US`, `es-ES`, `it-IT`, `fr-FR` e `de-DE`.

---

## 7. Cronologia modifiche (recente)

- **1.0.0.21**: filtraggio migrato a JSON tuple (`applyJsonFilter`) + sincronizzazione filtri.
- **1.0.0.22**: robustezza contro viste dati degeneri.
- **1.0.0.23**: l'intestazione mostra l'antenato comune.
- **1.0.0.24**: la finestra dati conserva l'ordine del modello.
- **1.0.0.25–1.0.0.27**: altezza controllo, spaziatura etichetta, posizioni `Superiore-destra` / `Inferiore-destra`.
- **1.0.0.28–1.0.0.31**: carattere/grassetto/corsivo dell'intestazione, tipografia `Elenco espanso`, testi predefiniti in inglese, valori misura spostati e spenti per impostazione predefinita.
- **1.0.0.32**: ordinamento per livello (1–3) e `Ignora ordinamento dell'oggetto visivo`.
- **1.0.0.33**: selezionare tutto conserva le selezioni; resilienza ai cambi di origine.
- **1.0.0.34**: revisione tecnica della localizzazione.
- **1.0.0.35–1.0.0.36**: titolo visibile senza dati, intestazione stabile guidata dal filtro proprio, spaziatura coerente.
- **1.0.0.37**: spaziatura etichetta predefinita 2px.
- **1.0.0.38–1.0.0.41**: modalità selezione singola/multipla, indicatore quadrato pieno, interruttore nell'intestazione, scheda `Selezione multipla` (attiva per impostazione predefinita).
- **1.0.0.42**: elevazione del contenitore host mentre l'elenco è aperto; limite di piattaforma documentato nel Service.
- **1.0.0.43**: geometria dell'elenco ricalcolata all'apertura della ricerca (mantiene l'elenco nel riquadro) e focus senza scorrimento.
- **1.0.0.44**: il contenitore host viene ri-localizzato a ogni elevazione (sopravvive ai re-render dell'host) e l'apilamento viene riaffermato poco dopo l'apertura, così l'elenco mantiene il suo livello dopo aver usato altri controlli.
- **1.0.0.45**: i pulsanti di azione dell'intestazione (ricerca, Seleziona tutto, cancella, singolo/multiplo) non arrestano più la propagazione dell'evento, così Power BI rileva il clic e eleva l'oggetto visivo — era questo il motivo per cui la casella di ricerca restava sotto altri controlli. L'intestazione ignora internamente quei clic e l'elevazione copre ora anche l'iframe stesso e i contenitori `visual-container` / `-modern` / `-group`.
