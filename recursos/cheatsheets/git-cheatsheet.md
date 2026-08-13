# 📋 Git Cheatsheet — Referência Rápida

> Imprima ou salve como favorito. Consulte quando precisar.

---

## ⚙️ Configuração

```bash
git config --global user.name "Nome"          # Nome para commits
git config --global user.email "email"        # Email para commits
git config --global core.editor "code --wait" # Editor padrão
git config --global init.defaultBranch main   # Branch padrão
git config --list                             # Ver configurações
```

## 🏁 Iniciar

```bash
git init                          # Novo repositório
git clone <url>                   # Clonar existente
```

## 📸 Snapshot (Fluxo Básico)

```bash
git status                        # O que mudou?
git diff                          # Detalhes das mudanças
git add <arquivo>                 # Adicionar ao staging
git add .                         # Adicionar tudo
git commit -m "mensagem"          # Salvar snapshot
git commit --amend                # Corrigir último commit
```

## 🔍 Inspecionar

```bash
git log --oneline                 # Histórico resumido
git log --graph --oneline --all   # Gráfico de branches
git show <hash>                   # Detalhes de um commit
git blame <arquivo>               # Quem alterou cada linha
git diff --staged                 # Mudanças no staging
```

## 🌿 Branches

```bash
git branch                        # Listar branches
git branch <nome>                 # Criar branch
git switch <nome>                 # Mudar de branch
git switch -c <nome>              # Criar e mudar
git merge <branch>                # Merge branch na atual
git branch -d <nome>              # Deletar branch (seguro)
git branch -D <nome>              # Deletar (forçado)
```

## ↩️ Desfazer

```bash
git restore <arquivo>             # Descartar mudanças
git restore --staged <arquivo>    # Remover do staging
git reset --soft HEAD~1           # Desfazer commit (manter mudanças)
git reset --hard HEAD~1           # Desfazer commit (descartar tudo!)
git revert <hash>                 # Reverter commit (seguro)
```

## 📦 Stash

```bash
git stash                         # Guardar mudanças
git stash save "descrição"        # Guardar com nome
git stash list                    # Listar guardados
git stash pop                     # Recuperar último
git stash drop                    # Descartar último
```

## 🌐 Remoto (GitHub)

```bash
git remote add origin <url>       # Conectar ao GitHub
git remote -v                     # Ver remotos
git push -u origin main           # Primeiro push
git push                          # Enviar mudanças
git pull                          # Baixar + merge
git fetch                         # Só baixar
```

## 🏷️ Tags

```bash
git tag v1.0.0                    # Criar tag
git tag -a v1.0.0 -m "Release"   # Tag com anotação
git push origin --tags            # Enviar tags
```

## 🔀 Avançado

```bash
git rebase <branch>               # Rebase
git rebase -i HEAD~3              # Rebase interativo
git cherry-pick <hash>            # Pegar commit específico
git bisect start                  # Busca binária por bug
```

## 📝 Conventional Commits

```
feat:     Nova funcionalidade
fix:      Correção de bug
docs:     Documentação
style:    Formatação
refactor: Refatoração
test:     Testes
chore:    Tarefas auxiliares
perf:     Performance
ci:       CI/CD
build:    Build/dependências
```

## ⚡ Atalhos Úteis

```bash
# Aliases (configurar uma vez, usar sempre)
git config --global alias.st "status"
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.ci "commit"
git config --global alias.lg "log --oneline --graph --all"

# Depois de configurar:
git st                            # = git status
git co main                       # = git checkout main
git lg                            # = git log --oneline --graph --all
```
