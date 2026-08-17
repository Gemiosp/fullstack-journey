# 🏋️ Exercícios Práticos — CSS Avançado

> Complete na ordem. O exercício final é estilizar o currículo do módulo de HTML.

---

## Exercício 1: Flexbox Froggy + Grid Garden

**Objetivo:** Dominar Flexbox e Grid através de jogos interativos.

### Tarefas:

1. Complete **todos os 24 níveis** do [Flexbox Froggy](https://flexboxfroggy.com)
2. Complete **todos os 28 níveis** do [Grid Garden](https://cssgridgarden.com)
3. Crie `exercicio-css-01/anotacoes.md` documentando:
   - Os 5 conceitos mais importantes que aprendeu
   - As propriedades que mais confundiram
   - Dicas que criou para lembrar

**Tempo estimado:** 2-3 horas

### ✅ Resultado esperado:
- Ambos os jogos completos (pode tirar print da tela final)
- Arquivo de anotações com reflexões

---

## Exercício 2: Componentes com Flexbox

**Objetivo:** Criar componentes reais de UI usando apenas Flexbox.

### Tarefas:

1. Crie `exercicio-css-02/index.html` e `style.css`
2. Implemente os seguintes componentes (todos com Flexbox):

**a) Navbar responsiva:**
- Logo à esquerda, links ao centro, botão à direita
- No mobile: links empilhados em coluna

**b) Card de produto:**
- Imagem no topo
- Título, descrição, preço
- Footer com botão "Comprar" fixo na base (mesmo que o conteúdo varie de tamanho)
- Efeito hover sutil (shadow + translate)

**c) Footer com 4 colunas:**
- Sobre, Links, Contato, Redes Sociais
- No mobile: 1 coluna
- No tablet: 2 colunas

**d) Lista de avatares empilhados:**
- Círculos sobrepostos (como o GitHub mostra contribuidores)
- Use `margin-left: -10px` para sobreposição

3. Use **variáveis CSS** para cores e espaçamentos
4. Siga a nomenclatura **BEM** para as classes

### ✅ Resultado esperado:
- 4 componentes funcionais e responsivos
- Código limpo com BEM e variáveis CSS

---

## Exercício 3: Layout com CSS Grid

**Objetivo:** Criar um layout de página completo usando Grid.

### Tarefas:

1. Crie `exercicio-css-03/index.html` e `style.css`
2. Implemente um layout de **Dashboard** com Grid:

```
Desktop:
┌──────────────────────────────┐
│           HEADER             │
├──────┬───────────────┬───────┤
│      │               │       │
│ SIDE │   CONTEÚDO    │ ASIDE │
│ BAR  │   PRINCIPAL   │       │
│      │               │       │
├──────┴───────────────┴───────┤
│           FOOTER             │
└──────────────────────────────┘

Tablet:
┌──────────────────────────────┐
│           HEADER             │
├──────┬───────────────────────┤
│ SIDE │    CONTEÚDO           │
│ BAR  │    PRINCIPAL          │
├──────┴───────────────────────┤
│           ASIDE              │
├──────────────────────────────┤
│           FOOTER             │
└──────────────────────────────┘

Mobile:
┌────────────────┐
│    HEADER      │
├────────────────┤
│   CONTEÚDO     │
│   PRINCIPAL    │
├────────────────┤
│    SIDEBAR     │
├────────────────┤
│    ASIDE       │
├────────────────┤
│    FOOTER      │
└────────────────┘
```

3. Use `grid-template-areas` para definir o layout
4. Dentro do "Conteúdo Principal", crie um **grid de cards** com `auto-fit` e `minmax` (sem media query para os cards!)
5. Crie pelo menos 6 cards com título, texto e botão

### ✅ Resultado esperado:
- Layout responsivo em 3 tamanhos (mobile, tablet, desktop)
- Grid de cards que se adapta automaticamente

---

## Exercício 4: Animações e Transições

**Objetivo:** Criar micro-interações e animações que melhoram a UX.

### Tarefas:

1. Crie `exercicio-css-04/index.html` e `style.css`
2. Implemente:

**a) Botão com hover animado:**
- Background com gradiente que se move no hover
- Sombra que aparece suavemente
- Efeito de "press" no `:active` (scale down)

