# 📖 Semana 4 — CSS Avançado: Flexbox, Grid, Animações e Responsividade

> *"CSS é a arte de transformar estrutura em experiência visual."*

## 📋 Índice

1. [CSS Moderno — Fundamentos](#1-css-moderno--fundamentos)
2. [Seletores Avançados](#2-seletores-avançados)
3. [Box Model e Layout](#3-box-model-e-layout)
4. [Flexbox — Completo](#4-flexbox--completo)
5. [CSS Grid — Completo](#5-css-grid--completo)
6. [Custom Properties (Variáveis CSS)](#6-custom-properties-variáveis-css)
7. [Responsividade](#7-responsividade)
8. [Animações e Transições](#8-animações-e-transições)
9. [Arquitetura CSS (BEM)](#9-arquitetura-css-bem)
10. [Boas Práticas e Performance](#10-boas-práticas-e-performance)
11. [Exercícios Práticos](#11-exercícios-práticos)

---

## 1. CSS Moderno — Fundamentos

### 1.1 Como o CSS Funciona

O navegador processa CSS em 3 etapas:

```
1. PARSING        → Lê o CSS e cria regras
2. CASCADE        → Resolve conflitos (especificidade, ordem, !important)
3. RENDER TREE    → Calcula posição e pinta pixels na tela
```

### 1.2 Cascata e Especificidade

Quando duas regras afetam o mesmo elemento, quem ganha?

**Ordem de prioridade (da menor para a maior):**

```
1. Estilos do navegador (user agent)
2. Estilos externos/internos (seu CSS)
3. Estilos inline (style="...")
4. !important (evite ao máximo!)
```

**Cálculo de Especificidade:**

```
Seletor                              Especificidade
─────────────────────────────────────────────────────
*                                    0-0-0
elemento (p, div, h1)                0-0-1
.classe                              0-1-0
#id                                  1-0-0
style=""                             1-0-0-0
!important                           ∞ (ganha de tudo)

Exemplos:
p                                    0-0-1
p.intro                              0-1-1
#header .nav a                       1-1-1
#header .nav a:hover                 1-2-1
```

**Regra simples:** Se a especificidade for igual, a última regra no CSS ganha.

### 1.3 Herança

Algumas propriedades são herdadas automaticamente (do pai para o filho):

```
✅ Herdadas: color, font-*, text-*, line-height, letter-spacing, visibility
❌ NÃO herdadas: margin, padding, border, background, width, height, display
```

```css
/* Para forçar herança */
.filho {
  border: inherit;      /* Herda do pai */
  margin: initial;      /* Valor padrão do navegador */
  padding: unset;       /* Herda se herdável, senão initial */
}
```

---

## 2. Seletores Avançados

### 2.1 Seletores de Atributo

```css
/* Tem o atributo */
[disabled] { opacity: 0.5; }

/* Valor exato */
[type="email"] { border-color: blue; }

/* Começa com */
[href^="https"] { color: green; }

/* Termina com */
[href$=".pdf"] { color: red; }

/* Contém */
[class*="card"] { border-radius: 12px; }
```

### 2.2 Pseudo-classes

```css
/* Estado */
a:hover { color: blue; }
a:active { color: red; }
a:visited { color: purple; }
input:focus { border-color: #06b6d4; }
input:focus-visible { outline: 3px solid #06b6d4; }  /* Só quando foca por teclado */

/* Validação de formulários */
input:valid { border-color: green; }
input:invalid { border-color: red; }
input:required { border-left: 3px solid red; }
input:placeholder-shown { background: #f0f0f0; }

/* Estruturais */
li:first-child { font-weight: bold; }
li:last-child { border-bottom: none; }
li:nth-child(odd) { background: #f8f8f8; }    /* Ímpares (1, 3, 5...) */
li:nth-child(even) { background: white; }      /* Pares (2, 4, 6...) */
li:nth-child(3n) { color: red; }               /* Cada 3 itens */
li:nth-child(3) { font-size: 1.2rem; }         /* Só o terceiro */
p:first-of-type { font-size: 1.2rem; }         /* Primeiro <p> do pai */
p:last-of-type { margin-bottom: 0; }

/* Negação */
a:not(.btn) { text-decoration: underline; }
input:not([type="hidden"]) { margin-bottom: 10px; }

/* Vazio */
p:empty { display: none; }

/* Has (NOVO e poderoso!) */
.card:has(img) { padding-top: 0; }              /* Card que TEM imagem */
.card:has(:focus) { box-shadow: 0 0 0 3px blue; } /* Card com foco dentro */
```

### 2.3 Pseudo-elementos

```css
/* Antes e depois (conteúdo decorativo) */
.required::before {
  content: "* ";
  color: red;
}

blockquote::before {
  content: open-quote;
  font-size: 3rem;
  color: #ccc;
}

/* Primeira letra e primeira linha */
p::first-letter {
  font-size: 3rem;
  float: left;
  line-height: 1;
}

p::first-line {
  font-weight: bold;
}

/* Seleção de texto */
::selection {
  background: #06b6d4;
  color: white;
}

/* Placeholder */
input::placeholder {
  color: #999;
  font-style: italic;
}

/* Scrollbar (Webkit) */
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-track { background: #f1f1f1; }
::-webkit-scrollbar-thumb { background: #888; border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #555; }
```

### 2.4 Combinadores

```css
/* Descendente (qualquer nível) */
article p { color: #333; }

/* Filho direto */
.nav > li { display: inline-block; }

/* Irmão adjacente (imediatamente após) */
h2 + p { font-size: 1.1rem; }

/* Irmãos gerais (todos após) */
h2 ~ p { color: #666; }
```

---

## 3. Box Model e Layout

### 3.1 Box Model

```
┌─────────────────────────────────────┐
│              MARGIN                 │
│   ┌─────────────────────────────┐   │
│   │          BORDER             │   │
│   │   ┌─────────────────────┐   │   │
│   │   │      PADDING        │   │   │
│   │   │   ┌─────────────┐   │   │   │
│   │   │   │   CONTENT   │   │   │   │
│   │   │   └─────────────┘   │   │   │
│   │   └─────────────────────┘   │   │
│   └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

```css
/* SEMPRE use border-box (99% dos projetos) */
*, *::before, *::after {
  box-sizing: border-box;
}

/* content-box (padrão): width = só o conteúdo */
/* border-box: width = conteúdo + padding + border */
```

### 3.2 Display

```css
display: block;         /* Ocupa linha inteira (div, p, h1) */
display: inline;        /* Flui com texto (span, a, strong) */
display: inline-block;  /* Inline + aceita width/height */
display: none;          /* Remove completamente */
display: flex;          /* Container flexbox */
display: grid;          /* Container grid */
display: inline-flex;   /* Flexbox inline */
display: inline-grid;   /* Grid inline */
```

### 3.3 Position

```css
position: static;       /* Padrão: fluxo normal */
position: relative;     /* Relativo à posição original (cria contexto) */
position: absolute;     /* Relativo ao ancestral posicionado mais próximo */
position: fixed;        /* Relativo ao viewport (não scrolla) */
position: sticky;       /* Misto: relative até um threshold, depois fixed */
```

```css
/* Sticky: fica fixo quando scrolla até ele */
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: white;
}
```

---

## 4. Flexbox — Completo

> Flexbox é para layouts **unidimensionais** (linha OU coluna).

### 4.1 Container (Pai)

```css
.container {
  display: flex;

  /* Direção dos itens */
  flex-direction: row;             /* ← → (padrão) */
  flex-direction: row-reverse;     /* → ← */
  flex-direction: column;          /* ↓ */
  flex-direction: column-reverse;  /* ↑ */

  /* Quebra de linha */
  flex-wrap: nowrap;     /* Tudo em uma linha (padrão) */
  flex-wrap: wrap;       /* Quebra quando não cabe */
  flex-wrap: wrap-reverse;

  /* Alinhamento no eixo PRINCIPAL (horizontal em row) */
  justify-content: flex-start;     /* |||.......... */
  justify-content: flex-end;       /* ...........||| */
  justify-content: center;         /* .....|||..... */
  justify-content: space-between;  /* |.....||.....| */
  justify-content: space-around;   /* ..|..||..||..| */
  justify-content: space-evenly;   /* ..|..|..|..|.. */

  /* Alinhamento no eixo CRUZADO (vertical em row) */
  align-items: stretch;      /* Esticam para preencher (padrão) */
  align-items: flex-start;   /* No topo */
  align-items: flex-end;     /* Na base */
  align-items: center;       /* Centralizado verticalmente */
  align-items: baseline;     /* Alinha pela linha de texto */

  /* Alinhamento das LINHAS (quando tem wrap) */
  align-content: flex-start;
  align-content: flex-end;
  align-content: center;
  align-content: space-between;
  align-content: space-around;
  align-content: stretch;

  /* Gap (espaçamento entre itens) */
  gap: 16px;               /* Todos os lados */
  row-gap: 16px;           /* Entre linhas */
  column-gap: 24px;        /* Entre colunas */
}
```

### 4.2 Itens (Filhos)

```css
.item {
  /* Ordem (padrão: 0) */
  order: 1;

  /* Crescimento (preencher espaço disponível) */
  flex-grow: 0;    /* Não cresce (padrão) */
  flex-grow: 1;    /* Cresce para preencher */

  /* Encolhimento (quando não cabe) */
  flex-shrink: 1;  /* Encolhe (padrão) */
  flex-shrink: 0;  /* Não encolhe */

  /* Tamanho base */
  flex-basis: auto;  /* Tamanho natural (padrão) */
  flex-basis: 200px; /* Tamanho fixo */
  flex-basis: 25%;   /* Percentual */

  /* Atalho: grow shrink basis */
  flex: 1;           /* flex: 1 1 0% — cresce e encolhe igualmente */
  flex: 0 0 200px;   /* Não cresce, não encolhe, 200px fixo */

  /* Alinhamento individual (sobrescreve align-items do pai) */
  align-self: auto;
  align-self: center;
  align-self: flex-start;
  align-self: flex-end;
  align-self: stretch;
}
```

### 4.3 Padrões Comuns com Flexbox

```css
/* Centralizar perfeitamente */
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Card com footer fixo na base */
.card {
  display: flex;
  flex-direction: column;
}
.card .content { flex: 1; }         /* Cresce */
.card .footer { flex-shrink: 0; }   /* Não encolhe */

/* Itens iguais */
.grid-equal > * { flex: 1; }

/* Holy Grail Layout */
.page {
  display: flex;
  min-height: 100vh;
}
.sidebar { flex: 0 0 250px; }
.main { flex: 1; }
```

---

## 5. CSS Grid — Completo

> Grid é para layouts **bidimensionais** (linhas E colunas).

### 5.1 Container (Pai)

```css
.grid {
  display: grid;

  /* Definir colunas */
  grid-template-columns: 200px 1fr 200px;          /* 3 colunas */
  grid-template-columns: repeat(3, 1fr);            /* 3 iguais */
  grid-template-columns: repeat(4, minmax(200px, 1fr)); /* Mín 200px */
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); /* Responsivo! */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));  /* Responsivo! */

  /* Definir linhas */
  grid-template-rows: auto 1fr auto;               /* Header, main, footer */
  grid-auto-rows: minmax(100px, auto);              /* Linhas automáticas */

  /* Gap */
  gap: 16px;
  row-gap: 20px;
  column-gap: 16px;

  /* Template Areas (visual e poderoso!) */
  grid-template-areas:
    "header  header  header"
    "sidebar main   aside"
    "footer  footer  footer";

  /* Alinhamento */
  justify-items: stretch;    /* Horizontal dentro da célula */
  align-items: stretch;      /* Vertical dentro da célula */
  justify-content: center;   /* Horizontal do grid inteiro */
  align-content: center;     /* Vertical do grid inteiro */
  place-items: center;       /* Atalho para align-items + justify-items */
}
```

### 5.2 auto-fill vs auto-fit

```css
/* auto-fill: cria colunas vazias se tiver espaço */
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));

/* auto-fit: estica itens existentes para preencher o espaço */
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));

/* Na prática: auto-fit é o mais usado (itens crescem para preencher) */
```

### 5.3 Itens (Filhos)

```css
.item {
  /* Posicionar por linhas */
  grid-column: 1 / 3;      /* Da coluna 1 até a 3 (ocupa 2 colunas) */
  grid-column: 1 / -1;     /* Da primeira até a última coluna (full width) */
  grid-column: span 2;     /* Ocupa 2 colunas */
  grid-row: 1 / 3;         /* Da linha 1 até a 3 */

  /* Posicionar por área (precisa de grid-template-areas no pai) */
  grid-area: header;
  grid-area: sidebar;
  grid-area: main;
  grid-area: footer;

  /* Alinhamento individual */
  justify-self: center;
  align-self: center;
  place-self: center;       /* Atalho */
}
```

### 5.4 Layout Completo com Grid

```css
/* Layout de página com areas nomeadas */
.page {
  display: grid;
  grid-template-areas:
    "header header header"
    "nav    main   aside"
    "footer footer footer";
  grid-template-columns: 200px 1fr 250px;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
  gap: 0;
}

.page > header { grid-area: header; }
.page > nav    { grid-area: nav; }
.page > main   { grid-area: main; }
.page > aside  { grid-area: aside; }
.page > footer { grid-area: footer; }

/* Responsivo: no mobile, tudo vira coluna */
@media (max-width: 768px) {
  .page {
    grid-template-areas:
      "header"
      "nav"
      "main"
      "aside"
      "footer";
    grid-template-columns: 1fr;
  }
}
```

### 5.5 Grid de Cards Responsivo (Sem Media Queries!)

```css
/* O padrão mais útil do CSS Grid */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
}
```

---

## 6. Custom Properties (Variáveis CSS)

### 6.1 Declaração e Uso

```css
/* Declarar no :root (globais) */
:root {
  /* Cores */
  --color-primary: #06b6d4;
  --color-primary-dark: #0891b2;
  --color-secondary: #8b5cf6;
  --color-bg: #0a0e17;
  --color-surface: #1a2234;
  --color-text: #f1f5f9;
  --color-text-muted: #94a3b8;

  /* Tipografia */
  --font-family: 'Inter', -apple-system, sans-serif;
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font-size-2xl: 1.5rem;

  /* Espaçamento */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;

  /* Bordas */
  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-full: 9999px;

  /* Sombras */
  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.15);
  --shadow-lg: 0 10px 30px rgba(0, 0, 0, 0.2);

  /* Transição */
  --transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Usar as variáveis */
.card {
  background: var(--color-surface);
  color: var(--color-text);
  padding: var(--space-lg);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-md);
  font-family: var(--font-family);
  transition: transform var(--transition);
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

/* Valor fallback */
.element {
  color: var(--cor-que-nao-existe, red); /* Usa red se a variável não existir */
}
```

### 6.2 Tema Dark/Light

```css
/* Tema claro (padrão) */
:root {
  --bg: #ffffff;
  --text: #1a1a1a;
  --surface: #f5f5f5;
  --border: #e0e0e0;
}

/* Tema escuro */
[data-theme="dark"] {
  --bg: #0a0e17;
  --text: #f1f5f9;
  --surface: #1a2234;
  --border: rgba(148, 163, 184, 0.1);
}

/* Ou: respeitar preferência do sistema */
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0a0e17;
    --text: #f1f5f9;
    --surface: #1a2234;
    --border: rgba(148, 163, 184, 0.1);
  }
}

