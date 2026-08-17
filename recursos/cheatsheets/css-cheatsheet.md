# 📋 CSS Cheatsheet — Referência Rápida

---

## 📐 Flexbox

```css
/* Container */
display: flex;
flex-direction: row | column;
flex-wrap: wrap;
justify-content: center | space-between | space-evenly;
align-items: center | flex-start | flex-end | stretch;
gap: 16px;

/* Item */
flex: 1;              /* Cresce igualmente */
flex: 0 0 200px;      /* Fixo em 200px */
align-self: center;
order: -1;            /* Mover para o início */
```

## 🔲 Grid

```css
/* Container */
display: grid;
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
grid-template-rows: auto 1fr auto;
grid-template-areas: "header header" "sidebar main" "footer footer";
gap: 16px;

/* Item */
grid-column: span 2;
grid-area: header;
```

## 🎨 Variáveis

```css
:root { --cor: #06b6d4; }
.el  { color: var(--cor, fallback); }
```

## 📱 Responsividade

```css
/* Mobile-first */
.el { font-size: 14px; }
@media (min-width: 768px) { .el { font-size: 16px; } }
@media (min-width: 1024px) { .el { font-size: 18px; } }

/* clamp */
font-size: clamp(1rem, 2.5vw, 2rem);
width: min(90%, 1200px);
```

## ✨ Animações

```css
/* Transição */
transition: transform 0.3s ease, opacity 0.3s ease;

/* Keyframes */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
.el { animation: fadeIn 0.5s ease-out; }
```

## 🎯 Seletores Úteis

```css
:hover :focus :active :focus-visible
:first-child :last-child :nth-child(odd)
:not(.classe)
:has(img)
::before ::after ::placeholder ::selection
```

## 📦 Box Model

```css
*, *::before, *::after { box-sizing: border-box; }
```

## 🌗 Dark Mode

```css
:root { --bg: white; --text: black; }
[data-theme="dark"] { --bg: #111; --text: white; }
@media (prefers-color-scheme: dark) { ... }
```

## 📏 Unidades

```
px    — Pixels (fixo)
rem   — Relativo à raiz (=16px)
em    — Relativo ao pai
%     — Percentual do pai
vw/vh — Viewport width/height
fr    — Fração (Grid)
```

## 🏷️ BEM

```
.block
.block__element
.block--modifier
```
