# BRIEF CURSOR – Landing Page Vetrina: Valsesia Electric Green
### Stack: Astro + Tailwind CSS · Deploy: Vercel

---

## OBIETTIVO

Crea una **landing page vetrina a singola pagina** per Valsesia Electric Green, azienda specializzata in escursioni guidate e noleggio di moto elettriche in zone naturalistiche del Piemonte e della Lombardia. La pagina deve comunicare **sostenibilità, divertimento e professionalità**, differenziando chiaramente i servizi in sede dalle esperienze outdoor.

---

## SETUP PROGETTO

### Inizializzazione
```bash
npm create astro@latest sp-services -- --template minimal
cd sp-services
npx astro add tailwind
npm run dev
```

### Struttura cartelle
```
sp-services/
├── public/
│   └── images/          ← foto reali del cliente (da aggiungere)
├── src/
│   ├── components/
│   │   ├── Navbar.astro
│   │   ├── Hero.astro
│   │   ├── ChiSiamo.astro
│   │   ├── Vantaggi.astro
│   │   ├── Servizi.astro
│   │   ├── Experience.astro
│   │   ├── FlowPark.astro
│   │   ├── Galleria.astro
│   │   ├── Contatti.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── Layout.astro  ← head, font, meta SEO
│   └── pages/
│       └── index.astro   ← importa tutti i componenti in sequenza
├── tailwind.config.mjs
└── astro.config.mjs
```

### Configurazione Tailwind (`tailwind.config.mjs`)
```js
export default {
  content: ['./src/**/*.{astro,html,js,ts}'],
  theme: {
    extend: {
      colors: {
        brand: {
          green: '#18b24b',
          'green-dark': '#0e7a30',
          dark: '#2c2c2c',
        },
      },
      fontFamily: {
        poppins: ['Poppins', 'sans-serif'],
      },
    },
  },
}
```

### Layout base (`src/layouts/Layout.astro`)
```astro
---
export interface Props { title: string }
const { title } = Astro.props
---
<!DOCTYPE html>
<html lang="it">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{title}</title>
    <meta name="description" content="Valsesia Electric Green – Tour guidati e noleggio moto elettriche in Piemonte e Lombardia. Partner ufficiale Talaria Italia." />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet" />
  </head>
  <body class="font-poppins text-[#2c2c2c] bg-white antialiased">
    <slot />
  </body>
</html>
```

---

## IDENTITÀ VISIVA

- **Colori primari**: Bianco `#ffffff` e Verde `#18b24b`
- **Hover/ombreggiature**: Verde scuro `#0e7a30`
- **Testi corpo**: Grigio caldo `#2c2c2c`
- **Font**: Poppins (Google Fonts) — pesi usati: 300, 400, 500, 600, 700, 800
- **Stile**: outdoor premium — pulito, arioso, forme curve, sfumature naturali. Ispirazione: Patagonia, Decathlon Trail
- **Mood**: professionale ma caldo, accessibile, vicino alla natura

**Classi Tailwind di riferimento:**
- Testo verde brand: `text-[#18b24b]`
- Sfondo verde brand: `bg-[#18b24b]`
- Hover verde scuro: `hover:bg-[#0e7a30]`
- Testo scuro: `text-[#2c2c2c]`

---

## STRUTTURA SEZIONI (componenti Astro)

---

### 1. `Navbar.astro` — Header sticky
- Logo testuale **"Valsesia Electric Green"** in Poppins Bold, colore `#18b24b`
- Link navigazione: Chi Siamo · Servizi · Experience · Flow Park · Contatti (ancore `#chi-siamo`, `#servizi`, `#experience`, `#flow-park`, `#contatti`)
- CTA button: **"Prenota un Tour"** → ancora `#contatti`, `bg-[#18b24b] text-white rounded-full px-6 py-2 hover:bg-[#0e7a30] transition-colors`
- Sticky con `backdrop-blur` e ombra al scroll (script inline con `window.addEventListener('scroll', ...)`)
- **Mobile**: hamburger menu con toggle, menu a tendina verticale
- Tailwind: `sticky top-0 z-50 bg-white/90 backdrop-blur-sm shadow-sm`

