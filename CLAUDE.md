# Valle dell'Aniene — FAI
## Istruzioni per Claude

---

## Workflow Git

- Sviluppa sempre su un branch dedicato: `git checkout -b claude/<descrizione-breve>`
- Dopo aver pushato tutte le modifiche, esegui sempre il **merge in `main`** e push
- Sequenza standard:
  ```
  git add <files>
  git commit -m "messaggio"
  git push -u origin <branch>
  git checkout main
  git pull origin main --rebase
  git merge <branch> --no-ff
  git push -u origin main
  ```

---

## Workflow PDF → Sito

Il contenuto del sito proviene **esclusivamente dal PDF** `guida-valle-aniene.pdf`.

Quando arriva un PDF nuovo o aggiornato:
1. Leggi il PDF con il tool `Read` per estrarre testo e struttura
2. Mappa ogni sezione del PDF ai **componenti esistenti** (vedi sotto)
3. Mantieni invariate classi CSS, token e pattern HTML esistenti
4. Non inventare nuovi stili: usa sempre i componenti documentati qui

---

## Design System

### Colori (CSS custom properties)
| Token | Valore | Uso |
|---|---|---|
| `--fai-orange` | `#C8471A` | CTA primari, accenti, Curiosità |
| `--fai-orange-d` | `#9E3210` | Hover arancio |
| `--fai-gold` | `#C8971A` | Suggerimento, accenti secondari |
| `--fai-gold-l` | `#E5B935` | Link footer, bento tag |
| `--fai-cream` | `#FAF7F2` | Sfondo pagina |
| `--fai-brown` | `#2A1C0E` | Sfondo footer, pdf-bar |
| `--text-primary` | `#1E1208` | Titoli |
| `--text-body` | `#3D2B14` | Testo corpo |
| `--text-muted` | `#7A6347` | Testo secondario, nav link |

### Tipografia
| Token | Range | Uso |
|---|---|---|
| `--text-xs` | 0.75–0.875rem | Label, meta, tag |
| `--text-sm` | 0.875–1rem | Corpo card, callout |
| `--text-base` | 1–1.125rem | Testo corpo principale |
| `--text-lg` | 1.125–1.5rem | Sottotitoli, nav title |
| `--text-xl` | 1.5–2.25rem | Titoli sezione |
| `--text-2xl` | 2–3.5rem | Titoli grandi |
| `--text-hero` | 3–7rem | Titolo hero |
| `--font-display` | Cormorant Garamond | Titoli, hero, quote |
| `--font-body` | Inter | Corpo, UI, label |

### Spaziatura
`--sp-1` (0.25rem) · `--sp-2` · `--sp-3` · `--sp-4` (1rem) · `--sp-6` (1.5rem) · `--sp-8` (2rem) · `--sp-10` · `--sp-12` · `--sp-16` (4rem) · `--sp-20` · `--sp-24` · `--sp-32` (8rem)

### Border radius
`--r-sm` 0.375rem · `--r-md` 0.625rem · `--r-lg` 1rem · `--r-xl` 1.5rem · `--r-full` 9999px

---

## Componenti HTML

### Hero
```html
<section class="hero" aria-label="...">
  <div class="hero-bg" style="background-image:url('img/...')"></div>
  <div class="hero-overlay"></div>
  <div class="hero-content container--wide">
    <p class="hero-label">Etichetta · Sottotitolo</p>
    <h1 class="hero-title">Titolo<br>Principale</h1>
    <p class="hero-subtitle">Sottotitolo in corsivo</p>
    <div class="hero-cta-group">
      <a href="..." class="btn btn-primary">CTA primario</a>
      <a href="..." class="btn btn-outline">CTA secondario</a>
    </div>
  </div>
</section>
```

### Callout — Curiosità
```html
<div class="callout callout--curiosita reveal">
  <div class="callout-header">
    <span class="callout-icon">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>
    </span>
    <p class="callout-label">Curiosità</p>
  </div>
  <p class="callout-text">Testo del contenuto...</p>
</div>
```

