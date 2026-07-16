# 🏗️ Architektur – Astro Starter Pro

> Zuletzt aktualisiert: Juli 2026

---

## Inhaltsverzeichnis

- [Verwendete Technologien](#verwendete-technologien)
- [Projektstruktur](#projektstruktur)
- [Konfigurationsdateien](#konfigurationsdateien)
- [Seiten & Routing](#seiten--routing)
- [Komponenten-Architektur](#komponenten-architektur)
- [Navigation / Menüs](#navigation--menüs)
- [Layouts](#layouts)
- [Content / Blog-System](#content--blog-system)
- [Bilder & Assets](#bilder--assets)
- [Styling / Theming](#styling--theming)
- [SEO](#seo)
- [TypeScript-Typen](#typescript-typen)
- [Code-Qualität & Tooling](#code-qualität--tooling)
- [Skripte](#skripte)

---

## Verwendete Technologien

| Technologie                 | Version  | Zweck                                        |
| --------------------------- | -------- | -------------------------------------------- |
| **Astro**                   | ^7.1.0   | Static Site Generator (SSG), Haupt-Framework |
| **Tailwind CSS**            | ^4.3.3   | Utility-First CSS Framework                  |
| **@tailwindcss/typography** | ^0.5.20  | Prose-Styling für Markdown/MDX-Inhalte       |
| **@tailwindcss/vite**       | ^4.3.3   | Vite-Plugin für Tailwind CSS v4              |
| **TypeScript**              | ^6.0.3   | Typisierung                                  |
| **MDX** (@astrojs/mdx)      | ^7.0.3   | Markdown mit JSX-Komponenten                 |
| **astro-icon**              | ^1.1.5   | Icon-Integration (Iconify)                   |
| **@iconify-json/lucide**    | ^1.2.117 | Lucide Icon-Set                              |
| **@iconify-json/tabler**    | ^1.2.35  | Tabler Icon-Set                              |
| **@astrojs/sitemap**        | ^3.7.3   | Automatische Sitemap-Generierung             |
| **@astrojs/rss**            | ^4.0.19  | RSS-Feed-Generierung                         |
| **@vercel/analytics**       | ^2.0.1   | Vercel Analytics Integration                 |
| **remark-reading-time**     | ^2.1.0   | Lesezeit-Berechnung für Blog-Posts           |
| **ESLint**                  | ^10.7.0  | Code-Linting                                 |
| **Prettier**                | ^3.9.5   | Code-Formatierung                            |
| **Husky**                   | ^9.1.7   | Git-Hooks (Pre-Commit)                       |
| **lint-staged**             | ^17.0.8  | Lint nur geänderte Dateien                   |
| **Vitest**                  | ^4.1.10  | Test-Framework                               |

---

## Projektstruktur

```
astro-starter-pro/
├── .github/                    # GitHub-spezifisch (Workflows, Daten)
│   ├── workflows/
│   │   └── traffic.yml         # Traffic-Tracking-Workflow
│   ├── data/
│   │   └── clones.json         # Klon-Statistiken
│   └── save_traffic.js         # Traffic-Speicher-Skript
│
├── public/                     # Statische Assets (unverarbeitet, 1:1 kopiert)
│   ├── favicon.svg             # Favicon
│   └── blog/                   # Blog-Bilder (WebP)
│       ├── welcome.webp
│       ├── markdown.webp
│       └── blog_post_*.webp    # Blog-Post-Bilder
│
├── src/
│   ├── assets/                 # Verarbeitete Assets (Astro-Bildoptimierung)
│   │   ├── og-image.png        # Standard Open Graph Bild
│   │   └── images/
│   │       ├── about-office.webp
│   │       ├── dev_balanced.png
│   │       ├── open-source.png
│   │       └── services/       # Service-spezifische Bilder
│   │           ├── consulting.webp
│   │           ├── seo.webp
│   │           └── web-dev.webp
│   │
│   ├── components/             # Wiederverwendbare Komponenten
│   │   ├── blog/               # Blog-Komponenten
│   │   │   └── PostItem.astro
│   │   ├── layout/             # Layout-Komponenten (Navbar, Footer)
│   │   │   ├── Navbar.astro
│   │   │   └── Footer.astro
│   │   ├── seo/                # SEO-Komponenten
│   │   │   ├── Seo.astro       # Meta-Tags, Open Graph, Twitter Cards
│   │   │   └── Schema.astro    # JSON-LD Structured Data
│   │   ├── ui/                 # Basis-UI-Komponenten
│   │   │   ├── Button.astro
│   │   │   ├── Card.astro
│   │   │   ├── Form.astro
│   │   │   ├── Headline.astro
│   │   │   ├── Pagination.astro
│   │   │   ├── Tags.astro
│   │   │   └── ThemeToggle.astro
│   │   └── widgets/            # Seitenabschnitt-Widgets (Sektionen)
│   │       ├── CallToAction.astro
│   │       ├── Content.astro
│   │       ├── Content2.astro
│   │       ├── Experience.astro
│   │       ├── FAQ.astro
│   │       ├── Features.astro
│   │       ├── Github.astro
│   │       ├── Hero.astro
│   │       ├── Integrations.astro
│   │       ├── Portfolio.astro
│   │       ├── Pricing.astro
│   │       ├── ServiceList.astro
│   │       ├── Skills.astro
│   │       ├── Stats.astro
│   │       ├── Testimonials.astro
│   │       ├── Values.astro
│   │       └── WidgetWrapper.astro
│   │
│   ├── config/                 # Zentrale Konfiguration
│   │   └── site.ts             # Site-Name, Links, Social Links, Navigation
│   │
│   ├── content/                # Content Collections (Astro Content Layer)
│   │   └── blog/               # Blog-Posts (Markdown)
│   │       ├── welcome.md
│   │       ├── markdown-features.md
│   │       └── *.md            # Weitere Blog-Posts
│   │
│   ├── layouts/                # Seiten-Layouts
│   │   └── BaseLayout.astro    # Haupt-Layout (HTML-Grundgerüst)
│   │
│   ├── pages/                  # Seiten (File-based Routing)
│   │   ├── index.astro         # Startseite
│   │   ├── about.astro         # Über uns
│   │   ├── services.astro      # Dienstleistungen
│   │   ├── pricing.astro       # Preise
│   │   ├── contact.astro       # Kontakt
│   │   ├── widgets.astro       # Widget-Showcase
│   │   ├── 404.astro           # Fehlerseite
│   │   ├── robots.txt.ts       # Dynamische robots.txt
│   │   ├── rss.xml.js          # RSS-Feed
│   │   ├── blog/
│   │   │   ├── [...page].astro      # Blog-Übersicht (paginiert)
│   │   │   ├── [...slug].astro      # Einzelner Blog-Post
│   │   │   ├── category/
│   │   │   │   └── [category].astro # Blog nach Kategorie
│   │   │   └── tags/
│   │   │       └── [tag].astro      # Blog nach Tag
│   │   └── templates/
│   │       ├── portfolio.astro      # Portfolio-Template
│   │       └── saas.astro           # SaaS-Landing-Template
│   │
│   ├── styles/                 # Globale Styles
│   │   └── global.css          # Tailwind-Import, CSS-Variablen, Animationen
│   │
│   ├── types/                  # TypeScript-Typdefinitionen
│   │   └── types.d.ts          # Alle Widget- und Komponenten-Interfaces
│   │
│   └── content.config.ts       # Content Collection Schema-Definition
│
├── astro.config.mjs            # Astro-Hauptkonfiguration
├── tsconfig.json               # TypeScript-Konfiguration
├── eslint.config.js            # ESLint-Konfiguration (Flat Config)
├── .prettierrc                 # Prettier-Konfiguration
├── .editorconfig               # Editor-Konfiguration
├── package.json                # Dependencies & Scripts
└── package-lock.json           # Dependency Lock-File
```

---

## Konfigurationsdateien

### `astro.config.mjs`

- **Site-URL**: `https://astrostarterpro.com/`
- **Integrations**: Sitemap, astro-icon, MDX
- **Markdown**: remark-reading-time Plugin für Lesezeit-Berechnung
- **i18n**: Unterstützung für `en` (Standard) und `es` (Spanisch), ohne Prefix für Standardsprache
- **Prefetch**: Alle Links werden im Viewport-Modus vorgeladen
- **Build**: Stylesheets werden immer inline eingefügt
- **Vite**: Tailwind CSS v4 Plugin

### `src/config/site.ts`

**Die zentrale Konfiguration des Projekts.** Hier werden definiert:

- Site-Name, Beschreibung, URL
- Sprache und Locale
- Autor und Twitter-Handle
- OG-Image (Standard)
- **Social Links** (Twitter, GitHub, Discord)
- **Navigation** (siehe [Navigation](#navigation--menüs))

### `tsconfig.json`

- Extends: `astro/tsconfigs/strict`
- **Path-Alias**: `@/*` → `src/*` (Import-Kurzform)

---

## Seiten & Routing

Astro verwendet **File-based Routing**. Jede `.astro`-Datei in `src/pages/` wird zu einer Route:

| Datei                                  | Route                    | Beschreibung                |
| -------------------------------------- | ------------------------ | --------------------------- |
| `pages/index.astro`                    | `/`                      | Startseite                  |
| `pages/about.astro`                    | `/about`                 | Über uns                    |
| `pages/services.astro`                 | `/services`              | Dienstleistungen            |
| `pages/pricing.astro`                  | `/pricing`               | Preise                      |
| `pages/contact.astro`                  | `/contact`               | Kontakt-Formular            |
| `pages/widgets.astro`                  | `/widgets`               | Widget-Showcase             |
| `pages/404.astro`                      | `/404`                   | Fehlerseite                 |
| `pages/blog/[...page].astro`           | `/blog`, `/blog/2`, ...  | Blog-Übersicht (paginiert)  |
| `pages/blog/[...slug].astro`           | `/blog/mein-post`        | Einzelner Blog-Post         |
| `pages/blog/category/[category].astro` | `/blog/category/general` | Posts einer Kategorie       |
| `pages/blog/tags/[tag].astro`          | `/blog/tags/astro`       | Posts eines Tags            |
| `pages/templates/portfolio.astro`      | `/templates/portfolio`   | Portfolio-Template-Seite    |
| `pages/templates/saas.astro`           | `/templates/saas`        | SaaS-Landing-Template-Seite |
| `pages/robots.txt.ts`                  | `/robots.txt`            | Dynamische robots.txt       |
| `pages/rss.xml.js`                     | `/rss.xml`               | RSS-Feed                    |

---

## Komponenten-Architektur

Komponenten sind in **5 Kategorien** organisiert:

### 1. `components/layout/` – Layout-Komponenten

Strukturelle Komponenten, die auf jeder Seite erscheinen:

- **`Navbar.astro`** – Haupt-Navigation (Desktop + Mobile-Menü)
- **`Footer.astro`** – Footer mit Social Links und Copyright

### 2. `components/ui/` – Basis-UI-Komponenten

Wiederverwendbare, atomare UI-Elemente:

- **`Button.astro`** – Button mit Varianten (`primary`, `secondary`, `link`)
- **`Card.astro`** – Karten-Container
- **`Form.astro`** – Kontaktformular
- **`Headline.astro`** – Überschrift mit Tagline und Subtitle
- **`Pagination.astro`** – Blog-Paginierung
- **`Tags.astro`** – Tag-Badges
- **`ThemeToggle.astro`** – Dark/Light-Mode-Umschalter

### 3. `components/widgets/` – Seiten-Sektionen

Größere, zusammengesetzte Abschnitte für Landing Pages. Jedes Widget kann über Props konfiguriert werden (siehe `src/types/types.d.ts`):

- **`Hero.astro`** – Hero-Banner mit CTA-Buttons
- **`Features.astro`** – Feature-Grid mit Icons
- **`Content.astro` / `Content2.astro`** – Text + Bild Sektionen
- **`FAQ.astro`** – FAQ-Akkordeon
- **`Pricing.astro`** – Preis-Tabelle
- **`Testimonials.astro`** – Kundenstimmen
- **`Stats.astro`** – Statistik-Zähler
- **`CallToAction.astro`** – CTA-Banner
- **`ServiceList.astro`** – Service-Auflistung
- **`Values.astro`** – Werte/Prinzipien-Grid
- **`Integrations.astro`** – Integrations-Logos
- **`Portfolio.astro`** – Projekt-Showcase
- **`Experience.astro`** – Timeline/Erfahrung
- **`Skills.astro`** – Skill-Badges
- **`Github.astro`** – GitHub-Integration
- **`WidgetWrapper.astro`** – Wrapper für konsistentes Widget-Spacing

### 4. `components/blog/` – Blog-Komponenten

- **`PostItem.astro`** – Blog-Post-Vorschau-Karte

### 5. `components/seo/` – SEO-Komponenten

- **`Seo.astro`** – Meta-Tags, Open Graph, Twitter Cards
- **`Schema.astro`** – JSON-LD Structured Data (`WebSite`, `BlogPosting`)

---

## Navigation / Menüs

### Wo die Navigation definiert wird

Die Navigation wird **zentral** in `src/config/site.ts` definiert im `navLinks`-Array:

```typescript
// src/config/site.ts
navLinks: [
  { text: "Home", href: "/" },
  { text: "About", href: "/about" },
  { text: "Services", href: "/services" },
  { text: "Pricing", href: "/pricing" },
  { text: "Blog", href: "/blog" },
  { text: "Contact", href: "/contact" },
  { text: "Widgets", href: "/widgets" },
  {
    text: "Templates",
    href: "/templates",
    links: [  // Dropdown-Untermenü
      { text: "Personal Portfolio", href: "/templates/portfolio" },
      { text: "SaaS Landing", href: "/templates/saas" },
    ],
  },
],
```

### Wie die Navigation gerendert wird

- **`Navbar.astro`** (`src/components/layout/Navbar.astro`) liest `siteConfig.navLinks` und rendert:
  - **Desktop**: Horizontale Link-Leiste mit Dropdown-Menüs (Hover-gesteuert via CSS `group-hover`)
  - **Mobile**: Hamburger-Menü mit Toggle-Button (JavaScript: `astro:page-load`-Event)
- **`Footer.astro`** (`src/components/layout/Footer.astro`) zeigt `siteConfig.socialLinks` (Twitter, GitHub, Discord)

### Menüpunkte bearbeiten

Um **einen Menüpunkt hinzuzufügen/zu entfernen/zu ändern**, bearbeite ausschließlich:
📄 **`src/config/site.ts`** → `navLinks`-Array

Für **Dropdown-Menüs** füge ein `links`-Array zum Menüpunkt hinzu.

---

## Layouts

### `BaseLayout.astro` (`src/layouts/BaseLayout.astro`)

Das einzige Layout des Projekts. Enthält:

1. **Head**: SEO-Component, Schema-Markup, View Transitions (`ClientRouter`), Theme-Script
2. **Body**:
   - Skip-to-Content Link (Accessibility)
   - Hintergrund-Glow-Effekte (radiale Gradienten)
   - Navbar
   - `<main>` mit `<slot />` für Seiteninhalt
   - Footer
   - Vercel Analytics
   - Scroll-Reveal-Animations-Script (IntersectionObserver)

**Props:**

```typescript
interface Props {
  title?: string;
  description?: string;
  ogImage?: string;
  canonical?: string;
  metadata?: {
    title?: string;
    description?: string;
    ogImage?: string;
    canonical?: string;
    ignoreTitleTemplate?: boolean;
  };
}
```

**Verwendung in einer Seite:**

```astro
---
import BaseLayout from "@/layouts/BaseLayout.astro";
---

<BaseLayout title="Meine Seite" description="Beschreibung">
  <!-- Seiteninhalt hier -->
</BaseLayout>
```

---

## Content / Blog-System

### Content Collections

Das Blog-System nutzt **Astro Content Collections** (definiert in `src/content.config.ts`):

```typescript
const blog = defineCollection({
  loader: glob({ pattern: "**/*.{md,mdx}", base: "./src/content/blog" }),
  schema: z.object({
    title: z.string(),
    description: z.string(),
    pubDate: z.coerce.date(),
    author: z.string(),
    image: z.string().optional(),
    tags: z.array(z.string()).optional(),
    category: z.string().optional(),
  }),
});
```

### Einen neuen Blog-Post erstellen

1. Erstelle eine `.md`- oder `.mdx`-Datei in `src/content/blog/`
2. Verwende dieses Frontmatter-Format:

```markdown
---
title: "Mein Titel"
pubDate: "2026-07-16"
description: "Kurze Beschreibung für SEO und Vorschau"
author: "Autor Name"
category: "General"
tags: ["tag1", "tag2"]
image: "/blog/mein-bild.webp"
---

# Inhalt hier...
```

3. Blog-Bilder werden in `public/blog/` abgelegt (WebP-Format bevorzugt)

### Blog-Routing

| Route                    | Seite                                            |
| ------------------------ | ------------------------------------------------ |
| `/blog`                  | Paginierte Übersicht                             |
| `/blog/mein-post-slug`   | Einzelner Post (Slug = Dateiname ohne Extension) |
| `/blog/category/general` | Alle Posts der Kategorie                         |
| `/blog/tags/astro`       | Alle Posts mit dem Tag                           |

---

## Bilder & Assets

### Wo werden Bilder abgelegt?

Es gibt **zwei Orte** für Bilder, je nach Anwendungsfall:

#### `src/assets/images/` – Verarbeitete Bilder (empfohlen)

- Bilder hier werden von **Astro automatisch optimiert** (Größenanpassung, Format-Konvertierung)
- Werden über `import` in Astro-Komponenten eingebunden
- **Verwende diesen Ort für**: Seiten-Bilder, Service-Bilder, OG-Images, allgemeine Assets
- Unterstruktur:
  - `src/assets/images/services/` – Service-bezogene Bilder
  - `src/assets/og-image.png` – Standard Open Graph Bild

```astro
---
import myImage from "@/assets/images/mein-bild.webp";
---

<img src={myImage.src} alt="Beschreibung" />
```

#### `public/blog/` – Statische Blog-Bilder

- Bilder hier werden **1:1 kopiert** ohne Verarbeitung
- Referenziert über URL-Pfad: `/blog/mein-bild.webp`
- **Verwende diesen Ort für**: Blog-Post-Bilder (werden im Frontmatter referenziert)

```markdown
---
image: "/blog/mein-bild.webp"
---
```

#### `public/` – Andere statische Dateien

- `public/favicon.svg` – Favicon

### Bildformate

- **Bevorzugt**: WebP (`.webp`)
- Auch unterstützt: PNG, JPG/JPEG

---

## Styling / Theming

### Tailwind CSS v4

Das Projekt nutzt **Tailwind CSS v4** mit dem Vite-Plugin. Die Konfiguration erfolgt über CSS (nicht `tailwind.config.js`):

**`src/styles/global.css`:**

```css
@import "tailwindcss";
@plugin "@tailwindcss/typography";

@custom-variant dark (&:where([data-theme=dark], [data-theme=dark] *));
```

### Design-Tokens (CSS-Variablen)

| Variable             | Light     | Dark      | Beschreibung           |
| -------------------- | --------- | --------- | ---------------------- |
| `--background`       | `#ffffff` | `#030303` | Hintergrundfarbe       |
| `--foreground`       | `#0a0a0a` | `#e5e7eb` | Textfarbe              |
| `--primary`          | `#0254d8` | `#8bbcff` | Primärfarbe / Akzent   |
| `--border`           | `#e5e7eb` | `#262626` | Rahmenfarbe            |
| `--muted`            | `#f4f4f5` | `#171717` | Gedämpfter Hintergrund |
| `--muted-foreground` | `#52525b` | `#a1a1aa` | Gedämpfter Text        |
| `--card`             | `#ffffff` | `#0a0a0a` | Karten-Hintergrund     |

Diese Variablen werden über `@theme` als Tailwind-Farben verfügbar gemacht:

```css
@theme {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  /* ... */
}
```

**Verwendung in Tailwind-Klassen:** `bg-background`, `text-foreground`, `text-primary`, `border-border`, etc.

### Dark Mode

- Gesteuert über `data-theme`-Attribut auf `<html>`
- Umschaltbar via **ThemeToggle**-Komponente
- Wird in `localStorage` gespeichert (key: `theme`)
- Respektiert `prefers-color-scheme` als Fallback

### Scroll-Animationen

- Klasse `.reveal` auf Elementen → Fade-in + Slide-up beim Scrollen
- Gesteuert über `IntersectionObserver` in `BaseLayout.astro`
- Kompatibel mit Astro View Transitions

---

## SEO

### Automatisch auf jeder Seite

Über `Seo.astro` (in `BaseLayout.astro` eingebunden):

- `<title>` mit Template: `Seitentitel | Astro Starter Pro`
- Meta-Description
- Canonical URL
- Open Graph Tags (og:title, og:description, og:image, og:locale)
- Twitter Card Tags (summary_large_image)
- Autor-Meta-Tag

### Structured Data (JSON-LD)

Über `Schema.astro`:

- **`WebSite`** Schema auf allen Seiten
- **`BlogPosting`** Schema auf Blog-Post-Seiten

### Weitere SEO-Features

- **Sitemap**: Automatisch generiert via `@astrojs/sitemap`
- **RSS-Feed**: `/rss.xml` via `@astrojs/rss`
- **robots.txt**: Dynamisch generiert via `pages/robots.txt.ts`
- **Prefetch**: Alle Links im Viewport werden vorgeladen

---

## TypeScript-Typen

Alle Widget- und Komponenten-Interfaces sind in **`src/types/types.d.ts`** definiert.

### Wichtige Interfaces

| Interface           | Beschreibung                                      |
| ------------------- | ------------------------------------------------- |
| `Widget`            | Basis-Interface für alle Widgets (id, isDark, bg) |
| `HeadlineProps`     | Erweitert Widget mit title, subtitle, tagline     |
| `HeroProps`         | Hero-Banner Props                                 |
| `FeaturesProps`     | Feature-Grid Props                                |
| `ContentProps`      | Text+Bild-Sektion Props                           |
| `PricingProps`      | Preis-Tabelle Props                               |
| `FAQProps`          | FAQ-Liste Props                                   |
| `TestimonialsProps` | Testimonials Props                                |
| `StatsProps`        | Statistiken Props                                 |
| `PortfolioProps`    | Portfolio-Projekte Props                          |
| `ExperienceProps`   | Erfahrungs-Timeline Props                         |
| `SkillsProps`       | Skills-Grid Props                                 |
| `CallToAction`      | CTA-Button (text, href, variant, icon)            |
| `NavLink`           | Navigations-Link (text, href)                     |

### Vererbungs-Hierarchie

```
Widget
  └── HeadlineProps
        ├── HeroProps
        ├── FeaturesProps
        ├── ContentProps
        ├── ServiceListProps
        ├── ValuesProps
        ├── PricingProps
        ├── IntegrationsProps
        ├── StatsProps
        ├── TestimonialsProps
        ├── FAQProps
        ├── PortfolioProps
        ├── ExperienceProps
        └── SkillsProps
```

---

## Code-Qualität & Tooling

### ESLint (`eslint.config.js`)

- Flat Config Format
- Plugins: `eslint-plugin-astro`, `jsx-a11y`, `typescript-eslint`
- Prettier-Integration via `eslint-config-prettier`
- A11y-Regeln: `alt-text` (error), `anchor-is-valid` (error)

### Prettier (`.prettierrc`)

```json
{
  "semi": true,
  "trailingComma": "all",
  "tabWidth": 2,
  "plugins": ["prettier-plugin-astro"]
}
```

### Husky + lint-staged

Pre-Commit-Hook formatiert und lintet automatisch:

- `*.{js,jsx,ts,tsx,astro}` → ESLint fix + Prettier
- `*.{json,md,mdx,css}` → Prettier

### Path-Alias

Import-Kurzform konfiguriert in `tsconfig.json`:

```
@/* → src/*
```

**Beispiel:**

```typescript
import { siteConfig } from "@/config/site";
import Hero from "@/components/widgets/Hero.astro";
```

---

## Skripte

| Skript          | Befehl                             | Beschreibung               |
| --------------- | ---------------------------------- | -------------------------- |
| `dev`           | `astro dev`                        | Entwicklungsserver starten |
| `build`         | `astro build`                      | Produktions-Build          |
| `preview`       | `astro preview`                    | Build-Vorschau             |
| `check`         | `astro check`                      | Astro Type-Check           |
| `typecheck`     | `tsc --noEmit`                     | TypeScript Type-Check      |
| `lint`          | `eslint . --fix`                   | Linting mit Auto-Fix       |
| `lint:check`    | `eslint .`                         | Linting ohne Fix           |
| `format`        | `prettier --write .`               | Formatierung               |
| `fix`           | `npm run format && npm run lint`   | Format + Lint              |
| `test`          | `vitest`                           | Tests ausführen            |
| `build-preview` | `npm run build && npm run preview` | Build + Vorschau           |

---

## Schnellreferenz: Wo lege ich was ab?

| Ich möchte...                     | Ablageort                                             |
| --------------------------------- | ----------------------------------------------------- |
| Einen Menüpunkt ändern            | `src/config/site.ts` → `navLinks`                     |
| Eine neue Seite erstellen         | `src/pages/meine-seite.astro`                         |
| Einen Blog-Post schreiben         | `src/content/blog/mein-post.md`                       |
| Ein Blog-Bild hinzufügen          | `public/blog/mein-bild.webp`                          |
| Ein Seiten-Bild hinzufügen        | `src/assets/images/mein-bild.webp`                    |
| Eine UI-Komponente erstellen      | `src/components/ui/MeineKomponente.astro`             |
| Ein neues Widget/Sektion bauen    | `src/components/widgets/MeinWidget.astro`             |
| Neue TypeScript-Typen definieren  | `src/types/types.d.ts`                                |
| Globale Styles ändern             | `src/styles/global.css`                               |
| Site-Name/URL/Social Links ändern | `src/config/site.ts`                                  |
| SEO-Defaults ändern               | `src/config/site.ts` + `src/components/seo/Seo.astro` |
| Favicon ändern                    | `public/favicon.svg`                                  |
| OG-Image ändern                   | `src/assets/og-image.png`                             |