---

### 2. `Hero.astro` — Full-screen hero
- Layout `min-h-screen` con immagine di sfondo + overlay `bg-black/50`
- Immagine placeholder: `https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1600&auto=format&fit=crop`
  → `{/* TODO: sostituire con foto reale del cliente */}`
- **Headline**: `Esplora la natura. In silenzio.` — `font-extrabold text-white text-4xl md:text-6xl lg:text-7xl`
- **Sottotitolo**: `Tour guidati, noleggio e vendita di moto elettriche nelle montagne del Piemonte e della Lombardia.` — `font-light text-white text-lg md:text-xl max-w-2xl`
- **Due CTA** affiancati:
  - `Scopri i Tour` → `#experience` — `bg-[#18b24b] text-white rounded-full px-8 py-3 hover:bg-[#0e7a30]`
  - `I Nostri Servizi` → `#servizi` — `border-2 border-white text-white rounded-full px-8 py-3 hover:bg-white hover:text-[#2c2c2c]`
- **Badge strip** in basso: `🌿 Zero emissioni · 🔇 Silenziose · ⚡ Elettriche` — `bg-white/20 backdrop-blur text-white rounded-full px-6 py-2 text-sm`

---

### 3. `ChiSiamo.astro` — Chi Siamo
**id:** `chi-siamo`
- Layout `grid grid-cols-1 md:grid-cols-2 gap-12 items-center`, stacked su mobile
- **Testo** (sinistra):
  - Titolo: `Nati dalla passione per la natura e la mobilità elettrica`
  - Corpo: Valsesia Electric Green nasce 4 anni fa dall'interesse per la mobilità elettrica e l'ecosostenibilità. Siamo specializzati in escursioni guidate in moto elettrica nelle zone naturalistiche del Piemonte e della Lombardia. Offriamo un'attività a 360°: noleggio, tour, vendita, assistenza e officina mobile.
  - **Badge partner**: `border border-[#18b24b] rounded-xl p-4 mt-6` con testo "🏅 Partner Ufficiale Talaria Italia — Garanzia di qualità e assistenza certificata"
- **Immagine** (destra): placeholder `https://images.unsplash.com/photo-1551698618-1dfe5d97d256?w=800&auto=format&fit=crop`, `rounded-2xl object-cover h-96 w-full`

---

### 4. `Vantaggi.astro` — Vantaggi mobilità elettrica
**id:** `vantaggi`
- Sfondo `bg-[#18b24b]`, testo bianco, padding `py-20`
- **Titolo**: `Perché scegliere una moto elettrica?`
- **3 card** `grid grid-cols-1 md:grid-cols-3 gap-8`:
  - Stile card: `bg-white/10 rounded-2xl p-8 text-white`
  1. 🌿 **Zero emissioni** — Rispettiamo l'ambiente: zero CO₂, zero impatto chimico
  2. 🔇 **Silenziosa** — Non spaventa la fauna selvatica: l'esperienza è più autentica
  3. ⚙️ **Manutenzione minima** — Più semplice da guidare, meno fermi tecnici, più divertimento

---

### 5. `Servizi.astro` — Servizi in sede
**id:** `servizi`
- Sfondo bianco, `py-20`
- **Titolo**: `I Nostri Servizi`
- **Sottotitolo**: `Tutto quello di cui hai bisogno, in un unico posto`
- **5 card** `grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6`:
  - Stile: `border border-gray-100 rounded-2xl p-6 shadow-sm hover:shadow-md transition-shadow`
  - 🏍️ **Noleggio** — Moto elettriche disponibili per uso personale o pratica
  - 🛒 **Vendita** — Gamma di moto elettriche selezionate, con consulenza dedicata
  - 🔧 **Assistenza e Riparazione** — Officina attrezzata, tecnici certificati
  - 🚐 **Officina Mobile** — Interventi direttamente fuori sede, dove sei tu
  - 🏷️ **Rivenditori Talaria Italia** — Partner ufficiali per assistenza e ricambi originali

