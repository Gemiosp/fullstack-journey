# 📖 Semana 3 — HTML5 Avançado: Semântica, Acessibilidade e SEO

> *"HTML não é só sobre fazer funcionar. É sobre fazer da forma certa."*

## 📋 Índice

1. [HTML Semântico — Por que Importa?](#1-html-semântico--por-que-importa)
2. [Elementos Estruturais do HTML5](#2-elementos-estruturais-do-html5)
3. [Elementos de Texto e Conteúdo](#3-elementos-de-texto-e-conteúdo)
4. [Formulários Avançados](#4-formulários-avançados)
5. [Acessibilidade (A11y)](#5-acessibilidade-a11y)
6. [SEO On-Page](#6-seo-on-page)
7. [Meta Tags e Open Graph](#7-meta-tags-e-open-graph)
8. [Multimídia](#8-multimídia)
9. [Boas Práticas](#9-boas-práticas)
10. [Exercícios Práticos](#10-exercícios-práticos)

---

## 1. HTML Semântico — Por que Importa?

### O que é HTML Semântico?

É usar as **tags corretas para o significado correto** do conteúdo, não apenas para a aparência visual.

```html
<!-- ❌ NÃO semântico — tudo com div -->
<div class="header">
  <div class="nav">
    <div class="nav-item">Home</div>
  </div>
</div>
<div class="main">
  <div class="article">
    <div class="title">Meu Post</div>
    <div class="text">Conteúdo...</div>
  </div>
</div>
<div class="footer">Rodapé</div>

<!-- ✅ SEMÂNTICO — cada tag tem significado -->
<header>
  <nav>
    <a href="/">Home</a>
  </nav>
</header>
<main>
  <article>
    <h1>Meu Post</h1>
    <p>Conteúdo...</p>
  </article>
</main>
<footer>Rodapé</footer>
```

### Por que usar HTML semântico?

| Benefício | Explicação |
|-----------|-----------|
| **Acessibilidade** | Leitores de tela entendem a estrutura da página |
| **SEO** | Google entende melhor o conteúdo e ranqueia melhor |
| **Manutenibilidade** | Código mais legível para outros desenvolvedores |
| **Consistência** | Comportamento padrão entre navegadores |

---

## 2. Elementos Estruturais do HTML5

### 2.1 Esqueleto de uma Página

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Descrição da página para SEO">
  <title>Título da Página</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header>
    <!-- Cabeçalho do site: logo, navegação principal -->
    <nav>...</nav>
  </header>

  <main>
    <!-- Conteúdo principal — ÚNICO por página -->

    <article>
      <!-- Conteúdo independente: post de blog, notícia, produto -->
    </article>

    <section>
      <!-- Agrupamento temático de conteúdo -->
    </section>

    <aside>
      <!-- Conteúdo relacionado: sidebar, links, anúncios -->
    </aside>
  </main>

  <footer>
    <!-- Rodapé: copyright, links, contato -->
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

### 2.2 Cada Elemento em Detalhe

#### `<header>` — Cabeçalho

Pode ser usado no topo da página OU dentro de `<article>` e `<section>`.

```html
<!-- Header do site -->
<header>
  <img src="logo.png" alt="Logo da empresa">
  <nav>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/sobre">Sobre</a></li>
      <li><a href="/contato">Contato</a></li>
    </ul>
  </nav>
</header>

<!-- Header de um artigo -->
<article>
  <header>
    <h2>Título do Artigo</h2>
    <time datetime="2026-08-17">17 de Agosto de 2026</time>
    <span>Por Gabriel Barros</span>
  </header>
  <p>Conteúdo do artigo...</p>
</article>
```

#### `<nav>` — Navegação

Use para blocos de **navegação principal**. Não precisa usar para todo link da página.

```html
<nav aria-label="Navegação principal">
  <ul>
    <li><a href="/" aria-current="page">Home</a></li>
    <li><a href="/produtos">Produtos</a></li>
    <li><a href="/blog">Blog</a></li>
    <li><a href="/contato">Contato</a></li>
  </ul>
</nav>

<!-- Breadcrumbs (navegação secundária) -->
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/blog">Blog</a></li>
    <li aria-current="page">Artigo Atual</li>
  </ol>
</nav>
```

#### `<main>` — Conteúdo Principal

- **Apenas UM por página**
- Deve conter o conteúdo único da página
- Exclui sidebar, header e footer globais

```html
<body>
  <header>...</header>

  <main>
    <!-- Todo o conteúdo principal fica aqui -->
    <h1>Bem-vindo ao Meu Site</h1>
    <p>Este é o conteúdo principal.</p>
  </main>

  <footer>...</footer>
</body>
```

#### `<article>` — Conteúdo Independente

Conteúdo que faz sentido sozinho, fora do contexto da página:

```html
<!-- Post de blog -->
<article>
  <header>
    <h2>Como Aprender Git em 2026</h2>
    <time datetime="2026-08-17">17/08/2026</time>
  </header>
  <p>Git é uma ferramenta essencial...</p>
  <footer>
    <p>Tags: <a href="/tag/git">Git</a>, <a href="/tag/dev">Desenvolvimento</a></p>
  </footer>
</article>

<!-- Card de produto -->
<article>
  <img src="produto.jpg" alt="Notebook Dell XPS 15">
  <h3>Notebook Dell XPS 15</h3>
  <p>O melhor notebook para desenvolvedores.</p>
  <p><strong>R$ 8.999,00</strong></p>
  <button>Adicionar ao Carrinho</button>
</article>

<!-- Comentário de usuário -->
<article>
  <header>
    <img src="avatar.jpg" alt="Foto de Maria">
    <strong>Maria Silva</strong>
    <time datetime="2026-08-17T10:30:00">Hoje às 10:30</time>
  </header>
  <p>Excelente artigo! Muito didático.</p>
</article>
```

#### `<section>` — Seção Temática

Agrupa conteúdo com um tema comum. **Deve ter um heading** (`<h2>`, `<h3>`, etc.).

```html
<main>
  <section>
    <h2>Nossos Serviços</h2>
    <div class="services-grid">
      <article>...</article>
      <article>...</article>
    </div>
  </section>

  <section>
    <h2>Depoimentos</h2>
    <article>...</article>
    <article>...</article>
  </section>
</main>
```

**Quando usar `<section>` vs `<div>`?**
- `<section>`: conteúdo **temático** que merece um heading
- `<div>`: agrupamento **visual/layout** sem significado semântico

#### `<aside>` — Conteúdo Lateral/Complementar

```html
<main>
  <article>
    <h1>Artigo Principal</h1>
    <p>Conteúdo do artigo...</p>
  </article>

  <aside>
    <h2>Artigos Relacionados</h2>
    <ul>
      <li><a href="/post-2">Outro Post</a></li>
      <li><a href="/post-3">Mais um Post</a></li>
    </ul>

    <h2>Newsletter</h2>
    <form>
      <input type="email" placeholder="Seu email">
      <button>Inscrever</button>
    </form>
  </aside>
</main>
```

#### `<footer>` — Rodapé

```html
<footer>
  <div class="footer-grid">
    <div>
      <h3>Links Rápidos</h3>
      <ul>
        <li><a href="/sobre">Sobre</a></li>
        <li><a href="/contato">Contato</a></li>
        <li><a href="/privacidade">Política de Privacidade</a></li>
      </ul>
    </div>
    <div>
      <h3>Redes Sociais</h3>
      <ul>
        <li><a href="https://github.com/Gemiosp">GitHub</a></li>
        <li><a href="https://linkedin.com/in/gabriel-barros-b1821321b">LinkedIn</a></li>
      </ul>
    </div>
  </div>
  <p>&copy; 2026 Gabriel Barros da Silva. Todos os direitos reservados.</p>
</footer>
```

---

## 3. Elementos de Texto e Conteúdo

### 3.1 Hierarquia de Headings

```html
<!-- ✅ Correto: hierarquia lógica -->
<h1>Título Principal da Página</h1>         <!-- 1 por página -->
  <h2>Seção 1</h2>
    <h3>Subseção 1.1</h3>
    <h3>Subseção 1.2</h3>
  <h2>Seção 2</h2>
    <h3>Subseção 2.1</h3>
      <h4>Detalhe 2.1.1</h4>

<!-- ❌ Errado: pular níveis -->
<h1>Título</h1>
<h4>Subtítulo</h4>    <!-- Pulou h2 e h3! -->
```

### 3.2 Elementos de Texto Semânticos

```html
<!-- Ênfase (itálico com significado) -->
<p>Isso é <em>muito importante</em> para entender.</p>

<!-- Importância forte (negrito com significado) -->
<p><strong>Atenção:</strong> não esqueça de salvar.</p>

<!-- Abreviação -->
<p>Usamos <abbr title="Hypertext Markup Language">HTML</abbr> para estruturar páginas.</p>

<!-- Citação em bloco -->
<blockquote cite="https://example.com">
  <p>"A simplicidade é o último grau de sofisticação."</p>
  <footer>— <cite>Leonardo da Vinci</cite></footer>
</blockquote>

<!-- Citação inline -->
<p>Como dizia Steve Jobs: <q>Stay hungry, stay foolish.</q></p>

<!-- Código -->
<p>Use o comando <code>git push</code> para enviar.</p>

<!-- Bloco de código -->
<pre><code>
function hello() {
  console.log("Hello, World!");
}
</code></pre>

<!-- Data e hora -->
<p>Publicado em <time datetime="2026-08-17">17 de agosto de 2026</time>.</p>

<!-- Texto marcado/destacado -->
<p>O resultado da busca: <mark>JavaScript</mark> é essencial.</p>

<!-- Texto deletado e inserido -->
<p>O preço é <del>R$ 99,00</del> <ins>R$ 79,00</ins>.</p>

<!-- Detalhes e resumo (accordion nativo!) -->
<details>
  <summary>Clique para ver mais detalhes</summary>
  <p>Este conteúdo fica escondido até o usuário clicar.</p>
  <p>Funciona sem JavaScript!</p>
</details>

<!-- Progresso -->
<label for="progresso">Progresso do curso:</label>
<progress id="progresso" value="30" max="100">30%</progress>

<!-- Medidor (range com zonas) -->
<label for="nota">Nota:</label>
<meter id="nota" value="0.8" min="0" max="1" low="0.3" high="0.7" optimum="1">80%</meter>
```

### 3.3 Listas

```html
<!-- Lista ordenada com tipo personalizado -->
<ol type="a" start="3">
  <li>Item c</li>
  <li>Item d</li>
</ol>

<!-- Lista de definições (ótimo para glossários, FAQ) -->
<dl>
  <dt>HTML</dt>
  <dd>Linguagem de marcação para estruturar páginas web.</dd>

  <dt>CSS</dt>
  <dd>Linguagem de estilo para definir a aparência visual.</dd>

  <dt>JavaScript</dt>
  <dd>Linguagem de programação para interatividade.</dd>
</dl>
```

### 3.4 Tabelas Semânticas

```html
<table>
  <caption>Vendas do Trimestre — 2026</caption>

  <thead>
    <tr>
      <th scope="col">Produto</th>
      <th scope="col">Q1</th>
      <th scope="col">Q2</th>
      <th scope="col">Q3</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <th scope="row">Notebooks</th>
      <td>150</td>
      <td>200</td>
      <td>180</td>
    </tr>
    <tr>
      <th scope="row">Monitores</th>
      <td>80</td>
      <td>120</td>
      <td>95</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td>230</td>
      <td>320</td>
      <td>275</td>
    </tr>
  </tfoot>
</table>
```

---

## 4. Formulários Avançados

### 4.1 Estrutura de Formulário

```html
<form action="/api/cadastro" method="POST" novalidate>

  <!-- Agrupamento com fieldset e legend -->
  <fieldset>
    <legend>Dados Pessoais</legend>

    <div>
      <label for="nome">Nome completo *</label>
      <input
        type="text"
        id="nome"
        name="nome"
        required
        minlength="3"
        maxlength="100"
        placeholder="Ex: Gabriel Barros"
        autocomplete="name"
      >
    </div>

    <div>
      <label for="email">Email *</label>
      <input
        type="email"
        id="email"
        name="email"
        required
        placeholder="seu@email.com"
        autocomplete="email"
      >
    </div>

    <div>
      <label for="telefone">Telefone</label>
      <input
        type="tel"
        id="telefone"
        name="telefone"
        pattern="\([0-9]{2}\)\s[0-9]{4,5}-[0-9]{4}"
        placeholder="(32) 99959-1116"
        autocomplete="tel"
      >
    </div>

    <div>
      <label for="nascimento">Data de Nascimento</label>
      <input
        type="date"
        id="nascimento"
        name="nascimento"
        min="1950-01-01"
        max="2010-12-31"
      >
    </div>
  </fieldset>

  <fieldset>
    <legend>Endereço</legend>

    <div>
      <label for="cep">CEP</label>
      <input type="text" id="cep" name="cep" pattern="[0-9]{5}-[0-9]{3}" placeholder="36520-000">
    </div>

    <div>
      <label for="estado">Estado</label>
      <select id="estado" name="estado">
        <option value="">Selecione...</option>
        <optgroup label="Sudeste">
          <option value="MG">Minas Gerais</option>
          <option value="SP">São Paulo</option>
          <option value="RJ">Rio de Janeiro</option>
          <option value="ES">Espírito Santo</option>
        </optgroup>
        <optgroup label="Sul">
          <option value="PR">Paraná</option>
          <option value="SC">Santa Catarina</option>
          <option value="RS">Rio Grande do Sul</option>
        </optgroup>
      </select>
    </div>
  </fieldset>

  <fieldset>
    <legend>Preferências</legend>

    <!-- Checkboxes -->
    <p>Áreas de interesse:</p>
    <label><input type="checkbox" name="interesse" value="frontend"> Frontend</label>
    <label><input type="checkbox" name="interesse" value="backend"> Backend</label>
    <label><input type="checkbox" name="interesse" value="devops"> DevOps</label>

    <!-- Radio buttons -->
    <p>Nível de experiência:</p>
    <label><input type="radio" name="nivel" value="junior" required> Júnior</label>
    <label><input type="radio" name="nivel" value="pleno"> Pleno</label>
    <label><input type="radio" name="nivel" value="senior"> Sênior</label>

    <!-- Range slider -->
    <div>
      <label for="horas">Horas de estudo por dia: <output id="horas-output">4</output></label>
      <input type="range" id="horas" name="horas" min="1" max="12" value="4"
             oninput="document.getElementById('horas-output').value = this.value">
    </div>

    <!-- Textarea -->
    <div>
      <label for="bio">Sobre você</label>
      <textarea id="bio" name="bio" rows="4" maxlength="500" placeholder="Conte um pouco sobre você..."></textarea>
    </div>
  </fieldset>

  <button type="submit">Enviar Cadastro</button>
  <button type="reset">Limpar</button>
</form>
```

### 4.2 Tipos de Input do HTML5

| Tipo | Para quê | Exemplo |
|------|---------|---------|
| `text` | Texto genérico | Nome, cidade |
| `email` | Email (valida formato) | user@email.com |
| `password` | Senha (oculta) | ●●●●●● |
| `tel` | Telefone (teclado numérico no mobile) | (32) 9999-1234 |
| `url` | URL (valida formato) | https://... |
| `number` | Número (com setas) | Idade, quantidade |
| `range` | Slider | Volume, progresso |
| `date` | Data (com calendário) | 2026-08-17 |
| `time` | Hora | 14:30 |
| `datetime-local` | Data + hora | 2026-08-17T14:30 |
| `month` | Mês/ano | 2026-08 |
| `week` | Semana do ano | 2026-W33 |
| `color` | Seletor de cor | #ff6600 |
| `file` | Upload de arquivo | Imagens, PDFs |
| `search` | Campo de busca | Com ícone de limpar |
| `hidden` | Dados ocultos | IDs, tokens |

### 4.3 Validação Nativa

```html
<!-- Atributos de validação -->
<input required>                          <!-- Campo obrigatório -->
<input minlength="3" maxlength="50">     <!-- Tamanho do texto -->
<input min="1" max="100">                <!-- Valor numérico -->
<input pattern="[A-Za-z]{3,}">           <!-- Expressão regular -->
<input type="email">                      <!-- Validação de email automática -->
<input type="url">                        <!-- Validação de URL automática -->

<!-- Mensagem de erro personalizada -->
<input type="text" required
  oninvalid="this.setCustomValidity('Por favor, preencha este campo!')"
  oninput="this.setCustomValidity('')"
>
```

### 4.4 Datalist (Autocomplete)

```html
<label for="linguagem">Linguagem favorita:</label>
<input list="linguagens" id="linguagem" name="linguagem">

<datalist id="linguagens">
  <option value="JavaScript">
  <option value="TypeScript">
  <option value="Python">
  <option value="Java">
  <option value="C#">
  <option value="Go">
  <option value="Rust">
</datalist>
```

### 4.5 Dialog (Modal Nativo)

```html
<!-- Botão que abre o modal -->
<button onclick="document.getElementById('meuModal').showModal()">
  Abrir Modal
</button>

<!-- Modal nativo do HTML! -->
<dialog id="meuModal">
  <h2>Confirmação</h2>
  <p>Tem certeza que deseja continuar?</p>
  <form method="dialog">
    <button value="cancel">Cancelar</button>
    <button value="confirm">Confirmar</button>
  </form>
</dialog>
```

---

## 5. Acessibilidade (A11y)

> **A11y** é abreviação de "Accessibility" (a + 11 letras + y).
> Cerca de **15% da população mundial** tem alguma deficiência. Acessibilidade não é opcional.

### 5.1 ARIA (Accessible Rich Internet Applications)

ARIA adiciona informações extras para tecnologias assistivas (leitores de tela).

**Regra de ouro:** Prefira HTML semântico nativo. Use ARIA **apenas** quando o HTML nativo não for suficiente.

```html
<!-- ❌ Não faça isso — use o elemento nativo -->
<div role="button" tabindex="0" onclick="submit()">Enviar</div>

<!-- ✅ Faça isso -->
<button onclick="submit()">Enviar</button>
```

### 5.2 Atributos ARIA Essenciais

```html
<!-- aria-label: nome acessível quando não há texto visível -->
<button aria-label="Fechar menu">✕</button>
<button aria-label="Buscar"><svg>...</svg></button>

<!-- aria-labelledby: referencia outro elemento como rótulo -->
<h2 id="secao-titulo">Nossos Serviços</h2>
<section aria-labelledby="secao-titulo">
  <!-- conteúdo -->
</section>

<!-- aria-describedby: descrição adicional -->
<label for="senha">Senha</label>
<input type="password" id="senha" aria-describedby="senha-dica">
<p id="senha-dica">Mínimo 8 caracteres, incluindo números e letras.</p>

<!-- aria-hidden: esconde do leitor de tela (ícones decorativos) -->
<button>
  <span aria-hidden="true">🛒</span>
  Carrinho
</button>

<!-- aria-live: anuncia mudanças dinâmicas -->
<div aria-live="polite" id="notificacao">
  <!-- JS insere mensagens aqui e o leitor de tela anuncia -->
</div>

<!-- aria-expanded: indica estado de expansão -->
<button aria-expanded="false" aria-controls="menu-dropdown">
  Menu ▼
</button>
<ul id="menu-dropdown" hidden>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<!-- aria-current: indica item atual em navegação -->
<nav>
  <a href="/" aria-current="page">Home</a>
  <a href="/sobre">Sobre</a>
</nav>

<!-- role: define o papel do elemento (quando não há tag nativa) -->
<div role="alert">Erro: campo obrigatório!</div>
<div role="status">Carregando...</div>
<div role="tabpanel">Conteúdo da aba</div>
```

### 5.3 Checklist de Acessibilidade

```html
<!-- 1. Toda imagem tem alt -->
<img src="foto.jpg" alt="Gabriel programando em seu notebook">
<img src="decoracao.png" alt="">  <!-- alt vazio para imagens decorativas -->

<!-- 2. Links têm texto descritivo -->
<!-- ❌ --> <a href="/artigo">Clique aqui</a>
<!-- ✅ --> <a href="/artigo">Leia o artigo sobre Git</a>

<!-- 3. Formulários têm labels -->
<!-- ❌ --> <input type="text" placeholder="Nome">
<!-- ✅ --> <label for="nome">Nome</label>
           <input type="text" id="nome">

<!-- 4. Contraste de cores suficiente -->
<!-- Use: https://webaim.org/resources/contrastchecker/ -->

<!-- 5. Navegação por teclado funciona -->
<!-- Tab, Shift+Tab, Enter, Escape, Setas -->

<!-- 6. Focus visível -->
<style>
  :focus-visible {
    outline: 3px solid #06b6d4;
    outline-offset: 2px;
  }
</style>

<!-- 7. Skip link (pular para conteúdo) -->
<a href="#main-content" class="skip-link">Pular para o conteúdo principal</a>
<!-- ... header, nav ... -->
<main id="main-content">...</main>

<!-- 8. Idioma definido -->
<html lang="pt-BR">
```

### 5.4 Testando Acessibilidade

| Ferramenta | O que faz | Link |
|-----------|-----------|------|
| **Lighthouse** | Audit integrado no Chrome DevTools | F12 → Lighthouse |
| **axe DevTools** | Extensão Chrome para testes | [axe](https://www.deque.com/axe/devtools/) |
| **WAVE** | Avaliador online | [wave.webaim.org](https://wave.webaim.org/) |
| **NVDA** | Leitor de tela gratuito (Windows) | [nvda.org](https://www.nvaccess.org/) |
| **Teclado** | Navegar só com Tab/Enter | Teste você mesmo! |

---

## 6. SEO On-Page

### 6.1 O que é SEO?

**SEO** (Search Engine Optimization) é otimizar seu site para aparecer melhor nos resultados de busca do Google.

### 6.2 Estrutura HTML para SEO

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <!-- 1. Charset e viewport (básico) -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 2. Título (até 60 caracteres) — MAIS IMPORTANTE para SEO -->
  <title>Aprenda Git em 2026 — Guia Completo para Iniciantes | Gabriel Dev</title>

  <!-- 3. Descrição (até 160 caracteres) — aparece no Google -->
  <meta name="description" content="Guia completo de Git para iniciantes. Aprenda comandos, branches, GitHub e boas práticas em 2026. Tutorial gratuito em português.">

  <!-- 4. Canonical (evita conteúdo duplicado) -->
  <link rel="canonical" href="https://meusite.com/blog/aprenda-git">

  <!-- 5. Favicon -->
  <link rel="icon" type="image/png" href="/favicon.png">

  <!-- 6. Robots (indexação) -->
  <meta name="robots" content="index, follow">
</head>
<body>

  <!-- 7. Um ÚNICO h1 por página -->
  <h1>Como Aprender Git em 2026: Guia Completo</h1>

  <!-- 8. Hierarquia de headings correta -->
  <h2>...</h2>
    <h3>...</h3>

  <!-- 9. Imagens otimizadas -->
  <img
    src="git-workflow.webp"
    alt="Diagrama mostrando o fluxo de trabalho do Git com working directory, staging area e repository"
    width="800"
    height="450"
    loading="lazy"
  >

  <!-- 10. Links internos com texto descritivo -->
  <a href="/blog/github-actions">Aprenda GitHub Actions neste tutorial</a>

</body>
</html>
```

### 6.3 Checklist SEO

- [ ] Um `<h1>` por página, descritivo e com palavra-chave
- [ ] `<title>` único e atrativo (até 60 caracteres)
- [ ] `<meta name="description">` convincente (até 160 caracteres)
- [ ] Hierarquia de headings lógica (h1 → h2 → h3)
- [ ] Todas as imagens com `alt` descritivo
- [ ] URLs amigáveis (`/blog/aprenda-git` em vez de `/post?id=123`)
- [ ] Links internos entre páginas do site
- [ ] `loading="lazy"` em imagens abaixo da dobra
- [ ] Atributos `width` e `height` nas imagens (evita layout shift)
- [ ] Site responsivo (mobile-first)
- [ ] HTTPS ativado
- [ ] Velocidade de carregamento otimizada

---

## 7. Meta Tags e Open Graph

### 7.1 Meta Tags Essenciais

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Descrição da página">
  <meta name="author" content="Gabriel Barros da Silva">
  <meta name="theme-color" content="#06b6d4">

  <!-- Controle de cache -->
  <meta http-equiv="Cache-Control" content="no-cache">
</head>
```

### 7.2 Open Graph (compartilhamento em redes sociais)

Quando alguém compartilha seu link no WhatsApp, LinkedIn ou Twitter, essas tags definem como ele aparece:

```html
<head>
  <!-- Open Graph (Facebook, WhatsApp, LinkedIn) -->
  <meta property="og:title" content="Como Aprender Git em 2026">
  <meta property="og:description" content="Guia completo e gratuito de Git para iniciantes.">
  <meta property="og:image" content="https://meusite.com/images/git-guide-cover.jpg">
  <meta property="og:url" content="https://meusite.com/blog/aprenda-git">
  <meta property="og:type" content="article">
  <meta property="og:locale" content="pt_BR">
  <meta property="og:site_name" content="Gabriel Dev Blog">

  <!-- Twitter Cards -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Como Aprender Git em 2026">
  <meta name="twitter:description" content="Guia completo e gratuito de Git para iniciantes.">
  <meta name="twitter:image" content="https://meusite.com/images/git-guide-cover.jpg">
</head>
```

---

## 8. Multimídia

### 8.1 Imagens Responsivas

```html
<!-- Imagem básica com lazy loading -->
<img
  src="foto.jpg"
  alt="Descrição da imagem"
  width="800"
  height="600"
  loading="lazy"
  decoding="async"
>

<!-- Imagens responsivas com srcset (tamanhos diferentes) -->
<img
  src="foto-800.jpg"
  srcset="
    foto-400.jpg 400w,
    foto-800.jpg 800w,
    foto-1200.jpg 1200w
  "
  sizes="
    (max-width: 600px) 400px,
    (max-width: 1000px) 800px,
    1200px
  "
  alt="Paisagem de Ouro Preto"
>

<!-- Picture: formatos diferentes para cada navegador -->
<picture>
  <source srcset="foto.avif" type="image/avif">
  <source srcset="foto.webp" type="image/webp">
  <img src="foto.jpg" alt="Descrição">
</picture>

<!-- Figure com caption -->
<figure>
  <img src="diagrama.png" alt="Diagrama de arquitetura do sistema">
  <figcaption>Figura 1: Arquitetura do sistema mostrando frontend, backend e banco de dados.</figcaption>
</figure>
```

### 8.2 Vídeo e Áudio

```html
<!-- Vídeo nativo -->
<video
  controls
  width="720"
  height="480"
  poster="thumbnail.jpg"
  preload="metadata"
>
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
  <p>Seu navegador não suporta vídeo HTML5.
     <a href="video.mp4">Baixe o vídeo</a>.
  </p>
</video>

<!-- Áudio -->
<audio controls preload="metadata">
  <source src="podcast.ogg" type="audio/ogg">
  <source src="podcast.mp3" type="audio/mpeg">
  <p>Seu navegador não suporta áudio HTML5.</p>
</audio>

<!-- YouTube embed (iframe) -->
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="Título do vídeo para acessibilidade"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope"
  allowfullscreen
  loading="lazy"
></iframe>
```

---

## 9. Boas Práticas

### 9.1 Regras de Ouro

1. **Use HTML semântico** — a tag certa para o conteúdo certo
2. **Um `<h1>` por página** — descreva o conteúdo principal
3. **Alt em toda imagem** — vazio (`alt=""`) se decorativa
4. **Label em todo input** — nunca apenas placeholder
5. **Não use divs para tudo** — `<nav>`, `<main>`, `<section>` existem
6. **Teste com teclado** — navegue sem mouse
7. **Valide seu HTML** — use o [W3C Validator](https://validator.w3.org/)

### 9.2 Performance

```html
<!-- CSS no <head> (carrega antes) -->
<link rel="stylesheet" href="style.css">

<!-- JS no final do <body> (não bloqueia renderização) -->
<script src="script.js"></script>

<!-- OU use defer (baixa em paralelo, executa após HTML) -->
<script src="script.js" defer></script>

<!-- async (baixa em paralelo, executa quando pronto - para analytics) -->
<script src="analytics.js" async></script>

<!-- Preload de recursos críticos -->
<link rel="preload" href="fonte.woff2" as="font" type="font/woff2" crossorigin>
<link rel="preload" href="hero.webp" as="image">

<!-- Preconnect para domínios externos -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- DNS prefetch -->
<link rel="dns-prefetch" href="https://api.example.com">
```

---

## 10. Exercícios Práticos

Veja os exercícios na pasta `exercicios/` desta seção.

---

## 📚 Recursos

| Recurso | Tipo | Link |
|---------|------|------|
| MDN HTML | Referência | [developer.mozilla.org](https://developer.mozilla.org/pt-BR/docs/Web/HTML) |
| web.dev Learn HTML | Curso | [web.dev/learn/html](https://web.dev/learn/html) |
| HTML5 Doctor | Referência | [html5doctor.com](http://html5doctor.com) |
| W3C Validator | Ferramenta | [validator.w3.org](https://validator.w3.org/) |
| A11y Project | Checklist | [a11yproject.com](https://www.a11yproject.com/checklist/) |
| Can I Use | Compatibilidade | [caniuse.com](https://caniuse.com) |

---

## ✅ Checklist da Semana

- [ ] Sabe a diferença entre `<section>`, `<article>`, `<aside>` e `<div>`
- [ ] Usa hierarquia de headings correta (h1 → h2 → h3)
- [ ] Cria formulários com validação nativa HTML5
- [ ] Entende e usa atributos ARIA básicos
- [ ] Sabe o que são meta tags e Open Graph
- [ ] Imagens com `alt`, `loading="lazy"`, `width` e `height`
- [ ] Testou acessibilidade com Lighthouse e teclado
- [ ] Validou HTML no W3C Validator
- [ ] Completou todos os exercícios práticos
