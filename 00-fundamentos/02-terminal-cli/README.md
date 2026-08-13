# 📖 Terminal & CLI — Guia Essencial

> *"O terminal é o superpoder do desenvolvedor. Quanto mais confortável você for com ele, mais produtivo será."*

## 📋 Índice

1. [Por que aprender Terminal?](#1-por-que-aprender-terminal)
2. [Configuração no Windows](#2-configuração-no-windows)
3. [Navegação de Arquivos](#3-navegação-de-arquivos)
4. [Manipulação de Arquivos](#4-manipulação-de-arquivos)
5. [Busca e Filtros](#5-busca-e-filtros)
6. [Variáveis de Ambiente](#6-variáveis-de-ambiente)
7. [NPM — Node Package Manager](#7-npm--node-package-manager)
8. [Dicas de Produtividade](#8-dicas-de-produtividade)

---

## 1. Por que aprender Terminal?

- ⚡ **Velocidade** — Muitas tarefas são mais rápidas via terminal
- 🔧 **Automação** — Scripts automatizam tarefas repetitivas
- 🖥️ **Servidores** — Servidores não têm interface gráfica
- 🛠️ **Ferramentas Dev** — Git, NPM, Docker todos rodam no terminal
- 💼 **Entrevistas** — Espera-se que devs saibam usar o terminal

---

## 2. Configuração no Windows

### Instalar Windows Terminal
1. Abra a **Microsoft Store**
2. Busque "Windows Terminal"
3. Instale

### Usar PowerShell (já vem instalado)

O PowerShell é o terminal padrão do Windows. Os comandos abaixo funcionam nele.

> 💡 **Dica:** Muitos comandos Linux funcionam no PowerShell também, pois ele tem aliases.

---

## 3. Navegação de Arquivos

```powershell
# Ver onde você está (diretório atual)
pwd                            # Print Working Directory

# Listar arquivos e pastas
ls                             # Listar conteúdo
ls -la                         # Listar com detalhes (Linux)
Get-ChildItem                  # PowerShell nativo
dir                            # Alternativa Windows

# Navegar entre pastas
cd Desktop                     # Entrar na pasta Desktop
cd ..                          # Voltar uma pasta
cd ~                           # Ir para a pasta do usuário (home)
cd /                           # Ir para a raiz
cd -                           # Voltar para a pasta anterior

# Caminho absoluto vs relativo
cd C:\Users\gabri\Desktop      # Absoluto (caminho completo)
cd Desktop                     # Relativo (a partir de onde estou)
```

---

## 4. Manipulação de Arquivos

```powershell
# Criar pastas
mkdir minha-pasta              # Criar uma pasta
mkdir -p pasta/sub/subsub      # Criar pastas aninhadas

# Criar arquivos
New-Item arquivo.txt           # PowerShell
echo "" > arquivo.txt          # Alternativa
ni arquivo.txt                 # Atalho PowerShell

# Copiar
cp arquivo.txt copia.txt       # Copiar arquivo
cp -r pasta/ copia-pasta/      # Copiar pasta inteira

# Mover / Renomear
mv arquivo.txt nova-pasta/     # Mover
mv antigo.txt novo.txt         # Renomear

# Deletar (CUIDADO: não vai para a lixeira!)
rm arquivo.txt                 # Deletar arquivo
rm -r pasta/                   # Deletar pasta e conteúdo
rm -rf pasta/                  # Deletar forçado (sem confirmação)

# Ler conteúdo de arquivos
cat arquivo.txt                # Mostrar conteúdo inteiro
Get-Content arquivo.txt        # PowerShell nativo
head -n 10 arquivo.txt         # Primeiras 10 linhas (Linux/Git Bash)
tail -n 10 arquivo.txt         # Últimas 10 linhas (Linux/Git Bash)

# Escrever em arquivos
echo "Hello World" > file.txt          # Criar/sobrescrever
echo "Nova linha" >> file.txt          # Adicionar ao final

# Abrir no VS Code
code .                         # Abrir pasta atual no VS Code
code arquivo.txt               # Abrir arquivo específico
```

---

## 5. Busca e Filtros

```powershell
# Buscar arquivos
Get-ChildItem -Recurse -Filter "*.js"     # Buscar todos os .js
Get-ChildItem -Recurse -Filter "*.md"     # Buscar todos os .md

# Buscar texto dentro de arquivos
Select-String -Path "*.js" -Pattern "function"     # Buscar "function" em .js
findstr "TODO" *.js                                # Alternativa Windows

# No Git Bash (comandos Linux)
find . -name "*.js"                        # Buscar arquivos .js
grep -r "function" --include="*.js"        # Buscar texto em .js
grep -rn "TODO" .                          # Buscar com número da linha

# Pipes — Encadear comandos
ls | Select-String "test"                  # Listar e filtrar
Get-Process | Sort-Object CPU -Descending  # Processos por CPU
```

---

## 6. Variáveis de Ambiente

```powershell
# Ver todas as variáveis de ambiente
Get-ChildItem Env:

# Ver uma variável específica
echo $env:PATH
echo $env:USERPROFILE

# Definir variável temporária (só nesta sessão)
$env:MEU_VARIAVEL = "valor"

# Verificar
echo $env:MEU_VARIAVEL

# Arquivo .env (usado em projetos)
# Crie um arquivo .env na raiz do projeto:
# PORT=3000
# DATABASE_URL=postgres://localhost:5432/meudb
# API_KEY=minha_chave_secreta
```

---

## 7. NPM — Node Package Manager

### 7.1 O que é?

**NPM** é o gerenciador de pacotes do Node.js. Com ele você:
- Instala bibliotecas/frameworks
- Gerencia dependências do projeto
- Executa scripts definidos no `package.json`

### 7.2 Comandos Essenciais

```bash
# Verificar instalação
node --version          # Versão do Node.js
npm --version           # Versão do NPM

# Iniciar um projeto (cria package.json)
npm init                # Interativo (responde perguntas)
npm init -y             # Automático (aceita padrões)

# Instalar dependências
npm install express             # Instalar pacote
npm install -D eslint           # Instalar como devDependency
npm install                     # Instalar tudo do package.json
npm ci                          # Instalação limpa (para CI/CD)

# Atalhos
npm i express                   # i = install
npm i -D vitest                 # -D = --save-dev

# Desinstalar
npm uninstall express

# Atualizar
npm update                      # Atualizar tudo
npm outdated                    # Ver pacotes desatualizados

# Executar scripts
npm run dev                     # Rodar script "dev"
npm run build                   # Rodar script "build"
npm test                        # Rodar testes (atalho)
npm start                       # Iniciar app (atalho)

# NPX — Executar pacotes sem instalar
npx create-next-app@latest ./   # Criar projeto Next.js
npx eslint --init               # Configurar ESLint
```

### 7.3 package.json

```json
{
  "name": "meu-projeto",
  "version": "1.0.0",
  "description": "Descrição do projeto",
  "main": "index.js",
  "scripts": {
    "dev": "node src/index.js",
    "build": "tsc",
    "test": "vitest",
    "lint": "eslint ."
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "eslint": "^8.0.0",
    "vitest": "^1.0.0"
  }
}
```

### 7.4 Versionamento Semântico (SemVer)

```
Versão: MAJOR.MINOR.PATCH
         1   .  2  .  3

MAJOR = Mudanças que QUEBRAM compatibilidade
MINOR = Novas funcionalidades (compatível)
PATCH = Correções de bugs (compatível)

No package.json:
"^1.2.3"  = Aceita 1.x.x (minor e patch updates)
"~1.2.3"  = Aceita 1.2.x (só patch updates)
"1.2.3"   = Exatamente esta versão
```

---

## 8. Dicas de Produtividade

### Atalhos do Terminal

| Atalho | Ação |
|--------|------|
| `Tab` | Autocompletar nome de arquivo/pasta |
| `↑` / `↓` | Navegar no histórico de comandos |
| `Ctrl + C` | Cancelar comando em execução |
| `Ctrl + L` | Limpar tela |
| `Ctrl + R` | Buscar no histórico de comandos |
| `Ctrl + A` | Ir para início da linha |
| `Ctrl + E` | Ir para final da linha |

### Caracteres Especiais

```bash
.         # Diretório atual
..        # Diretório pai
~         # Home do usuário
*         # Qualquer coisa (wildcard)
|         # Pipe (encadear comandos)
>         # Redirecionar saída (sobrescreve)
>>        # Redirecionar saída (adiciona)
&&        # Executar próximo comando se anterior deu certo
||        # Executar próximo comando se anterior falhou
```

### Exemplos de Combinações Úteis

```bash
# Criar estrutura de projeto inteira
mkdir -p src/{components,pages,utils,styles} && touch src/index.js

# Encontrar e contar arquivos por tipo
find . -name "*.js" | wc -l

# Matar processo na porta 3000
npx kill-port 3000

# Verificar espaço em disco
Get-PSDrive
```

---

## ✅ Checklist da Semana 2

- [ ] Windows Terminal configurado
- [ ] Sabe navegar pelo sistema de arquivos via terminal
- [ ] Sabe criar, copiar, mover e deletar arquivos/pastas
- [ ] Entende pipes e redirecionamento
- [ ] Sabe usar variáveis de ambiente
- [ ] NPM: init, install, scripts, semver
- [ ] package.json: entende a estrutura
- [ ] Usa atalhos de teclado no terminal
