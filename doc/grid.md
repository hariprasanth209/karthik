### 1. Grid Container Setup

Turn any element into a **grid container** with one property:

```css
.container {
  display: grid;
  /* or */
  display: inline-grid;   /* if you want it to behave like inline-block */
}
```

Once you set `display: grid`, its **direct children** become **grid items**.

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <!-- ... -->
</div>
```








### 2. Columns / Rows (Defining the grid structure)

You define the tracks (columns and rows) using:

- `grid-template-columns` → defines **column widths**
- `grid-template-rows`    → defines **row heights**

Common units in 2025–2026:
- `fr`       → fraction of available space (most powerful)
- `auto`     → content-based size
- `px`, `%`, `minmax()`, `repeat()`

Examples:

```css
/* 3 equal-width columns */
.container {
  grid-template-columns: 1fr 1fr 1fr;
  /* same as */ 
  grid-template-columns: repeat(3, 1fr);
}

/* Classic sidebar + main layout */
.container {
  grid-template-columns: 250px 1fr 200px;   /* fixed - flexible - fixed */
  grid-template-rows: auto 1fr auto;        /* header - content - footer */
}

/* Responsive card grid (auto-fits as many as possible) */
.cards {
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  /* → shrinks/grows nicely on any screen size */
}
```




### 3. Gap (Gutters between tracks)

`gap` is the modern, clean way to add space between grid cells (replaces old margin hacks).

```css
.container {
  gap: 24px;              /* sets both row-gap and column-gap */
  
  /* or separately: */
  row-gap: 2rem;
  column-gap: 1.5rem;
}
```

Very important:  
- `gap` only adds space **between** items — **not** around the container edges  
- Much better than margins (no collapsing, no last-child hacks)



### 4. Placement (Positioning items on the grid)

You have two main ways to place items:

**A. Line-based placement** (using column/row lines)

```css
.item-featured {
  grid-column: 1 / -1;           /* start at column line 1 → end at last line (full width) */
  grid-row: 2 / 4;               /* starts at row line 2, ends before row line 4 (spans 2 rows) */
}

/* shorthand */
.item-special {
  grid-area: 2 / 3 / 5 / 6;     /* row-start / col-start / row-end / col-end */
}
```




**B. Named areas** (most readable for page layouts)

1. Name areas in the container:

```css
.container {
  grid-template-areas:
    "header  header  header"
    "sidebar main    main"
    "footer  footer  footer";
  
  /* optional: give implicit sizes too */
  grid-template-columns: 280px 1fr;
  grid-template-rows: auto 1fr auto;
}
```

2. Assign items to those names:

```css
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```








### Quick Real-World Combo Example (Dashboard / Page Layout)

```css
.page {
  display: grid;
  grid-template-columns: 260px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  gap: 1.5rem;
  min-height: 100dvh;
  padding: 1rem;
}

.header  { grid-area: header; background: #0066ff; color: white; }
.sidebar { grid-area: sidebar; background: #f0f4ff; }
.main    { grid-area: main;    background: #ffffff; }
.footer  { grid-area: footer;  background: #333; color: white; }
```

This creates a classic responsive page structure in ~15 lines of CSS.

Grid is your go-to when Flexbox feels too one-dimensional. Use Flexbox for **components** (cards, nav, buttons), Grid for **overall page / section layouts**.