### Callout — Suggerimento
```html
<div class="callout callout--suggerimento reveal">
  <div class="callout-header">
    <span class="callout-icon">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/><circle cx="12" cy="10" r="3"/></svg>
    </span>
    <p class="callout-label">Suggerimento</p>
  </div>
  <p class="callout-text">Testo del contenuto...</p>
</div>
```

### Card 3D (con immagine)
```html
<article class="card-3d">
  <img class="card-img" src="img/..." alt="..." loading="lazy"/>
  <div class="card-body">
    <span class="card-tag">Etichetta</span>
    <h3 class="card-title">Titolo card</h3>
    <p class="card-text">Descrizione...</p>
  </div>
</article>
```
Le card vanno dentro `.cards-grid`.

### Sezione articolo
```html
<section class="section section--cream" id="anchor">
  <div class="container">
    <div class="section-header">
      <p class="section-label reveal">Label sopra</p>
      <h2 class="section-title reveal">Titolo<br>Sezione</h2>
    </div>
    <div class="article-body">
      <h2 class="reveal">Sottotitolo H2</h2>
      <p class="reveal">Testo paragrafo...</p>
      <!-- callout, card, quote-block, ecc. -->
    </div>
  </div>
</section>
```

### Quote block
```html
<div class="quote-block reveal">
  <blockquote class="quote-text">"Testo citazione..."</blockquote>
  <p class="quote-source">— AUTORE, anno</p>
</div>
```

### PDF Download bar
```html
<div class="pdf-bar reveal">
  <div class="pdf-icon"><!-- SVG documento --></div>
  <p class="pdf-bar-title">Scarica la guida completa in PDF</p>
  <p class="pdf-bar-meta">FAI Delegazione Roma · A cura di ...</p>
  <a href="guida-valle-aniene.pdf" download="Guida-Valle-Aniene-FAI.pdf" class="btn-pdf">
    <!-- SVG download -->
    Scarica PDF
  </a>
</div>
```

### Part-hero (mini-hero interno alle sezioni)
```html
<div class="part-hero reveal">
  <div class="part-hero-bg" style="background-image:url('img/...')"></div>
  <div class="part-hero-overlay"></div>
  <div class="part-hero-content">
    <p class="part-hero-num">Etichetta / Data</p>
    <h2 class="part-hero-title">Titolo</h2>
    <p class="part-hero-sub">Sottotitolo</p>
  </div>
</div>
```

### Tab navigation (pagine interne)
```html
<nav class="sticky-tabs" aria-label="Sezioni della pagina">
  <div class="tabs-inner">
    <button class="tab-btn active" data-tab="tab-id"><span class="tab-btn-num">1</span>Nome tab</button>
    <!-- altri tab -->
  </div>
</nav>
<div class="page-panel active" id="tab-id">
  <!-- contenuto pannello -->
</div>
```

---

## Classi di utilità

| Classe | Effetto |
|---|---|
| `reveal` | Animazione scroll fade-in (JS IntersectionObserver) |
| `container` | Max-width 960px, centrato |
| `container--wide` | Max-width 1200px, centrato |
| `section--cream` | Sfondo crema chiaro |
| `section--cream2` | Sfondo crema medio |
| `section--dark` | Sfondo marrone scuro |
| `.term` | Parola tecnica con tooltip (titolo hover) |

---

## Struttura file

```
valle-aniene-fai/
├── css/style.css          ← unico foglio di stile
├── js/main.js             ← scroll reveal, menu, 3D tilt, tabs, lightbox
├── img/                   ← immagini del sito
├── guida-valle-aniene.pdf ← PDF sorgente del contenuto
├── index.html             ← homepage
├── parte-prima.html       ← sezione 1
└── parte-seconda.html     ← sezione 2
```

Ogni nuova sezione del PDF diventa una nuova pagina HTML oppure un nuovo `page-panel` dentro una pagina esistente.

---

## Regole di stile

- Non aggiungere nuove dipendenze CSS/JS esterne
- Non creare nuove classi se esiste già un componente adatto
- Le immagini vanno nella cartella `img/` con `loading="lazy"`
- Ogni elemento interattivo/animato deve avere `reveal` per l'animazione scroll
- I titoli usano sempre `--font-display` (Cormorant Garamond)
- Il testo corpo usa sempre `--font-body` (Inter)
