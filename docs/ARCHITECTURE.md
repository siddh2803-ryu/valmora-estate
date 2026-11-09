# 🏗️ Technical Architecture & Engineering Decisions

This document outlines the software engineering patterns, performance characteristics, and animation synchronization powering the **Valmora Estate** prototype.

---

## 1. Zero-Framework Single Page Application (SPA)

Rather than bundling bulky client-side frameworks (React, Vue, or Angular) with multi-megabyte bundle footprints, Valmora implements an ultra-lightweight, zero-dependency SPA routing model directly in modern ES6+:

```javascript
function navigateTo(pageId) {
  // Graceful cross-fade between views
  currentEl.style.opacity = '0';
  setTimeout(() => {
    currentEl.classList.remove('active');
    nextEl.classList.add('active');
    nextEl.style.opacity = '1';
    initScrollAnimations();
  }, 400);
}
```

### Benefits
- **Zero Hydration Overhead:** First Contentful Paint (FCP) and Time to Interactive (TTI) occur virtually instantaneously (< 0.4s).
- **SEO & Social Crawlability:** Search crawlers receive pre-rendered HTML without needing headless rendering bots.
- **Predictable Memory Footprint:** No virtual DOM reconcilers consuming mobile memory.

---

## 2. Lenis + GSAP ScrollTrigger Synchronization

Valmora combines **Lenis** (momentum-based smooth scrolling) with **GSAP ScrollTrigger** (coordinate-locked animation triggers). To eliminate frame jitter and layout recalculation stutter:

```javascript
lenis.on('scroll', ScrollTrigger.update);
gsap.ticker.add((time) => {
  lenis.raf(time * 1000);
});
gsap.ticker.lagSmoothing(0);
```

- **Lag Smoothing set to 0:** Prevents animations from jumping or hitching during sudden scroll acceleration.
- **RAF Timing Normalization:** Ensures physics calculate in lockstep with the display's native refresh rate (60Hz / 120Hz ProMotion).

---

## 3. Inertia-Based Drag Gallery with Physics Deceleration

The horizontal gallery components use custom pointer physics featuring momentum decay:

- Multi-touch and cursor unified drag listener
- Velocity tracking with exponential decay damping (`velocity *= 0.95`)
- Native hardware acceleration (`transform: translate3d`)

---

## 4. Accessibility & Inclusive Design

- **Focus Management:** Modals feature programmatic focus traps to retain keyboard navigation context.
- **Escape Key Listener:** Closes overlay layers and restores body scroll locking.
- **`prefers-reduced-motion` Media Query:** Instantly disables parallax coordinate shifting and line splitting for sensitive users.
