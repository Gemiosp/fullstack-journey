# 🏋️ Exercícios Práticos — HTML5 Avançado

> Complete cada exercício na ordem. Ao final, você terá construído um site completo com HTML semântico perfeito.

---

## Exercício 1: Estrutura Semântica Completa

**Objetivo:** Criar a estrutura de uma página de blog usando apenas tags semânticas corretas.

### Tarefas:

1. Crie uma pasta `exercicio-html-01` dentro de `exercicios/`
2. Crie o arquivo `index.html` com a seguinte estrutura:
   - `<header>` com logo (texto), `<nav>` com 4 links (Home, Blog, Sobre, Contato)
   - `<main>` contendo:
     - `<section>` "Posts Recentes" com 3 `<article>` (cada um com `<header>`, parágrafo, `<footer>` com tags e data)
     - `<aside>` com "Posts Populares" (lista de links) e "Newsletter" (formulário com email e botão)
   - `<footer>` com copyright, links rápidos e redes sociais

3. Regras:
   - **Zero** `<div>` para estrutura (use tags semânticas)
   - Um único `<h1>` na página
   - Hierarquia de headings correta (h1 → h2 → h3)
   - Use `<time datetime="...">` para todas as datas
   - Use `<a>` com `aria-current="page"` para o link ativo