/* Usar nos componentes */
body {
  background: var(--bg);
  color: var(--text);
}
```

```html
<!-- Toggle com JavaScript (simples) -->
<button onclick="document.documentElement.dataset.theme =
  document.documentElement.dataset.theme === 'dark' ? 'light' : 'dark'">
  🌙 / ☀️
</button>
```

---

## 7. Responsividade

### 7.1 Mobile-First

Sempre escreva CSS primeiro para mobile, depois adicione estilos para telas maiores:

```css
/* Mobile (base) */
.container {
  padding: 16px;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

/* Tablet */
@media (min-width: 768px) {
  .container {
    padding: 24px;
    max-width: 768px;
    margin: 0 auto;
  }

  .grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    padding: 32px;
  }

  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

/* Desktop grande */
@media (min-width: 1440px) {
  .container {
    max-width: 1400px;
  }
}
```

### 7.2 Breakpoints Comuns

```
320px   — Mobile pequeno
375px   — Mobile médio (iPhone)
425px   — Mobile grande
768px   — Tablet
1024px  — Laptop
1440px  — Desktop
2560px  — 4K
```

### 7.3 Unidades Responsivas

```css
/* rem — relativo ao font-size da raiz (html), mais consistente */
font-size: 1rem;      /* 16px (padrão) */
padding: 1.5rem;      /* 24px */

/* em — relativo ao font-size do pai (efeito cascata) */
margin-bottom: 1em;

/* vw/vh — viewport width/height */
width: 100vw;         /* Largura total da tela */
height: 100vh;        /* Altura total da tela */
font-size: 5vw;       /* Texto que cresce com a tela */

/* % — relativo ao pai */
width: 50%;

/* clamp() — valor responsivo com limites (MUITO ÚTIL!) */
font-size: clamp(1rem, 2.5vw, 2rem);    /* Mín 1rem, máx 2rem, 2.5vw ideal */
width: clamp(280px, 80%, 1200px);        /* Largura responsiva com limites */
padding: clamp(16px, 4vw, 48px);         /* Padding responsivo */

/* min() e max() */
width: min(90%, 1200px);                 /* O menor dos dois */
padding: max(16px, 2vw);                 /* O maior dos dois */
```

### 7.4 Container Queries (Novo!)

```css
/* Definir container */
.card-wrapper {
  container-type: inline-size;
  container-name: card;
}

/* Estilos baseados no tamanho do CONTAINER, não da viewport */
@container card (min-width: 400px) {
  .card {
    display: flex;
    gap: 16px;
  }
}
```

---

## 8. Animações e Transições

### 8.1 Transitions

```css
/* Transição básica */
.button {
  background: #06b6d4;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  cursor: pointer;

  /* Propriedade, duração, timing, delay */
  transition: all 0.3s ease;
  /* Ou mais específico (melhor para performance): */
  transition: background 0.3s ease, transform 0.2s ease;
}

.button:hover {
  background: #0891b2;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(6, 182, 212, 0.3);
}

.button:active {
  transform: translateY(0);
}
```

**Timing functions:**
```css
transition-timing-function: ease;           /* Padrão (lento-rápido-lento) */
transition-timing-function: ease-in;        /* Lento no início */
transition-timing-function: ease-out;       /* Lento no final */
transition-timing-function: ease-in-out;    /* Lento nos dois */
transition-timing-function: linear;         /* Velocidade constante */
transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1); /* Personalizado */
```

### 8.2 Keyframes

```css
/* Definir a animação */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Usar a animação */
.card {
  animation: fadeInUp 0.6s ease-out;
}

