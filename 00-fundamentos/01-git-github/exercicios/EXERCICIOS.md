# 🏋️ Exercícios Práticos — Git & GitHub

> Complete cada exercício na ordem. Cada um constrói sobre o anterior.

---

## Exercício 1: Primeiros Passos

**Objetivo:** Configurar Git e criar seu primeiro repositório.

### Tarefas:

1. Verifique se o Git está instalado:
   ```bash
   git --version
   ```

2. Configure seu nome e email:
   ```bash
   git config --global user.name "Seu Nome"
   git config --global user.email "seu@email.com"
   ```

3. Crie uma pasta chamada `exercicio-git-01` e inicialize um repositório:
   ```bash
   mkdir exercicio-git-01
   cd exercicio-git-01
   git init
   ```

4. Crie um arquivo `index.html` com o seguinte conteúdo:
   ```html
   <!DOCTYPE html>
   <html lang="pt-BR">
   <head>
       <meta charset="UTF-8">
       <title>Meu Primeiro Repo Git</title>
   </head>
   <body>
       <h1>Olá, Git!</h1>
   </body>
   </html>
   ```

5. Verifique o status, adicione e faça o commit:
   ```bash
   git status
   git add index.html
   git commit -m "feat: adiciona página inicial"
   ```

6. Verifique o histórico:
   ```bash
   git log --oneline
   ```

### ✅ Resultado esperado:
- Um repositório Git inicializado
- Um commit no histórico com a mensagem correta

---

## Exercício 2: Trabalhando com Mudanças

**Objetivo:** Praticar add, commit, diff e restore.

### Tarefas:

1. No mesmo repositório, adicione um arquivo `style.css`:
   ```css
   body {
       font-family: Arial, sans-serif;
       margin: 0;
       padding: 20px;
       background-color: #f0f0f0;
   }

   h1 {
       color: #333;
   }
   ```

2. Modifique `index.html` para linkar o CSS:
   ```html
   <link rel="stylesheet" href="style.css">
   ```

3. Verifique o que mudou:
   ```bash
   git status
   git diff
   ```

4. Adicione APENAS o `style.css` ao staging:
   ```bash
   git add style.css
   git status   # Observe: style.css staged, index.html modified
   ```

5. Faça o commit do CSS:
   ```bash
   git commit -m "style: adiciona estilos básicos da página"
   ```

6. Agora adicione e commite o HTML:
   ```bash
   git add index.html
   git commit -m "feat: linka stylesheet ao HTML"
   ```

7. Veja o histórico:
   ```bash
   git log --oneline
   ```

### ✅ Resultado esperado:
- 3 commits no histórico
- Cada commit com uma mudança lógica separada

---

## Exercício 3: Branches

**Objetivo:** Criar branches, trabalhar nelas e fazer merge.

### Tarefas:

1. Crie e mude para uma branch `feature/nav`:
   ```bash
   git checkout -b feature/nav
   ```

2. Adicione uma barra de navegação no `index.html` (dentro do `<body>`):
   ```html
   <nav>
       <a href="#">Home</a>
       <a href="#">Sobre</a>
       <a href="#">Contato</a>
   </nav>
   ```

3. Adicione estilos para o nav no `style.css`:
   ```css
   nav {
       background-color: #333;
       padding: 10px;
       margin-bottom: 20px;
   }

   nav a {
       color: white;
       text-decoration: none;
       margin-right: 15px;
   }

   nav a:hover {
       text-decoration: underline;
   }
   ```

4. Commit as mudanças:
   ```bash
   git add .
   git commit -m "feat(nav): adiciona barra de navegação"
   ```

5. Volte para a main:
   ```bash
   git checkout main
   ```

6. Observe: o nav **NÃO** está nos arquivos! (foi feito na branch feature/nav)

7. Faça o merge:
   ```bash
   git merge feature/nav -m "merge: integra barra de navegação"
   ```

8. Observe: agora o nav **ESTÁ** nos arquivos!

9. Delete a branch (já foi merged):
   ```bash
   git branch -d feature/nav
   ```

### ✅ Resultado esperado:
- Branch criada, trabalhada e merged com sucesso
- Nav visível na main após o merge

---

## Exercício 4: Resolvendo Conflitos

**Objetivo:** Criar e resolver um conflito de merge propositalmente.

### Tarefas:

1. Crie duas branches a partir da main:
   ```bash
   git checkout -b feature/titulo-azul
   ```

2. Na branch `feature/titulo-azul`, mude o CSS do h1:
   ```css
   h1 {
       color: blue;
       font-size: 2.5rem;
   }
   ```

3. Commit:
   ```bash
   git add .
   git commit -m "style: muda título para azul"
   ```

4. Volte para main e crie outra branch:
   ```bash
   git checkout main
   git checkout -b feature/titulo-vermelho
   ```

5. Na branch `feature/titulo-vermelho`, mude o CSS do h1:
   ```css
   h1 {
       color: red;
       text-transform: uppercase;
   }
   ```

6. Commit:
   ```bash
   git add .
   git commit -m "style: muda título para vermelho maiúsculo"
   ```

7. Volte para main e merge a primeira branch:
   ```bash
   git checkout main
   git merge feature/titulo-azul
   ```

8. Agora tente merge a segunda:
   ```bash
   git merge feature/titulo-vermelho
   ```