### ✅ Resultado esperado:
- Página que valida sem erros no [W3C Validator](https://validator.w3.org/)
- Estrutura semântica que faz sentido lida por um leitor de tela

---

## Exercício 2: Formulário Completo com Validação

**Objetivo:** Criar um formulário de cadastro profissional usando validação HTML5 nativa.

### Tarefas:

1. Crie `exercicio-html-02/cadastro.html`
2. O formulário deve ter 3 `<fieldset>`:

**Fieldset 1 — Dados Pessoais:**
- Nome completo (obrigatório, mín. 3 caracteres)
- Email (obrigatório, tipo email)
- Telefone (padrão regex para formato brasileiro)
- Data de nascimento (min: 1950, max: 2010)
- CPF (campo texto com padrão `\d{3}\.\d{3}\.\d{3}-\d{2}`)

**Fieldset 2 — Profissional:**
- Cargo desejado (select com optgroups: Frontend, Backend, Full Stack, DevOps)
- Nível (radio: Júnior, Pleno, Sênior)
- Tecnologias (checkboxes: HTML, CSS, JavaScript, React, Node.js, Python)
- Anos de experiência (input number, min 0, max 30)
- Pretensão salarial (range slider de R$2.000 a R$30.000, com `<output>` mostrando valor)
- LinkedIn (input url)

**Fieldset 3 — Complementar:**
- Linguagem favorita (input com `<datalist>` com 8 opções)
- Sobre você (textarea, max 500 caracteres)
- Upload de currículo (input file, aceitar apenas .pdf)
- Aceito os termos (checkbox obrigatório)

3. Use `<label>` para TODOS os campos
4. Adicione `autocomplete` nos campos relevantes
5. Use `placeholder` como exemplo, não como label

### ✅ Resultado esperado:
- Formulário que não permite envio se campos obrigatórios estiverem vazios
- Validação visual nativa do navegador (bordas vermelhas)
- Slider mostra valor em tempo real

---

## Exercício 3: Acessibilidade na Prática

**Objetivo:** Pegar uma página com problemas de acessibilidade e corrigir todos.

### Tarefas:

1. Crie `exercicio-html-03/antes.html` com o código ERRADO abaixo:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Site</title>
</head>
<body>
  <div class="header">
    <div class="logo">MeuSite</div>
    <div class="nav">
      <div onclick="location.href='/'">Home</div>
      <div onclick="location.href='/sobre'">Sobre</div>
      <div onclick="location.href='/contato'">Contato</div>
    </div>
  </div>

  <div class="main">
    <div class="title">Bem-vindo ao Meu Site</div>
    <img src="hero.jpg">
    <div class="text">Este é um site incrível com muito conteúdo legal.</div>

    <div class="card">
      <img src="post1.jpg">
      <div class="card-title">Post Importante</div>
      <div>Publicado em 17/08/2026</div>
      <div class="btn" onclick="alert('ler')">Clique aqui</div>
    </div>

    <div class="form">
      <input type="text" placeholder="Seu nome">
      <input placeholder="email@email.com">
      <div class="btn" onclick="submit()">Enviar</div>
    </div>
  </div>

  <div class="footer">
    <div>© 2026</div>
  </div>
</body>
</html>
```

2. Crie `exercicio-html-03/depois.html` corrigindo TODOS os problemas:
   - Adicione `lang="pt-BR"`
   - Substitua `<div>` por tags semânticas corretas
   - Adicione `alt` em todas as imagens
   - Substitua `<div onclick>` por `<a>` ou `<button>`
   - Adicione `<label>` nos inputs
   - Use `<time>` para a data
   - Adicione skip link
   - Adicione `aria-label` onde necessário
   - Adicione `<meta name="description">`
   - Use hierarquia de headings correta

3. Liste todas as correções feitas em um comentário HTML no topo do arquivo `depois.html`

### ✅ Resultado esperado:
- `antes.html`: Lighthouse Accessibility score baixo
- `depois.html`: Lighthouse Accessibility score 90+
- Documento com lista de todas as correções

---

## Exercício 4: SEO e Meta Tags

**Objetivo:** Criar uma página de artigo otimizada para SEO e compartilhamento em redes sociais.

### Tarefas:

1. Crie `exercicio-html-04/artigo.html`
2. O artigo deve ser: **"Como Aprender Programação em 2026: Guia Completo"**
3. Inclua no `<head>`:
   - Title otimizado (até 60 caracteres)
   - Meta description (até 160 caracteres)
   - Canonical URL
   - Open Graph completo (og:title, og:description, og:image, og:url, og:type, og:locale)
   - Twitter Card (summary_large_image)
   - Favicon
   - Preconnect para Google Fonts
   - Theme color

4. No `<body>`, estruture o artigo com:
   - Header com nav e breadcrumbs
   - Article com header (h1, autor, data, tempo de leitura)
   - Conteúdo com 3+ seções (h2), cada uma com parágrafos
   - Imagens com alt, loading, width, height
   - Uma blockquote
   - Uma tabela comparativa
   - Lista de links relacionados
   - Footer com tags e botões de compartilhar

5. No final do `<body>`:
   - Scripts com `defer`
   - Structured data (JSON-LD) para artigo

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Como Aprender Programação em 2026",
  "author": {
    "@type": "Person",
    "name": "Gabriel Barros da Silva"
  },
  "datePublished": "2026-08-17",
  "description": "Guia completo para iniciantes...",
  "image": "https://meusite.com/images/capa.jpg"
}
</script>
```

### ✅ Resultado esperado:
- Lighthouse SEO score 100
- Links compartilhados mostram preview correto (teste em [metatags.io](https://metatags.io))

---

## Exercício 5: Tabela de Dados Acessível

**Objetivo:** Criar uma tabela semântica e acessível com dados reais.

### Tarefas:

1. Crie `exercicio-html-05/tabela.html`
2. Crie uma tabela de comparação de frameworks JavaScript:

| Framework | Linguagem | Tipo | Estrelas GitHub | Curva de Aprendizado | Ideal Para |
|-----------|-----------|------|----------------|---------------------|-----------|
| React | JavaScript/TSX | Biblioteca | 220k+ | Moderada | SPAs, Mobile |
| Next.js | JavaScript/TSX | Framework | 120k+ | Moderada-Alta | Sites, SSR |
| Vue.js | JavaScript | Framework | 210k+ | Fácil | SPAs, Iniciantes |
| Angular | TypeScript | Framework | 95k+ | Alta | Enterprise |
| Svelte | JavaScript | Compilador | 75k+ | Fácil | Performance |

3. Requisitos:
   - `<caption>` descritivo
   - `<thead>`, `<tbody>`, `<tfoot>` (com contagem total)
   - `scope="col"` e `scope="row"` nos headers
   - Estilização básica com CSS (bordas, hover, zebra stripes)
   - Responsiva: scroll horizontal no mobile

### ✅ Resultado esperado:
- Tabela legível por leitores de tela
- Responsiva em telas pequenas

---

## Exercício 6: Elementos Interativos Nativos

**Objetivo:** Usar elementos interativos do HTML5 sem JavaScript.

### Tarefas:

1. Crie `exercicio-html-06/interativo.html`
2. Implemente:
   - **FAQ com `<details>/<summary>`**: 5 perguntas frequentes sobre programação
   - **Modal com `<dialog>`**: botão "Contato" que abre um modal com formulário
   - **Barra de progresso** do seu aprendizado Full Stack usando `<progress>`
   - **Medidor** de satisfação usando `<meter>`
   - **Input com datalist** para selecionar tecnologias
   - **Color picker** para personalizar a cor do tema
   - **Range slider** com `<output>` para nota de 1 a 10

3. Adicione estilização CSS mínima para ficar apresentável

### ✅ Resultado esperado:
- Todos os elementos interativos funcionam SEM JavaScript
- Acessíveis via teclado

---

## 🏆 Desafio Final: Reconstruir seu Currículo

**Este é o projeto mais importante desta semana!**

### Tarefas:

1. Crie a pasta `exercicio-html-final/`
2. Reconstrua seu currículo profissional (o que já existe em `c:\Users\gabri\Desktop\Currículo\`) usando **todo o HTML semântico** que aprendeu:
   - Tags semânticas perfeitas (`<header>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`)
   - Hierarquia de headings correta
   - `<time>` para datas
   - `<dl>` para listas de definição (habilidades, etc.)
   - Tabela para comparações se necessário
   - Formulário de contato na parte inferior
   - Acessibilidade perfeita (ARIA, labels, alt, skip link)
   - SEO completo (title, description, Open Graph, structured data)
   - Meta tags para compartilhamento
   - Performance (preconnect, lazy loading, defer)
   - Validação W3C sem erros

3. **NÃO SE PREOCUPE com CSS bonito agora** — foque 100% no HTML semântico. O CSS será o exercício da semana seguinte.

4. Teste no Lighthouse (Chrome DevTools → Lighthouse):
   - Accessibility: meta 90+
   - SEO: meta 100
   - Best Practices: meta 90+

### ✅ Resultado esperado:
- Currículo com HTML perfeito, pronto para receber CSS na próxima semana
- Scores altos no Lighthouse
- Validação W3C sem erros

**Tempo estimado:** 3-4 horas

---

## 📝 Anotações Pessoais

*Use este espaço para anotar suas dúvidas, descobertas e aprendizados:*

```
[Suas anotações aqui]
```