/* Com delay para efeito cascata */
.card:nth-child(1) { animation-delay: 0.1s; }
.card:nth-child(2) { animation-delay: 0.2s; }
.card:nth-child(3) { animation-delay: 0.3s; }

/* Spinner de loading */
.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #e0e0e0;
  border-top-color: #06b6d4;
  border-radius: 50%;
  animation: rotate 0.8s linear infinite;
}

/* Gradiente animado */
.gradient-bg {
  background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  background-size: 400% 400%;
  animation: gradient 15s ease infinite;
}
```

### 8.3 Propriedades de Animação

```css
.element {
  animation-name: fadeInUp;
  animation-duration: 0.6s;
  animation-timing-function: ease-out;
  animation-delay: 0.2s;
  animation-iteration-count: 1;        /* infinite para repetir */
  animation-direction: normal;          /* reverse, alternate */
  animation-fill-mode: both;           /* forwards, backwards, both */
  animation-play-state: running;       /* paused */

  /* Atalho */
  animation: fadeInUp 0.6s ease-out 0.2s 1 normal both;
}

/* Preferência do usuário: respeitar quem não quer animações */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

### 8.4 Performance de Animações

```
✅ Propriedades BARATAS (GPU):     ❌ Propriedades CARAS (CPU):
   transform                          width, height
   opacity                            margin, padding
                                      top, left, right, bottom
                                      border
                                      font-size
```

