# Claude Code Prompt — Jongens van De Wit Landing Page

## Context
Bouw een premium craft beer landing page voor **Jongens van De Wit — Bossche Stadsbrouwerij** gebaseerd op de layout-structuur van singlefin.nc, met de visuele split-screen hero van de bijgevoegde beer_landing_page.webp referentie, maar volledig gebrand in de Jongens van De Wit stijl.

Gebruik de **DESIGN.md** file als leading design system. Lees deze volledig vóór je begint met schrijven.

---

## Referentie-materiaal (bijgevoegde bestanden)
- `beer_landing_page.webp` — Referentie voor layout en compositie (split-screen hero, typografisch contrast, product centraal)
- `bierglas.jpg` — Jongens van De Wit bierglas (gebruik als hero product image, zoals de Corona fles in de referentie)
- `logo.png` — Officieel logo, linksboven in de navigatie
- `Quiz-of-Workshop-bij-Jongens-van-de-Wit...jpg` — Brouwerij interieur foto (gebruik in een sfeer/about sectie)
- `DESIGN.md` — Volledig design system. Dit is leidend voor alle kleur-, typografie- en componentkeuzes.

---

## Layout-structuur (gebaseerd op singlefin.nc + referentie)

### 1. Navigatie (Floating Dock)
- Logo (`logo.png`) **linksboven**
- Floating glassmorphism nav bar: `backdrop-filter: blur(12px)` + `surface` kleur op 70% opacity
- Nav items rechts: **Bieren**, **Brouwerij**, **Events**, **Webshop**
- Geen hard border — "No-Line Rule" uit DESIGN.md

### 2. Hero — Split-screen (precieze nabootsing van referentie)
- **Links (60% breedte):** Grote, full-bleed atmosfeer-foto van bier/brouwerij. Gebruik `bierglas.jpg`. Laat het beeld aan de linkerkant "uitlopen" zonder harde border.
- **Rechts (40% breedte):** Donkere achtergrond (`#1b1c1c` of primaire donkere kleur), met:
  - Klein overkoepelend label in ochre (`#F9B600`): `BOSSCHE STADSBROUWERIJ`
  - Grote Display headline in wit: **"DIT IS VAKMANSCHAP"** (zelfde dramatisch typografisch contrast als "THIS IS LIVING" in referentie)
  - Korte bodytekst in lichtgrijs: beschrijving van het ambachtelijke karakter van de brouwerij
  - Gradient CTA button (primary → primary-container): "Ontdek de bieren"
  - Social icons onderaan rechts: Instagram, Facebook
- **Product overlay:** `bierglas.jpg` staat gecentreerd, overlappend over de split (net als de Corona fles die over de split heen valt). Gebruik `position: absolute`, hoge `z-index`.
- Verticale "SCROLL DOWN" tekst links, geroteerd 90°, in subtiele kleur

### 3. Featured Bieren — Horizontaal scrollbare cards
Geïnspireerd op de product-sectie van singlefin.nc:
- Sectietitel: `headline-lg` links uitgelijnd
- 3–4 bierkaarten naast elkaar (horizontaal scroll op mobile)
- Kaart-stijl: `surface-container-lowest` (#ffffff) op `surface` achtergrond — de layering principe uit DESIGN.md
- Geen dividers, gebruik verticale whitespace
- Kaart hover: subtiele `primary-fixed-dim` tint + ambient shadow (`0px 20px 40px rgba(80, 69, 50, 0.08)`)
- Placeholder biernamen: Bossche Blond, Stadsbrouner Donker, Bossche Bronsette, Witbier De Wit

### 4. Brouwerij Sfeer — Asymmetrische editorial sectie
Geïnspireerd op de "about" aanpak van singlefin.nc:
- Links: grote brouwerij foto (`Quiz-of-Workshop...jpg`), laat het beeld "uitlopen" rechts
- Rechts: tekstblok met `display-md` kop + `body-lg` paragraaf over het verhaal van de brouwerij
- Asymmetrisch: foto neemt 55% in, tekst 45%, met overlap via negatieve margin
- Accent-kleur ochre (`#F9B600`) voor een decoratief element (horizontale balk of label)

### 5. Events / Workshops CTA
- Brede sectie met lichte `surface-container` achtergrond
- 2-koloms grid: "Brouwerijrondleidingen" + "Proeverijen & Workshops"
- Per item: icon (SVG), titel, korte beschrijving, tertiary link ("Meer info →")
- Geen lijnen. Kleurshift als separator.

### 6. Footer
- Donkere achtergrond: `on-surface` (#1b1c1c)
- Logo linksboven
- 3-koloms: Navigatie | Contact | Socials
- Tagline: *"Gebrouwen in 's-Hertogenbosch"*

---

## Design tokens (uit DESIGN.md)

```css
:root {
  --primary: #7b5800;
  --primary-container: #f9b600;
  --ochre: #F9B600;
  --earth: #5C4A34;
  --surface: #fbf9f8;
  --surface-container-lowest: #ffffff;
  --surface-container: #efeded;
  --on-surface: #1b1c1c;
  --font: 'Plus Jakarta Sans', sans-serif;
}
```

**Importeer Plus Jakarta Sans via Google Fonts:**
```html
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

---

## Kritische design-regels (uit DESIGN.md — verplicht te volgen)

1. **No-Line Rule:** Geen `1px solid borders`. Secties worden gescheiden door achtergrondkleurwisselingen.
2. **Geen pure zwart:** Gebruik `#1b1c1c` voor donkere tekst.
3. **Geen dividers in kaartlijsten:** Gebruik 32–48px whitespace.
4. **Glassmorphism navigatie:** `backdrop-filter: blur(12px)` + 70% opacity surface.
5. **Gradient CTA:** `linear-gradient(to right, #7b5800, #f9b600)` voor primaire buttons.
6. **Ambient shadows:** `0px 20px 40px rgba(80, 69, 50, 0.08)` — nooit harde schaduwen.
7. **Ghost border fallback:** Als een border écht nodig is: `outline-variant` op 15% opacity.
8. **Roundedness:** Default `0.5rem`, grote kaarten `xl`.
9. **Intentional Asymmetry:** Niet alles centreren. Stagger layouts, laat beelden uitlopen.
10. **Typography contrast:** Dramatisch verschil tussen `display-lg` en `body-lg` — editorial gevoel.

---

## Technische vereisten
- Eén enkel `index.html` bestand (geen externe CSS/JS bestanden)
- Werkt op Cloudflare Pages (geen server-side code)
- Responsive: mobile-first, maar desktop is primaire focus
- Alle afbeeldingen via relatieve paden: `./bierglas.jpg`, `./logo.png`, etc.
- Smooth scroll-animaties met CSS `@keyframes` + `animation-delay` staggering
- Scroll-triggered fade-in voor secties (IntersectionObserver)
- Hero product-glas: subtiele float-animatie (`translateY` -10px ↔ 0, 3s ease-in-out infinite)

---

## Wat dit NIET moet zijn
- Geen generieke bootstrap/template look
- Geen stockfoto-achtige sfeer
- Geen overmatig gebruik van goud/premium clichés
- Geen centered everything — omarm asymmetrie
- Geen dividers of borders als sectie-scheidingen