**b) Card com animação de entrada:**
- Cards que aparecem com `fadeInUp` quando a página carrega
- Delay escalonado (card 1: 0.1s, card 2: 0.2s, card 3: 0.3s)

**c) Loading spinner:**
- Círculo girando (animation: rotate infinite)
- Barra de progresso animada

**d) Menu hamburguer:**
- 3 linhas que viram um X quando clicado (use checkbox hack)
- Transições suaves nas linhas

**e) Tooltip:**
- Texto que aparece com fade no hover
- Seta apontando para o elemento

**f) Underline animado em links:**
- Linha que cresce da esquerda para a direita no hover (usando `::after` + `scaleX`)

3. Respeite `prefers-reduced-motion`

### ✅ Resultado esperado:
- 6 animações/transições funcionais
- Performance ok (anima apenas transform e opacity)

---

## Exercício 5: Tema Dark/Light

**Objetivo:** Implementar um sistema de temas com variáveis CSS.

### Tarefas:

1. Crie `exercicio-css-05/index.html`, `style.css` e `theme.js`
2. Crie um Design System com variáveis CSS:
   - Cores (primary, secondary, bg, surface, text, muted, border)
   - Tipografia (font-family, sizes)
   - Espaçamento (4px, 8px, 16px, 24px, 32px, 48px)
   - Bordas e sombras
3. Implemente dois temas completos:
   - **Light**: fundo branco, texto escuro
   - **Dark**: fundo escuro, texto claro
4. Crie uma página com:
   - Toggle de tema (botão sol/lua)
   - Navbar, cards, formulário, footer
   - Todos os componentes devem usar variáveis (zero cor hardcoded)
5. O tema deve ser salvo no `localStorage`
6. Respeite `prefers-color-scheme` como tema inicial

**theme.js (básico):**
```javascript
const toggle = document.getElementById('theme-toggle');
const html = document.documentElement;

// Carregar tema salvo ou usar preferência do sistema
const savedTheme = localStorage.getItem('theme');
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
html.dataset.theme = savedTheme || (prefersDark ? 'dark' : 'light');

toggle.addEventListener('click', () => {
  const newTheme = html.dataset.theme === 'dark' ? 'light' : 'dark';
  html.dataset.theme = newTheme;
  localStorage.setItem('theme', newTheme);
});
```

### ✅ Resultado esperado:
- Toggle funcional entre dark e light
- Tema persiste ao recarregar a página
- Transição suave entre temas

---

## 🏆 Desafio Final: Estilizar o Currículo

**Este é o projeto principal da semana!**

### Tarefas:

1. Pegue o HTML semântico do currículo que você criou no exercício final de HTML (ou crie uma cópia)
2. Crie um `style.css` completo aplicando TUDO que aprendeu:

**Requisitos obrigatórios:**
- [ ] CSS Reset/Normalize
- [ ] Variáveis CSS (cores, fontes, espaçamento, sombras)
- [ ] Layout com CSS Grid (estrutura da página)
- [ ] Componentes com Flexbox (cards de habilidades, contato, etc.)
- [ ] Nomenclatura BEM
- [ ] Mobile-first com 3 breakpoints (mobile, tablet, desktop)
- [ ] Tema dark/light com toggle
- [ ] Tipografia com Google Fonts (Inter ou similar)
- [ ] Animações de entrada (fadeInUp nos sections)
- [ ] Transições no hover (cards, links, botões)
- [ ] Focus styles para acessibilidade
- [ ] `prefers-reduced-motion` respeitado
- [ ] Impressão (media print) com cores e layout adequados
- [ ] Loading spinner enquanto a página carrega (opcional)

**Inspiração visual:**
- Cores vibrantes com gradientes sutis
- Sombras e elevação
- Bordas arredondadas
- Espaçamento generoso
- Design moderno e profissional

3. Teste no Lighthouse:
   - Performance: meta 90+
   - Accessibility: meta 90+
   - Best Practices: meta 90+

4. Publique no GitHub Pages

**Tempo estimado:** 6-8 horas

### ✅ Resultado esperado:
- Currículo visualmente impressionante
- Responsivo em todos os tamanhos
- Dark/light mode
- Publicado no GitHub Pages
- Scores altos no Lighthouse

---

## 📝 Anotações Pessoais

*Use este espaço para anotar suas dúvidas, descobertas e aprendizados:*

```
[Suas anotações aqui]
```