```css
/* ✅ BOM: anima transform (GPU) */
.card:hover { transform: translateY(-4px) scale(1.02); }

/* ❌ RUIM: anima top (CPU, causa repaint) */
.card:hover { top: -4px; }

/* Dica: force GPU com will-change (use com moderação!) */
.card {
  will-change: transform;
}
```

---

## 9. Arquitetura CSS (BEM)

### 9.1 O que é BEM?

**BEM** = Block, Element, Modifier. Uma convenção de nomenclatura para classes CSS.

```
.block                  → Componente independente
.block__element         → Parte do componente
.block--modifier        → Variação do componente
.block__element--modifier → Variação do elemento
```

### 9.2 Exemplos

```html
<!-- Card -->
<div class="card card--featured">
  <img class="card__image" src="..." alt="...">
  <div class="card__content">
    <h3 class="card__title">Título</h3>
    <p class="card__description">Descrição...</p>
  </div>
  <div class="card__footer">
    <a class="card__link card__link--primary" href="#">Ler mais</a>
  </div>
</div>
```

```css
/* Bloco */
.card {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  overflow: hidden;
}

/* Modificador do bloco */
.card--featured {
  border: 2px solid var(--color-primary);
}

/* Elementos */
.card__image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card__content {
  padding: var(--space-lg);
}

.card__title {
  font-size: var(--font-size-xl);
  margin-bottom: var(--space-sm);
}

.card__description {
  color: var(--color-text-muted);
}

.card__footer {
  padding: var(--space-md) var(--space-lg);
  border-top: 1px solid var(--border);
}

/* Modificador do elemento */
.card__link--primary {
  color: var(--color-primary);
  font-weight: 600;
}
```

