# 🎨 Valmora Design System & Tokens

This document outlines the visual architecture, design tokens, and motion guidelines established in the **Valmora Estate** prototype.

---

## 1. Color Palette & Philosophy

The color system avoids stark pure whites (`#FFFFFF`) and deep pure blacks (`#000000`), embracing organic, tactile Mediterranean earth tones reminiscent of granite, weathered timber, aged parchment, and sun-baked schist.

| Token | Hex Value | Role & Usage |
| :--- | :--- | :--- |
| `--ground` | `#F4EFE6` | Primary background canvas; warm parchment |
| `--ground-deep` | `#EAE3D6` | Secondary background, mega-footer, and modal surfaces |
| `--ink` | `#1E1B16` | Primary typographic ink; deep charred umber |
| `--ink-soft` | `#6E675C` | Secondary captions, metadata, and editorial descriptions |
| `--accent-earth` | `#7A4A2B` | Brand signature terracotta accent; hover lines and highlights |
| `--line` | `rgba(30,27,22,0.2)` | Structural 1px hairlines and grid dividers |
| `--scrim` | `linear-gradient(...)` | Subdued cinematic gradient overlay for readable typography |

---

## 2. Typography

A classic European editorial pairing balancing literary grace with crisp, utilitarian legibility:

```css
--font-serif: 'Fraunces', 'Playfair Display', Georgia, serif;
--font-grotesk: 'Archivo', 'Inter', system-ui, sans-serif;
```

### Scale & Ratios
- **Display H1:** `clamp(44px, 6.5vw, 96px)` (Weight: 300, Line-height: 1.05)
- **Section H2:** `clamp(32px, 3.5vw, 52px)` (Weight: 300, Line-height: 1.1)
- **Sub-header H3:** `clamp(22px, 2vw, 30px)` (Weight: 300, Line-height: 1.2)
- **Eyebrow:** `11px`, Uppercase, `letter-spacing: 0.18em`
- **Body Text:** `15px`, `line-height: 1.65`, optimal reading width `62ch`

---

## 3. Spacing & Responsive Grid

- **Max Container Width:** `1440px`
- **Gutter:** `5vw` fluid padding
- **Section Vertical Rhythm:** `clamp(80px, 12vh, 200px)` (Mobile: `clamp(60px, 10vh, 100px)`)
- **Grid Layout:** 12-column CSS Grid with `24px` gutter

---

## 4. Motion Principles

Motion in Valmora conveys calm dignity, natural weight, and physical presence rather than rushed digital snaps.

- **Primary Ease:** `--ease-editorial: cubic-bezier(0.22, 1, 0.36, 1)`
- **Duration Curves:**
  - Element Entrance: `900ms`
  - Micro-interactions & Hovers: `350ms`
  - Page Fade/Transition: `400ms`
- **Accessibility:** Full graceful degradation for users with `prefers-reduced-motion: reduce`.