---

### 6. `Experience.astro` — Attività outdoor
**id:** `experience`
- Sfondo scuro `bg-[#1a1a1a]` con immagine montagna in overlay semi-trasparente — atmosfera avventura
- Testo bianco
- **Titolo**: `Vivi l'esperienza. Non solo il percorso.`
- **Sottotitolo**: `Tour guidati nelle montagne della Valsesia, per adulti e ragazzi da 14 anni (con patente ciclomotore). Partenza da Borgosesia.`
- **4 card** `grid grid-cols-1 sm:grid-cols-2 gap-6`:
  - Stile: `bg-white/5 border border-white/10 rounded-2xl p-6`
  - 🗺️ **Tour Guidati** — Percorsi sulle montagne della Valsesia, con guida esperta
  - 👨‍👩‍👧 **Tour Famiglie e Ragazzi** — Adatti da 14 anni con patente ciclomotore
  - 🏍️ **Noleggio Libero** — Esplora in autonomia o allenati su percorsi dedicati
  - 🏆 **Gare Ufficiali** — In collaborazione con la federazione ufficiale

---

### 7. `FlowPark.astro` — Flow Ride Park
**id:** `flow-park`
- Sfondo `bg-stone-900`, testo bianco — atmosfera tecnica/sportiva
- **Titolo**: `Flow Ride Park`
- **Sottotitolo**: `Tre piste per tutti i livelli — da chi inizia a chi gareggia`
- **3 card** `grid grid-cols-1 md:grid-cols-3 gap-6` con bordo laterale colorato per livello:
  - 🟢 **Pump Track** `border-l-4 border-green-400 bg-white/5 rounded-xl p-6` — Perfetta per iniziare: ritmo e tecnica di base
  - 🟡 **Pista Cross** `border-l-4 border-yellow-400 bg-white/5 rounded-xl p-6` — Adrenalina e salti su tracciato misto
  - 🔴 **Pista Enduro** `border-l-4 border-red-500 bg-white/5 rounded-xl p-6` — Per i più esperti: terreno impegnativo e tecnico

---

### 8. `Galleria.astro` — Galleria immagini
**id:** `galleria`
- **Titolo**: `In azione`
- **Layout**: griglia CSS columns `columns-2 md:columns-3 lg:columns-4 gap-4` (masonry nativo)
- **5 immagini placeholder** (sostituire con foto reali):
  ```
  https://images.unsplash.com/photo-1551698618-1dfe5d97d256?w=600&auto=format&fit=crop
  https://images.unsplash.com/photo-1596495577886-d920f1fb7238?w=600&auto=format&fit=crop
  https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=600&auto=format&fit=crop
  https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=600&auto=format&fit=crop
  https://images.unsplash.com/photo-1544551763-46a013bb70d5?w=600&auto=format&fit=crop
  ```
- Ogni immagine: `rounded-xl overflow-hidden mb-4 hover:scale-105 transition-transform duration-300`
- `loading="lazy"` su tutte le immagini
- Commento: `{/* TODO: sostituire con foto reali del cliente */}`

---

### 9. `Contatti.astro` — Form + Mappa
**id:** `contatti`
- Sfondo `bg-gray-50`, `py-20`
- **Titolo**: `Contattaci`
- Layout `grid grid-cols-1 lg:grid-cols-2 gap-12`
- **Info contatto** sopra il form:
  - 📍 Via Vittorio Veneto 104, Borgosesia (VC)
  - 📧 info@spservicess.it
  - 📞 347 6987492
- **Form** con `method="POST"` (integrabile con Formspree o Netlify Forms):
  - `Nome e Cognome` — `input type="text"`
  - `Email` — `input type="email"`
  - `Telefono` — `input type="tel"`
  - `Messaggio` — `textarea rows="5"`
  - Checkbox: `Ho letto l'informativa sulla privacy`
  - Button: `Invia Richiesta` — `bg-[#18b24b] text-white rounded-full w-full py-3 hover:bg-[#0e7a30]`
  - Stile input: `border border-gray-200 rounded-xl px-4 py-3 w-full focus:outline-none focus:ring-2 focus:ring-[#18b24b]`