### 9.3 Quando NÃO usar BEM

- **Utility classes** (como margem, padding): `.mt-4`, `.text-center`
- **Estados dinâmicos**: `.is-active`, `.is-hidden`, `.has-error`
- **JavaScript hooks**: `[data-toggle]`, `[data-modal]`

---

## 10. Boas Práticas e Performance

### 10.1 Reset / Normalize

```css
/* Reset mínimo e moderno */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
  -webkit-text-size-adjust: 100%;
}

body {
  min-height: 100vh;
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

img, picture, video, canvas, svg {
  display: block;
  max-width: 100%;
  height: auto;
}

input, button, textarea, select {
  font: inherit;
}

p, h1, h2, h3, h4, h5, h6 {
  overflow-wrap: break-word;
}

ul, ol {
  list-style: none;
}

a {
  color: inherit;
  text-decoration: none;
}
```

### 10.2 Ordem das Propriedades (Recomendado)

```css
.element {
  /* 1. Posicionamento */
  position: relative;
  top: 0;
  z-index: 1;

  /* 2. Display e Layout */
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 16px;

  /* 3. Box Model */
  width: 100%;
  max-width: 1200px;
  padding: 16px;
  margin: 0 auto;

  /* 4. Visual */
  background: white;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);

  /* 5. Tipografia */
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  font-weight: 400;
  color: #333;
  line-height: 1.6;

  /* 6. Outros */
  cursor: pointer;
  transition: all 0.3s ease;
  overflow: hidden;
}
```