9. **CONFLITO!** 🔥 Abra `style.css` e resolva o conflito manualmente. Escolha combinar os dois:
   ```css
   h1 {
       color: blue;
       font-size: 2.5rem;
       text-transform: uppercase;
   }
   ```

10. Complete o merge:
    ```bash
    git add style.css
    git commit -m "merge: resolve conflito de estilos do título"
    ```

### ✅ Resultado esperado:
- Conflito criado e resolvido com sucesso
- Histórico mostra a resolução

---

## Exercício 5: GitHub

**Objetivo:** Publicar seu repositório no GitHub e fazer um Pull Request.

### Tarefas:

1. Crie um novo repositório no GitHub (NÃO inicialize com README)

2. Conecte seu repositório local ao GitHub:
   ```bash
   git remote add origin git@github.com:SEU-USUARIO/exercicio-git-01.git
   git push -u origin main
   ```

3. Crie uma nova branch para uma feature:
   ```bash
   git checkout -b feature/footer
   ```

4. Adicione um footer no `index.html`:
   ```html
   <footer>
       <p>&copy; 2026 Gabriel Barros — Exercício Git</p>
   </footer>
   ```

5. Commit e push:
   ```bash
   git add .
   git commit -m "feat: adiciona footer com copyright"
   git push origin feature/footer
   ```

6. No GitHub, abra um **Pull Request** de `feature/footer` → `main`
   - Título: "feat: adiciona footer com copyright"
   - Descrição: Explique o que foi feito

7. Faça o merge pelo GitHub (botão "Merge pull request")

8. Atualize sua main local:
   ```bash
   git checkout main
   git pull origin main
   ```

### ✅ Resultado esperado:
- Repositório publicado no GitHub
- Pull Request criado e merged com sucesso

---

## Exercício 6: Stash e Histórico

**Objetivo:** Usar stash para guardar trabalho temporário e explorar o histórico.

### Tarefas:

1. Comece a trabalhar numa feature (sem commitar):
   ```bash
   # Adicione algo no index.html (uma seção nova)
   ```

2. Surge uma urgência! Guarde o trabalho:
   ```bash
   git stash save "WIP: seção de projetos"
   ```

3. Faça a correção urgente:
   ```bash
   git checkout -b hotfix/typo
   # Corrija algum texto
   git add .
   git commit -m "fix: corrige typo no título"
   git checkout main
   git merge hotfix/typo
   ```

4. Recupere seu trabalho:
   ```bash
   git stash pop
   ```

5. Continue e commit:
   ```bash
   git add .
   git commit -m "feat: adiciona seção de projetos"
   ```

6. Explore o histórico:
   ```bash
   git log --oneline --graph --all
   git log --author="Gabriel"
   git shortlog
   ```

### ✅ Resultado esperado:
- Stash usado para salvar trabalho temporário
- Histórico limpo e organizado

---

## Exercício 7: Conventional Commits na Prática

**Objetivo:** Fazer uma série de commits seguindo Conventional Commits.

### Tarefas:

Faça os seguintes commits (crie/modifique arquivos para cada um):

1. `feat: adiciona página sobre`
2. `style: melhora espaçamento do nav`
3. `docs: adiciona README com descrição do projeto`
4. `fix: corrige link quebrado no nav`
5. `refactor: reorganiza estrutura CSS`
6. `chore: adiciona .gitignore`

### ✅ Resultado esperado:
- 6+ novos commits, todos seguindo o padrão
- `git log --oneline` mostra um histórico limpo e padronizado

---

## Exercício 8: GitHub Actions

**Objetivo:** Criar seu primeiro workflow de CI.

### Tarefas:

1. No repositório, crie a pasta e arquivo:
   ```bash
   mkdir -p .github/workflows
   ```

2. Crie `.github/workflows/welcome.yml`:
   ```yaml
   name: Welcome CI

   on:
     push:
       branches: [main]

   jobs:
     welcome:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - name: Mostrar estrutura do projeto
           run: |
             echo "🚀 Build iniciado!"
             echo "📁 Estrutura do projeto:"
             find . -not -path './.git/*' | head -30
             echo "✅ Tudo certo!"
   ```

3. Commit e push:
   ```bash
   git add .
   git commit -m "ci: adiciona primeiro workflow de CI"
   git push origin main
   ```

4. No GitHub, vá em **Actions** e veja o workflow rodando!

### ✅ Resultado esperado:
- Workflow executou com sucesso (check verde ✅ no GitHub)

---

## 🏆 Desafio Final da Semana

Combine tudo que aprendeu:

1. Crie um repositório chamado `meu-primeiro-site`
2. Construa um site simples (HTML + CSS) com:
   - Header com navegação
   - Seção "Sobre Mim"
   - Seção "Habilidades"
   - Footer
3. Use **branches** para cada feature (`feature/header`, `feature/about`, etc.)
4. Use **Conventional Commits** em todas as mensagens
5. Publique no **GitHub Pages**
6. Adicione um **README.md** profissional
7. Configure um **GitHub Action** básico

**Tempo estimado:** 4-6 horas

### ✅ Resultado esperado:
- Site publicado no GitHub Pages
- Histórico limpo com branches e Conventional Commits
- GitHub Action funcionando

---

## 📝 Anotações Pessoais

*Use este espaço para anotar suas dúvidas, descobertas e aprendizados:*

```
[Suas anotações aqui]
```