- **Mappa** iframe:
  ```html
  <iframe
    src="https://maps.google.com/maps?q=Via+Vittorio+Veneto+104,+Borgosesia&output=embed"
    class="w-full h-96 rounded-2xl border-0"
    loading="lazy"
    title="Valsesia Electric Green – Mappa sede"
  ></iframe>
  ```

---

### 10. `Footer.astro`
- Sfondo `bg-[#1a1a1a]`, testo bianco
- **Logo**: "Valsesia Electric Green" `font-bold text-[#18b24b]`
- **Link rapidi**: Chi Siamo · Servizi · Experience · Flow Park · Contatti
- **Contatti**: 📞 347 6987492 · 📧 info@spservicess.it · 📍 Borgosesia (VC)
- **Menzione**: `🏅 Partner Ufficiale Talaria Italia`
- **Copyright**: `© 2025 Valsesia Electric Green – Tutti i diritti riservati`
- **Link**: Privacy Policy · Cookie Policy (creare come `src/pages/privacy.astro` e `src/pages/cookie.astro`)

---

## `index.astro` — Pagina principale

```astro
---
import Layout from '../layouts/Layout.astro'
import Navbar from '../components/Navbar.astro'
import Hero from '../components/Hero.astro'
import ChiSiamo from '../components/ChiSiamo.astro'
import Vantaggi from '../components/Vantaggi.astro'
import Servizi from '../components/Servizi.astro'
import Experience from '../components/Experience.astro'
import FlowPark from '../components/FlowPark.astro'
import Galleria from '../components/Galleria.astro'
import Contatti from '../components/Contatti.astro'
import Footer from '../components/Footer.astro'
---

<Layout title="Valsesia Electric Green – Tour ed Escursioni in Moto Elettrica | Borgosesia">
  <Navbar />
  <main>
    <Hero />
    <ChiSiamo />
    <Vantaggi />
    <Servizi />
    <Experience />
    <FlowPark />
    <Galleria />
    <Contatti />
  </main>
  <Footer />
</Layout>
```

---

## ANIMAZIONI — Scroll reveal con Intersection Observer

Aggiungi in `Layout.astro` prima di `</body>`:

```html
<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0.1 })

  document.querySelectorAll('[data-animate]').forEach(el => observer.observe(el))
</script>

<style is:global>
  [data-animate] {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  [data-animate].animate-in {
    opacity: 1;
    transform: translateY(0);
  }
</style>
```

Aggiungi `data-animate` ai wrapper delle sezioni o alle card che vuoi far apparire in scroll.

---

## DEPLOY SU VERCEL

```bash
# Verifica build locale
npm run build
npm run preview

# Deploy con Vercel CLI
npx vercel

# Oppure: collega repo GitHub su vercel.com → deploy automatico ad ogni push su main
```

Astro è supportato nativamente da Vercel — nessuna configurazione extra.

---

## NOTE PERFORMANCE E SEO

- `loading="lazy"` su tutte le immagini
- `alt` descrittivo su ogni immagine
- Meta description e `<title>` ottimizzati in `Layout.astro`
- `rel="preconnect"` su Google Fonts per ridurre il caricamento font
- Astro genera zero JS superfluo di default → Lighthouse score elevato

---

## TONE OF VOICE

- Professionale ma caldo, non istituzionale
- "Tu" diretto con l'utente
- Frasi brevi, concise, con energia
- Evita tecnicismi — il pubblico include famiglie e appassionati non esperti
- Keyword: natura, silenzio, elettrico, avventura, Valsesia, Piemonte, Lombardia, Talaria

---

*Brief preparato per uso in Cursor AI – Valsesia Electric Green / Meraviglialab*