### 10.3 Checklist de Performance CSS

- [ ] Use `box-sizing: border-box` global
- [ ] Anime apenas `transform` e `opacity`
- [ ] Use `will-change` com moderação
- [ ] Minimize o uso de `!important`
- [ ] Evite seletores muito profundos (`div > ul > li > a > span`)
- [ ] Use `loading="lazy"` nas imagens
- [ ] Minifique o CSS para produção
- [ ] Respeite `prefers-reduced-motion`
- [ ] Respeite `prefers-color-scheme`

---

## 11. Exercícios Práticos

Veja os exercícios na pasta `exercicios/` desta seção.

---

## 📚 Recursos

| Recurso | Tipo | Link |
|---------|------|------|
| Flexbox Froggy | Jogo | [flexboxfroggy.com](https://flexboxfroggy.com) |
| Grid Garden | Jogo | [cssgridgarden.com](https://cssgridgarden.com) |
| CSS Tricks Flexbox | Guia | [css-tricks.com/flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) |
| CSS Tricks Grid | Guia | [css-tricks.com/grid](https://css-tricks.com/snippets/css/complete-guide-grid/) |
| Modern CSS | Blog | [moderncss.dev](https://moderncss.dev) |
| Animista | Gerador | [animista.net](https://animista.net) |
| 100 Days CSS | Desafios | [100dayscss.com](https://100dayscss.com) |
| Can I Use | Compat. | [caniuse.com](https://caniuse.com) |
| web.dev Learn CSS | Curso | [web.dev/learn/css](https://web.dev/learn/css) |

---

## ✅ Checklist da Semana

- [ ] Entende a cascata e especificidade
- [ ] Domina seletores avançados (pseudo-classes, pseudo-elementos)
- [ ] Flexbox: sabe centralizar, distribuir e alinhar
- [ ] Grid: sabe criar layouts com template-areas e auto-fit
- [ ] Usa Custom Properties para Design Tokens
- [ ] Implementa tema dark/light
- [ ] Cria layouts mobile-first com media queries
- [ ] Usa unidades responsivas (rem, clamp, min, max)
- [ ] Cria animações suaves com transitions e keyframes
- [ ] Segue a convenção BEM para nomenclatura
- [ ] Completou Flexbox Froggy e Grid Garden
- [ ] Completou todos os exercícios práticos
