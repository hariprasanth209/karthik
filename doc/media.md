### 1. Media Queries

Media queries let you apply different CSS rules based on device characteristics (mainly screen width, but also orientation, resolution, etc.).

**Syntax basics** (most common today):

```css
/* Mobile-first: base styles for small screens first */
body {
  font-size: 1rem;
  padding: 1rem;
}

.card {
  width: 100%;
  margin-bottom: 1.5rem;
}

/* Tablet and up (min-width = progressive enhancement) */
@media (min-width: 768px) {
  .card {
    width: 48%;
    float: left;               /* or use flex/grid instead */
    margin-right: 4%;
  }
  .card:nth-child(2n) {
    margin-right: 0;
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    margin: 0 auto;
  }
  .card {
    width: 31%;
    margin-right: 3.5%;
  }
  .card:nth-child(3n) {
    margin-right: 0;
  }
}
```

Common modern approach in 2026:  
- Use **min-width** queries (mobile-first)  
- Avoid many fixed breakpoints — prefer fluid layouts with Flexbox/Grid + a few logical breakpoints  
- Popular content-driven breakpoints (not strict device sizes):  
  - 480–640px (small phones)  
  - 768px (tablets/portrait)  
  - 1024px (small laptops)  
  - 1280px+ (large screens)












### 2. Mobile-First Thinking

Mobile-first means:  
- Start designing & coding for the **smallest screens** first (base styles = mobile)  
- Then **progressively add** enhancements for larger screens using min-width media queries  
- Why it's essential in 2026:  
  - Most traffic is mobile (often 60%+)  
  - Forces you to prioritize content & performance  
  - Avoids "shrink desktop to mobile" problems (bloated desktop-first sites)

**Mobile-first vs Desktop-first comparison**:




**Desktop-first** (older way — avoid this now):  
```css
/* Base = desktop */
.card { width: 30%; }

/* Then override for smaller → harder to maintain */
@media (max-width: 1023px) { .card { width: 48%; } }
@media (max-width: 767px)  { .card { width: 100%; } }
```

**Mobile-first** (recommended):  
Start simple → add complexity only when screen allows it.

### 3. Viewport Units

Viewport units make sizes relative to the browser window/viewport (great for full-screen sections, heroes, etc.).

Main ones:

| Unit   | Meaning                              | Best use case                          | Caveat on mobile                     |
|--------|--------------------------------------|----------------------------------------|--------------------------------------|
| **vw** | 1% of viewport **width**             | Full-width elements                    | Stable                               |
| **vh** | 1% of viewport **height**            | Hero sections                          | Problematic (includes address bar)   |
| **dvh** | **Dynamic** viewport height          | Mobile full-screen (ignores bars)      | Recommended 2024–2026 standard       |
| **svh** | **Small** viewport height            | When UI bars are expanded              | Safe minimum                         |
| **lvh** | **Large** viewport height            | When UI bars are hidden/minimized      | Max possible                         |

**Real mobile problem with plain vh** (address bar / bottom nav bar changes height):












**Modern fix for full-height hero on mobile**:

```css
.hero {
  height: 100dvh;                    /* dynamic = follows visible viewport */
  min-height: -webkit-fill-available; /* Safari/iOS fallback ~2020–2023 */
  background: linear-gradient(#0066ff, #003399);
  display: grid;
  place-items: center;
  color: white;
}
```

Other viewport tips:  
- `100dvw` for full-width ignoring scrollbar  
- Combine with `min()`/`max()`/`clamp()` for safety:  
  ```css
  font-size: clamp(1rem, 4vw, 2.5rem);
  ```

### Quick Combined Example (2026 best practice snippet)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    :root {
      --spacing: 1.5rem;
    }

    body {
      margin: 0;
      font-family: system-ui, sans-serif;
    }

    .hero {
      height: 80dvh;                    /* safe mobile full-ish height */
      background: #0066ff;
      color: white;
      display: grid;
      place-items: center;
      text-align: center;
      padding: var(--spacing);
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 var(--spacing);
    }

    .cards {
      display: grid;
      grid-template-columns: 1fr;
      gap: var(--spacing);
    }

    .card {
      background: #f8f9fa;
      padding: 1.5rem;
      border-radius: 12px;
    }

    @media (min-width: 640px) {
      .cards { grid-template-columns: repeat(2, 1fr); }
    }

    @media (min-width: 1024px) {
      .cards { grid-template-columns: repeat(3, 1fr); }
      .hero { height: 90dvh; font-size: 1.5rem; }
    }
  </style>
</head>
<body>
  <section class="hero">
    <div>
      <h1>Welcome to Responsive Site</h1>
      <p>Works beautifully on any device — mobile first!</p>
    </div>
  </section>

  <div class="container">
    <div class="cards">
      <div class="card"><h2>Card 1</h2><p>Content here...</p></div>
      <div class="card"><h2>Card 2</h2><p>More content...</p></div>
      <div class="card"><h2>Card 3</h2><p>Even more...</p></div>
    </div>
  </div>
</body>
</html>
```

Resize your browser — see how it adapts smoothly.
