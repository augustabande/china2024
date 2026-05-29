# Cina 2024 — Atlante editoriale

> Un micrositio navigabile per documentare quindici giorni in Cina nell'estate del 2024.
> La mappa è la chiave d'accesso, gli approfondimenti sono il contenuto, l'esperienza è quella di esplorare un atlas curato con la lentezza di chi sa che il viaggio è già stato fatto.

```
中 · 国 · 二零二四
Shanghai — 上海   ·   Yunnan — 云南   ·   Pechino — 北京
```

---

## Indice

- [Concept](#concept)
- [Struttura del sito](#struttura-del-sito)
- [Sistema visivo](#sistema-visivo)
- [Tappe del viaggio](#tappe-del-viaggio)
- [Sezioni di approfondimento](#sezioni-di-approfondimento)
- [Interazioni e navigazione](#interazioni-e-navigazione)
- [Architettura tecnica](#architettura-tecnica)
- [Struttura dei file](#struttura-dei-file)
- [Come aprirlo / pubblicarlo](#come-aprirlo--pubblicarlo)
- [Personalizzazione](#personalizzazione)
- [Accessibilità](#accessibilità)
- [Crediti & licenze](#crediti--licenze)

---

## Concept

Il sito **non** è un blog di viaggio cronologico né un'anteprima da scrollare. È un **archivio editoriale** organizzato come un atlante: una mappa stilizzata della Cina è il dispositivo di navigazione principale; ogni punto sulla mappa apre un capitolo di approfondimento.

Le scelte editoriali derivano da tre intenzioni:

1. **Spaziale prima che lineare.** L'ordine cronologico esiste (le tappe sono numerate), ma la lettura non parte dal giorno 1: parte da dove si vuole entrare.
2. **Lettura lunga, post-viaggio.** Tipografia tarata per pagine editoriali, non per dashboard. Drop-cap, pull quotes, figure tabulari.
3. **Sottrazione.** Niente cliché visivi cinesi (draghi, lanterne, motivi cloud), niente emoji, niente iconografia Material. Whitespace generoso.

---

## Struttura del sito

```
┌────────────────────────────────────────────────────┐
│  HEADER · brand + top nav                          │
├────────────────────────────────────────────────────┤
│                                                    │
│   HERO   ·   Cina, duemilaventiquattro             │
│                                                    │
│   Citazione · 4 facts · "Apri la mappa"            │
│                                                    │
├──────────────────────────┬─────────────────────────┤
│                          │                         │
│   MAPPA (sticky)         │   PANNELLO CONTENUTO    │
│                          │                         │
│   SVG silhouette Cina    │   Indice degli          │
│   8 tappe numerate       │   approfondimenti       │
│   Rotta tratteggiata     │   ↓                     │
│   Compass + grid latlon  │   Articolo aperto       │
│                          │   (long-form)           │
│                          │                         │
├──────────────────────────┴─────────────────────────┤
│  FOOTER · periodo, tappe, 再见                     │
└────────────────────────────────────────────────────┘
```

Su mobile la mappa si sposta sopra (compatta) e il contenuto sotto.

---

## Sistema visivo

### Palette

| Token            | Hex       | Uso                                         |
|------------------|-----------|---------------------------------------------|
| `--paper`        | `#F4EFE5` | Sfondo principale (rice paper caldo)        |
| `--paper-warm`   | `#ECE5D6` | Superfici secondarie, pull quotes           |
| `--paper-deep`   | `#E3DBC8` | Wash interno della mappa                    |
| `--ink`          | `#1A1814` | Testo principale, contorni mappa            |
| `--ink-soft`     | `#3A352D` | Testo corrente lungo                        |
| `--ink-mute`     | `#6B6557` | Eyebrows, meta, didascalie                  |
| `--ink-faint`    | `#948D7E` | Numerazioni secondarie, gridlines           |
| `--rule`         | `#C9C0AC` | Divisori                                    |
| `--vermilion`    | `#A23B2A` | **Accent strutturale.** Caratteri cinesi, drop-cap, hover, stop attivo |
| `--celadon`      | `#8FA38C` | Riserva per natura / giardini               |
| `--brass`        | `#B8956A` | Numerazioni ordinate, dettagli rari         |

Il rosso vermiglio è desaturato di proposito (non vivido / brillante) ed è usato come **richiamo**, mai come superficie. Celadon e ottone sono in riserva: presenti nel sistema, attivabili se servono.

### Tipografia

| Famiglia          | Ruolo                                              |
|-------------------|----------------------------------------------------|
| **Spectral**      | Display, titoli, body editoriale, pull quotes      |
| **Inter**         | UI, header, top nav, meta                          |
| **Noto Serif SC** | Caratteri cinesi (sempre accanto al pinyin)        |
| **JetBrains Mono**| Numeri, eyebrow, didascalie tecniche, figure tab.  |

Tutti i font sono caricati da Google Fonts via `preconnect`.

### Decisioni di composizione

- **Numeri con figure tabolari** (`font-feature-settings: "tnum" 1, "lnum" 1`)
- **Citazioni** come pull quotes con bordo superiore/inferiore
- **Drop-cap vermiglio** sull'incipit di ogni articolo
- **Grain noise** SVG sottile sovrapposto all'intero documento (carta, non texture)
- **Pieno respiro orizzontale** (max-width ~46–48ch sui paragrafi)
- **`text-wrap: pretty`** dove supportato per evitare orfane

---

## Tappe del viaggio

8 tappe sulla mappa, 5 basi notturne. Coordinate approssimative usate per il posizionamento SVG.

| # | Tappa             | 中文       | Notti | Note                                    |
|---|-------------------|------------|------:|-----------------------------------------|
| 01 | Shanghai         | 上海       | 3 | Base: The Langham, Xintiandi             |
|    | Zhouzhuang       | 周庄       | — | Escursione · città sull'acqua            |
|    | French Concession| 法租界     | — | Approfondimento di quartiere             |
| 02 | Lijiang / Shuhe  | 丽江 · 束河 | 3 | Base: The Bivou                          |
|    | Shaxi            | 沙溪       | — | Escursione · Via del Tè e dei Cavalli    |
| 03 | Shangri-La       | 香格里拉   | 3 | Songzanlin · Napahai · 3.200 m           |
| 04 | Dali             | 大理       | 1 | Tre Pagode · Lago Erhai                  |
| 05 | Pechino          | 北京       | 3 | Hutong · Lama Temple · Tiananmen         |
|    | Huanghuacheng    | 黄花城     | — | Grande Muraglia, tratto sconosciuto      |

Periodo: **15 — 30 Luglio 2024** · 13 notti · 4 voli e treni.

---

## Sezioni di approfondimento

Una sezione per ciascuno dei sette markdown originali. Ogni sezione è autonoma e linkabile via hash URL.

| Hash                  | Titolo                                | Fonte                                                   |
|-----------------------|---------------------------------------|---------------------------------------------------------|
| `#overview`           | Come si organizza un viaggio in Cina  | `guida_viaggio_cina_fai_da_te.md`                       |
| `#itinerario`         | Shanghai · Yunnan · Pechino           | `itinerario_cina_shanghai_yunnan_pechino.md`            |
| `#shanghai`           | Shanghai, tre giorni                  | `shanghai_3_giorni_itinerario.md`                       |
| `#frenchconcession`   | French Concession, a piedi            | `french_concession_shanghai_walking_tour.md`            |
| `#zhouzhuang`         | Zhouzhuang, città sull'acqua          | `zhouzhuang_cosa_vedere_citta_acqua_cina.md`            |
| `#yunnan`             | Yunnan, città storiche e minoranze    | `yunnan_cosa_vedere_citta_storiche_minoranze_etniche.md`|
| `#huanghuacheng`      | La Muraglia, tratto sconosciuto       | `grande_muraglia_huanghuacheng.md`                      |

Gli hash sono **condivisibili e bookmarkabili**: aprire la pagina con `#shanghai` apre direttamente il pannello.

---

## Interazioni e navigazione

- **Mappa cliccabile** — ogni punto è una tappa; click apre il pannello corrispondente
- **Hover** — il punto si colora di vermiglio, l'etichetta si attiva
- **Stato attivo** — quando un approfondimento è aperto, il punto sulla mappa è in vermiglio con anello concentrico; le tappe correlate si accendono insieme (es. Yunnan illumina Lijiang + Shaxi + Shangri-La + Dali)
- **Indice testuale** — la lista degli approfondimenti sul lato destro come navigazione semantica alternativa alla mappa
- **Prev / Next** in fondo a ogni articolo, per scorrere senza tornare all'indice
- **Top nav** — Atlante / Contesto / Itinerario / Colophon
- **Keyboard**
  - `Tab` percorre tutte le tappe della mappa e le voci dell'indice
  - `Enter` / `Spazio` apre la tappa attiva
  - `Esc` chiude il pannello corrente
- **URL hash** — ogni approfondimento ha il proprio anchor (`#shanghai`, `#yunnan`, …); l'apertura dalla URL funziona al caricamento

Animazioni sobrie (200–300ms) limitate a hover, focus, line-extend del prompt "Apri la mappa". Nessuno scrollytelling, nessuna animazione sovrapposta.

---

## Architettura tecnica

- **Single-file HTML**: `Cina 2024.html` contiene markup, CSS e JS inline
- **Zero framework, zero build step.** Vanilla JS, ~120 righe
- **SVG inline** per la mappa (~12 KB, nessuna immagine raster)
- **Google Fonts** con `preconnect`
- **Responsive** mobile-first; breakpoint principale a 900px
- **Performance** — caricamento immediato, niente librerie esterne oltre ai font

### Markup principale

```
<header>            site-header
<section.hero>      hero con titolo, citazione, facts
<section.atlas>
  <aside.atlas-map>     mappa SVG sticky
  <main.atlas-content>  indice + 7 <article> hidden
<footer>            site-foot
```

### Stato

Tutto in `data-` attributes:

- `data-stop="shanghai"` sulle tappe della mappa
- `data-open="yunnan"` sui link dell'indice e su prev/next
- `data-jump="atlas"` sulla top-nav
- `data-screen-label="..."` su slide/screen principali (compatibilità con tool di anteprima)

Una sola mappa JavaScript `STOP_TO_ARTICLE` decide quale articolo aprire per ogni tappa — così Shuhe / Shaxi / Shangri-La / Dali condividono il pannello Yunnan; Pechino e Huanghuacheng condividono quello della Muraglia.

---

## Struttura dei file

```
.
├── Cina 2024.html               ← l'atlante (file principale)
├── README.md                    ← questo documento
└── uploads/                     ← markdown sorgente del viaggio
    ├── guida_viaggio_cina_fai_da_te.md
    ├── itinerario_cina_shanghai_yunnan_pechino.md
    ├── shanghai_3_giorni_itinerario.md
    ├── french_concession_shanghai_walking_tour.md
    ├── zhouzhuang_cosa_vedere_citta_acqua_cina.md
    ├── yunnan_cosa_vedere_citta_storiche_minoranze_etniche.md
    └── grande_muraglia_huanghuacheng.md
```

I markdown in `uploads/` sono i **sorgenti editoriali** da cui sono stati distillati i contenuti pubblicati nell'HTML. Non vengono caricati a runtime: il contenuto è inline nel file HTML.

---

## Come aprirlo / pubblicarlo

### Locale

Doppio click su `Cina 2024.html`. Non serve server, non serve build.

### GitHub Pages

1. Push del repo su GitHub
2. Settings → Pages → Source: `main` / root
3. URL sarà `https://<utente>.github.io/<repo>/Cina%202024.html`

Per usare l'atlante come homepage del repo, rinominare il file in `index.html`:

```bash
mv "Cina 2024.html" index.html
```

### Netlify / Vercel / Cloudflare Pages

Drag-and-drop della cartella. Build command: nessuno. Output dir: `/`.

---

## Personalizzazione

### Cambiare i colori

Modificare i token `:root` nel blocco `<style>`. L'intera palette è centralizzata.

```css
:root{
  --paper:     #F4EFE5;   /* sfondo principale */
  --ink:       #1A1814;   /* testo */
  --vermilion: #A23B2A;   /* accent — rosso desaturato */
  /* ... */
}
```

### Aggiungere una tappa

1. **Mappa** — aggiungere un nuovo `<g class="stop-group" data-stop="<id>">` con `circle` e `text` etichetta nella sezione SVG
2. **Articolo** — duplicare un `<article id="art-<id>">` e riempirlo
3. **Mapping** — aggiungere la voce in `STOP_TO_ARTICLE` nello script
4. **Indice** — aggiungere una `<li>` con `data-open="<id>"`
5. **Prev/Next** — aggiornare i link in coda agli articoli adiacenti

### Cambiare i font

Sostituire l'import Google Fonts in `<head>` e aggiornare le variabili `--serif`, `--sans`, `--han`, `--mono`.

### Aggiungere foto

Le immagini al momento sono **assenti per scelta editoriale**. Per inserirne:

- una sezione `figure` editoriale tra i paragrafi degli articoli, con didascalia in `JetBrains Mono`
- preferibilmente immagini in toni naturali / tendenti al monocromo, larghezza max ~720px, lazy-loaded

---

## Accessibilità

- Contrasti **AA** su body text e UI
- Ogni tappa SVG è `tabindex="0"` con `role="button"` e `aria-label` descrittivo
- Navigazione completa da tastiera (Tab / Enter / Esc)
- Caratteri cinesi sempre **accompagnati da pinyin / traslitterazione**
- Heading in gerarchia corretta (h1 hero, h2 articolo, h3 sezione, h4 sottosezione)
- Nessuna animazione critica al di sotto di 200ms; nessun flash

Limite noto: la mappa SVG è una rappresentazione visiva. Per utenti che usano screen reader la lista testuale dell'indice (`.section-index`) replica le stesse destinazioni in forma semantica.

---

## Crediti & licenze

### Contenuti

I testi degli approfondimenti sono **riformulazioni in italiano** delle informazioni contenute negli articoli originali pubblicati su **pureJoy / byChloe**:

- https://www.bychloe.it/guida-completa-per-organizzare-un-viaggio-in-cina-fai-da-te-tutto-quello-che-devi-sapere/
- https://www.bychloe.it/viaggio-in-cina-itinerario-tra-modernita-e-tradizione-dal-shanghai-allo-yunnan-fino-a-pechino/
- https://www.bychloe.it/3-giorni-a-shanghai-itinerario/
- https://www.bychloe.it/french-concession-cosa-vedere-con-un-walking-tour-mappa/
- https://www.bychloe.it/zhouzhuang-cosa-vedere-in-una-delle-piu-belle-citta-sullacqua-della-cina/
- https://www.bychloe.it/cosa-vedere-in-yunnan-un-viaggio-tra-citta-storiche-e-minoranze-etniche/
- https://www.bychloe.it/come-visitare-la-grande-muraglia-cinese-di-huanghuacheng/

Il copyright dei testi originali appartiene ai rispettivi autori. Questo atlante è un'opera derivata personale per archivio di viaggio.

### Font

- [Spectral](https://fonts.google.com/specimen/Spectral) — Production Type · OFL
- [Inter](https://fonts.google.com/specimen/Inter) — Rasmus Andersson · OFL
- [Noto Serif SC](https://fonts.google.com/noto/specimen/Noto+Serif+SC) — Google · OFL
- [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) — JetBrains · OFL

### Codice

© 2026 Augusta Bande. Tutti i diritti riservati.

---

## Stato

| Voce                  | Stato      |
|-----------------------|------------|
| Hero + atlante        | ✓ completo |
| 7 approfondimenti     | ✓ completo |
| Mappa SVG             | ✓ completo |
| Responsive mobile     | ✓ completo |
| Stato URL / hash      | ✓ completo |
| Keyboard navigation   | ✓ completo |
| Immagini foto reali   | ✗ assenti (scelta editoriale) |
| Multilingua (EN/ZH)   | ✗ non previsto |

---

```
Cina, duemilaventiquattro · 再见
```
