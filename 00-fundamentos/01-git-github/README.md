# 📖 Semana 1 — Git & GitHub: O Guia Completo

> *"Git é a ferramenta mais importante que um desenvolvedor usa todos os dias. Domine-a."*

## 📋 Índice

1. [O que é Git?](#1-o-que-é-git)
2. [Instalação e Configuração](#2-instalação-e-configuração)
3. [Conceitos Fundamentais](#3-conceitos-fundamentais)
4. [Comandos Essenciais](#4-comandos-essenciais)
5. [Branches](#5-branches)
6. [GitHub](#6-github)
7. [Git Avançado](#7-git-avançado)
8. [Conventional Commits](#8-conventional-commits)
9. [Git Flow](#9-git-flow)
10. [GitHub Actions (Introdução)](#10-github-actions-introdução)
11. [Exercícios Práticos](#11-exercícios-práticos)

---

## 1. O que é Git?

**Git** é um **sistema de controle de versão distribuído** (DVCS). Ele rastreia as mudanças nos seus arquivos ao longo do tempo, permitindo:

- 🔄 Voltar a qualquer versão anterior do código
- 👥 Trabalhar em equipe sem conflitos
- 🌿 Criar ramificações (branches) para trabalhar em features isoladas
- 📝 Manter um histórico completo de todas as mudanças

### Por que é essencial?

```
Sem Git:                          Com Git:
arquivo_v1.js                     projeto/
arquivo_v2.js                       ├── src/
arquivo_v2_final.js                 │   └── app.js  ← Único arquivo
arquivo_v2_final_FINAL.js           └── .git/       ← Todo o histórico
arquivo_v2_final_FINAL_v3.js              └── (centenas de versões salvas)
```

### Git vs GitHub

| Git | GitHub |
|-----|--------|
| Software instalado localmente | Plataforma online (nuvem) |
| Controla versões dos arquivos | Hospeda repositórios Git |
| Funciona offline | Adiciona colaboração, issues, PRs |
| Ferramenta de linha de comando | Interface web + API |

**Analogia:** Git é como o **Word com "Ctrl+Z" infinito**, e GitHub é como o **Google Drive** para seus repositórios Git.

---

## 2. Instalação e Configuração

### 2.1 Instalar Git

**Windows:**
1. Baixe em [git-scm.com](https://git-scm.com/download/win)
2. Execute o instalador (aceite padrões, mas escolha **VS Code como editor padrão**)
3. Verifique a instalação:

```bash
git --version
# Saída esperada: git version 2.x.x
```

### 2.2 Configuração Inicial (OBRIGATÓRIO)

```bash
# Seu nome (aparece nos commits)
git config --global user.name "Gabriel Barros da Silva"

# Seu email (mesmo do GitHub!)
git config --global user.email "gabrielbarrosdasilva9@gmail.com"

# Editor padrão
git config --global core.editor "code --wait"

# Branch padrão (main em vez de master)
git config --global init.defaultBranch main

# Habilitar cores no terminal
git config --global color.ui auto

# Configurar fim de linha (Windows)
git config --global core.autocrlf true

# Verificar todas as configurações
git config --list
```

### 2.3 Gerar chave SSH (para GitHub)

```bash
# Gerar chave SSH
ssh-keygen -t ed25519 -C "gabrielbarrosdasilva9@gmail.com"

# Iniciar o agente SSH
# NOTA: O comando abaixo ('eval') funciona no Git Bash ou Linux/Mac.
# No PowerShell do Windows, ele dará erro. Se der erro, pule para o próximo passo.
eval "$(ssh-agent -s)"

# Adicionar a chave (no Windows, às vezes não é necessário iniciar o agente manualmente)
ssh-add ~/.ssh/id_ed25519

# Copiar a chave pública (adicionar no GitHub → Settings → SSH Keys)
cat ~/.ssh/id_ed25519.pub
```

---

## 3. Conceitos Fundamentais

### 3.1 Os Três Estados do Git

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  Working Directory    Staging Area      Repository          │
│  (Diretório de       (Área de          (Histórico de       │
│   Trabalho)           Preparação)       Commits)            │
│                                                             │
│  ┌──────────┐        ┌──────────┐      ┌──────────┐        │
│  │ Arquivos │ ──────>│ Arquivos │ ────>│ Snapshot │        │
│  │ editados │ git add│ prontos  │ git  │ salvo    │        │
│  │          │        │          │commit│          │        │
│  └──────────┘        └──────────┘      └──────────┘        │
│                                                             │
│  Untracked/Modified   Staged            Committed           │
└─────────────────────────────────────────────────────────────┘
```

**Explicação simples:**
1. **Working Directory** — Onde você edita os arquivos
2. **Staging Area** — A "fila" de mudanças prontas para serem salvas
3. **Repository** — O histórico de versões (commits)

### 3.2 O que é um Commit?

Um **commit** é um **snapshot** (foto) do seu projeto em um momento específico. Cada commit tem:

- **Hash** — Identificador único (ex: `a1b2c3d`)
- **Autor** — Quem fez o commit
- **Data** — Quando foi feito
- **Mensagem** — Descrição do que mudou
- **Ponteiro para o commit anterior** — Forma uma cadeia (histórico)

```
commit a1b2c3d (HEAD -> main)
Author: Gabriel Barros <gabrielbarrosdasilva9@gmail.com>
Date:   Wed Aug 13 14:00:00 2026

    feat: adiciona página de login
```

### 3.3 HEAD

**HEAD** é um ponteiro que indica "onde você está agora" no histórico. Geralmente aponta para o último commit da branch atual.

```
main:    A ── B ── C ── D (HEAD)
```

---

## 4. Comandos Essenciais

### 4.1 Criar e Inicializar

```bash
# Criar um novo repositório
git init

# Clonar um repositório existente
git clone https://github.com/usuario/repo.git

# Clonar com SSH
git clone git@github.com:usuario/repo.git
```

### 4.2 Fluxo Básico de Trabalho

```bash
# 1. Verificar o status (quais arquivos foram modificados)
git status

# 2. Ver as diferenças (o que exatamente mudou)
git diff                    # Mudanças no working directory
git diff --staged           # Mudanças no staging area

# 3. Adicionar ao staging
git add arquivo.js          # Adicionar arquivo específico
git add .                   # Adicionar TODOS os arquivos modificados
git add -p                  # Adicionar interativamente (pedaço por pedaço)

# 4. Fazer o commit
git commit -m "feat: adiciona validação de formulário"

# 5. Ver o histórico
git log                     # Histórico completo
git log --oneline           # Resumido (uma linha por commit)
git log --graph --oneline   # Com gráfico de branches
git log -n 5                # Últimos 5 commits
```

### 4.3 Desfazer Mudanças

```bash
# Descartar mudanças no working directory (CUIDADO: irreversível!)
git checkout -- arquivo.js
git restore arquivo.js              # Comando moderno (Git 2.23+)

# Remover do staging (manter mudanças no working directory)
git reset HEAD arquivo.js
git restore --staged arquivo.js     # Comando moderno

# Desfazer o último commit (mantendo as mudanças)
git reset --soft HEAD~1

# Desfazer o último commit (descartando as mudanças - CUIDADO!)
git reset --hard HEAD~1

# Criar um novo commit que desfaz um commit anterior (seguro)
git revert <hash-do-commit>
```

### 4.4 Inspecionar

```bash
# Ver detalhes de um commit
git show <hash>

# Ver quem alterou cada linha de um arquivo
git blame arquivo.js

# Buscar no histórico
git log --grep="login"              # Buscar na mensagem
git log -S "funcao_nome"            # Buscar no código alterado
```

---

## 5. Branches

### 5.1 Conceito

Uma **branch** é uma ramificação independente do código. Permite trabalhar em features sem afetar o código principal.

```
main:     A ── B ── C ── D ── E ── F (merge)
                    \              /
feature:             X ── Y ── Z
```

### 5.2 Comandos de Branch

```bash
# Listar branches
git branch              # Locais
git branch -a           # Locais + remotas

# Criar branch
git branch nome-branch

# Mudar para branch
git checkout nome-branch
git switch nome-branch          # Comando moderno (Git 2.23+)

# Criar E mudar para branch (atalho)
git checkout -b nome-branch
git switch -c nome-branch       # Comando moderno

# Deletar branch
git branch -d nome-branch       # Seguro (só se já foi merged)
git branch -D nome-branch       # Forçado (CUIDADO!)

# Renomear branch
git branch -m nome-antigo nome-novo
```

### 5.3 Merge

```bash
# Estando na branch que vai RECEBER as mudanças (ex: main)
git checkout main
git merge feature-login

# Merge com commit explícito (--no-ff)
git merge --no-ff feature-login -m "merge: integra feature de login"
```

### 5.4 Resolver Conflitos

Quando duas branches alteram a mesma linha, Git não consegue resolver automaticamente:

```
<<<<<<< HEAD
console.log("Versão da branch main");
=======
console.log("Versão da branch feature");
>>>>>>> feature
```

**Para resolver:**
1. Abra o arquivo com conflito
2. Escolha qual versão manter (ou combine ambas)
3. Remova os marcadores (`<<<<<<<`, `=======`, `>>>>>>>`)
4. `git add arquivo-resolvido.js`
5. `git commit`

---

## 6. GitHub

### 6.1 Repositórios Remotos

```bash
# Adicionar repositório remoto
git remote add origin https://github.com/seu-usuario/fullstack-journey.git

# Verificar remotos
git remote -v

# Enviar código para o GitHub
git push origin main

# Enviar uma branch
git push origin feature-login

# Primeira vez (configura tracking)
git push -u origin main        # Depois disso, basta: git push

# Baixar atualizações
git pull origin main           # Baixa E merge
git fetch origin               # Só baixa (sem merge)
```

### 6.2 Fork & Pull Request

**Fork:** Criar uma cópia de um repositório de outra pessoa na sua conta.

**Pull Request (PR):** Proposta de mudança. Fluxo:

1. Fork o repositório
2. Clone o fork: `git clone git@github.com:SEU-USER/repo.git`
3. Crie uma branch: `git checkout -b minha-feature`
4. Faça as mudanças e commits
5. Push: `git push origin minha-feature`
6. No GitHub: Abra um Pull Request

### 6.3 Issues

Issues são usadas para:
- 🐛 Reportar bugs
- 💡 Sugerir features
- 📋 Gerenciar tarefas

**Dica:** Referencie issues nos commits: `fix: corrige bug do login (#12)`

### 6.4 GitHub Pages

Publicar sites estáticos gratuitamente:

1. Vá em Settings → Pages
2. Selecione a branch (main) e pasta (/ ou /docs)
3. Seu site estará em `https://seu-usuario.github.io/repo`

---

## 7. Git Avançado

### 7.1 Stash

Salvar mudanças temporariamente sem fazer commit:

```bash
# Guardar mudanças
git stash

# Guardar com descrição
git stash save "WIP: formulário de login"

# Listar stashes
git stash list

# Recuperar o último stash
git stash pop               # Aplica E remove da lista
git stash apply             # Aplica E mantém na lista

# Recuperar stash específico
git stash pop stash@{2}

# Deletar stash
git stash drop stash@{0}
```

### 7.2 Rebase

Reescreve o histórico colocando seus commits "em cima" de outra branch:

```bash
# Estando na sua feature branch
git rebase main

# Rebase interativo (para limpar histórico)
git rebase -i HEAD~3        # Editar últimos 3 commits
```

**Opções no rebase interativo:**
- `pick` — Manter o commit
- `squash` — Juntar com o commit anterior
- `reword` — Mudar a mensagem
- `drop` — Remover o commit

> ⚠️ **NUNCA** faça rebase em branches públicas/compartilhadas!

### 7.3 Cherry-pick

Pegar um commit específico de outra branch:

```bash
git cherry-pick <hash-do-commit>
```

### 7.4 Tags

Marcar versões importantes:

```bash
# Criar tag
git tag v1.0.0

# Tag com anotação
git tag -a v1.0.0 -m "Primeira versão estável"

# Listar tags
git tag

# Enviar tags para o GitHub
git push origin v1.0.0
git push origin --tags      # Todas as tags
```

---

## 8. Conventional Commits

Padrão para mensagens de commit que facilita a leitura do histórico e a geração automática de changelogs.

### Formato

```
<tipo>(<escopo opcional>): <descrição>

[corpo opcional]

[rodapé opcional]
```

### Tipos Principais

| Tipo | Quando usar | Exemplo |
|------|------------|---------|
| `feat` | Nova funcionalidade | `feat: adiciona sistema de login` |
| `fix` | Correção de bug | `fix: corrige validação de email` |
| `docs` | Documentação | `docs: atualiza README com instruções de setup` |
| `style` | Formatação (não muda lógica) | `style: aplica formatação do Prettier` |
| `refactor` | Refatoração (não muda comportamento) | `refactor: extrai lógica de autenticação` |
| `test` | Testes | `test: adiciona testes para o serviço de usuários` |
| `chore` | Tarefas auxiliares | `chore: atualiza dependências` |
| `perf` | Performance | `perf: otimiza query de busca` |
| `ci` | CI/CD | `ci: adiciona workflow de testes` |
| `build` | Build/dependências | `build: configura Webpack` |

### Exemplos Completos

```bash
# Simples
git commit -m "feat: adiciona componente de card de produto"

# Com escopo
git commit -m "fix(auth): corrige expiração do token JWT"

# Com corpo explicativo
git commit -m "refactor(api): migra de callbacks para async/await

Migra todas as rotas da API para usar async/await em vez de
callbacks aninhados. Isso melhora a legibilidade e facilita
o tratamento de erros.

Closes #45"

# Breaking change
git commit -m "feat(api)!: altera formato de resposta da API

BREAKING CHANGE: O campo 'data' agora retorna um array
em vez de um objeto."
```

---

## 9. Git Flow

Modelo de branches para projetos profissionais:

```
main ─────────────────────────────────────────────────
  │                                         ↑
  └──> develop ──────────────────────────────┤
         │               ↑         ↑        │
         └──> feature/x ─┘         │        │
         └──> feature/y ───────────┘        │
         └──> release/1.0 ──────────────────┘
                                    ↑
  main ──> hotfix/bug ──────────────┘
```

### Branches Principais
- **main** — Código em produção (estável)
- **develop** — Código de desenvolvimento (integração)

### Branches de Suporte
- **feature/** — Nova funcionalidade (`feature/login-page`)
- **release/** — Preparação para release (`release/1.0.0`)
- **hotfix/** — Correção urgente em produção (`hotfix/fix-crash`)

### Convenção de Nomes para Branches

```
feature/adiciona-login
feature/dashboard-metricas
fix/corrige-validacao-email
hotfix/crash-na-homepage
docs/atualiza-readme
refactor/migra-para-typescript
```

---

## 10. GitHub Actions (Introdução)

GitHub Actions permite automatizar tarefas (CI/CD) diretamente no repositório.

### Primeiro Workflow

Crie o arquivo `.github/workflows/ci.yml`:

```yaml
name: CI

# Quando executar
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

# O que executar
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # 1. Baixar o código
      - uses: actions/checkout@v4

      # 2. Configurar Node.js
      - uses: actions/setup-node@v4
        with:
          node-version: '20'

      # 3. Instalar dependências
      - run: npm ci

      # 4. Rodar linter
      - run: npm run lint

      # 5. Rodar testes
      - run: npm test
```

### Workflow Simples (para começar)

Como ainda não temos Node.js, use este workflow básico:

```yaml
name: Welcome

on:
  push:
    branches: [main]

jobs:
  welcome:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Exibir mensagem
        run: echo "🎉 Push na main com sucesso!"
      - name: Listar arquivos
        run: ls -la
```

---

## 11. Exercícios Práticos

Veja os exercícios na pasta `exercicios/` desta seção.

---

## 📚 Recursos para Aprofundar

| Recurso | Tipo | Link |
|---------|------|------|
| Learn Git Branching | Interativo | [learngitbranching.js.org](https://learngitbranching.js.org) |
| Oh My Git! | Game | [ohmygit.org](https://ohmygit.org/) |
| Git Cheatsheet | Referência | Na pasta `../../recursos/cheatsheets/` |
| Pro Git Book | Livro gratuito | [git-scm.com/book](https://git-scm.com/book/pt-br/v2) |
| GitHub Skills | Curso | [skills.github.com](https://skills.github.com) |

---

## ✅ Checklist da Semana

- [ ] Git instalado e configurado
- [ ] Chave SSH configurada no GitHub
- [ ] Repositório `fullstack-journey` criado e publicado
- [ ] Sabe usar: init, add, commit, status, log, diff
- [ ] Sabe criar e mergear branches
- [ ] Fez pelo menos 1 Pull Request
- [ ] Entende Conventional Commits
- [ ] GitHub Action básica funcionando
- [ ] Completou todos os exercícios práticos
- [ ] Documentou aprendizados neste README
