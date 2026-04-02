# 🌿 Tutorial de Comandos Git — Uso no Dia a Dia

> **Git** é um sistema de controle de versão distribuído. Cada repositório local contém o histórico completo do projeto, permitindo trabalhar offline e colaborar com segurança.

---

## 1. Conceitos Fundamentais

| Conceito | O que é |
|----------|---------|
| **Working Directory** | Onde você edita os arquivos |
| **Staging Area (Index)** | Área de preparação antes do commit |
| **Repository (.git)** | Histórico e metadados do projeto |
| **Branch** | Linha independente de desenvolvimento |
| **HEAD** | Ponteiro para o commit/branch atual |
| **Remote** | Repositório remoto (ex: GitHub, GitLab) |

---

## 2. Configuração Inicial

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
git config --global core.editor vim          # Define o editor padrão
git config --global init.defaultBranch main  # Branch padrão ao iniciar
git config --list                            # Lista todas as configurações
```

---

## 3. Criando e Clonando Repositórios

| Comando | Ação |
|---------|------|
| `git init` | Inicia um repositório no diretório atual |
| `git init nome-projeto` | Inicia em um novo diretório |
| `git clone <url>` | Clona um repositório remoto |
| `git clone <url> pasta` | Clona dentro de uma pasta específica |
| `git clone --depth 1 <url>` | Clona apenas o último commit (shallow clone) |

---

## 4. Inspecionando o Repositório

| Comando | Ação |
|---------|------|
| `git status` | Exibe o estado dos arquivos |
| `git status -s` | Versão curta do status |
| `git log` | Histórico de commits |
| `git log --oneline` | Histórico resumido (uma linha por commit) |
| `git log --oneline --graph --all` | Histórico visual com todas as branches |
| `git log -p` | Histórico com diff de cada commit |
| `git log --author="Nome"` | Filtra commits por autor |
| `git diff` | Diferenças não indexadas (unstaged) |
| `git diff --staged` | Diferenças indexadas (staged) |
| `git diff branch1..branch2` | Diferenças entre duas branches |
| `git show <commit>` | Detalhes de um commit específico |
| `git blame arquivo` | Mostra quem alterou cada linha |

---

## 5. Staging e Commits

### Adicionar ao Stage

| Comando | Ação |
|---------|------|
| `git add arquivo.txt` | Adiciona um arquivo específico |
| `git add .` | Adiciona todos os arquivos modificados |
| `git add -p` | Adiciona interativamente por trecho (hunk) |
| `git add *.js` | Adiciona todos os arquivos `.js` |
| `git rm arquivo` | Remove arquivo do disco e do stage |
| `git rm --cached arquivo` | Remove do stage, mantém no disco |
| `git mv origem destino` | Move/renomeia e já indexa a mudança |

### Fazer Commits

| Comando | Ação |
|---------|------|
| `git commit -m "mensagem"` | Commit com mensagem inline |
| `git commit` | Abre o editor para a mensagem |
| `git commit -am "mensagem"` | Stage + commit de arquivos já rastreados |
| `git commit --amend` | Corrige o último commit (mensagem ou conteúdo) |
| `git commit --amend --no-edit` | Corrige o conteúdo sem alterar a mensagem |

---

## 6. Branches

| Comando | Ação |
|---------|------|
| `git branch` | Lista branches locais |
| `git branch -a` | Lista branches locais e remotas |
| `git branch nome` | Cria uma nova branch |
| `git branch -d nome` | Deleta branch (seguro) |
| `git branch -D nome` | Força a deleção da branch |
| `git branch -m novo-nome` | Renomeia a branch atual |
| `git switch nome` | Muda para a branch |
| `git switch -c nome` | Cria e muda para a nova branch |
| `git checkout nome` | Muda para a branch (forma clássica) |
| `git checkout -b nome` | Cria e muda (forma clássica) |

---

## 7. Merge e Rebase

### Merge

```bash
git merge feature       # Incorpora a branch 'feature' na atual
git merge --no-ff feature  # Força commit de merge (preserva histórico)
git merge --squash feature # Combina todos os commits em um só
git merge --abort       # Cancela um merge em conflito
```

### Rebase

```bash
git rebase main         # Reaplica commits da branch atual sobre 'main'
git rebase -i HEAD~3    # Rebase interativo dos últimos 3 commits
git rebase --abort      # Cancela o rebase
git rebase --continue   # Continua após resolver conflito
```

> 💡 **Regra de ouro:** nunca faça `rebase` em branches públicas/compartilhadas.

### Resolvendo Conflitos

```bash
# 1. Edite os arquivos com conflito (procure por <<<<<<<)
# 2. Marque como resolvido:
git add arquivo-resolvido.txt
# 3. Finalize:
git commit           # para merge
git rebase --continue  # para rebase
```

---

## 8. Desfazendo Alterações

| Comando | Ação |
|---------|------|
| `git restore arquivo` | Descarta alterações no working directory |
| `git restore --staged arquivo` | Remove do stage (mantém as mudanças) |
| `git restore .` | Descarta **todas** as alterações locais |
| `git revert <commit>` | Cria um novo commit que desfaz o commit alvo |
| `git reset --soft HEAD~1` | Desfaz o último commit, mantém no stage |
| `git reset --mixed HEAD~1` | Desfaz o commit e o stage (padrão) |
| `git reset --hard HEAD~1` | Desfaz tudo, **perde as alterações** |
| `git clean -fd` | Remove arquivos e pastas não rastreados |

> ⚠️ `reset --hard` e `clean -fd` são **destrutivos** — use com cuidado.

---

## 9. Repositórios Remotos

| Comando | Ação |
|---------|------|
| `git remote -v` | Lista os remotos configurados |
| `git remote add origin <url>` | Adiciona um remoto chamado `origin` |
| `git remote rename origin upstream` | Renomeia um remoto |
| `git remote remove nome` | Remove um remoto |
| `git fetch` | Baixa atualizações sem aplicar |
| `git fetch --prune` | Baixa e remove branches remotas deletadas |
| `git pull` | Fetch + merge da branch atual |
| `git pull --rebase` | Fetch + rebase (histórico mais limpo) |
| `git push origin nome-branch` | Envia a branch para o remoto |
| `git push -u origin nome-branch` | Envia e define o upstream |
| `git push --force-with-lease` | Push forçado com verificação de segurança |
| `git push origin --delete nome` | Deleta uma branch remota |

---

## 10. Tags

| Comando | Ação |
|---------|------|
| `git tag` | Lista todas as tags |
| `git tag v1.0.0` | Cria uma tag leve |
| `git tag -a v1.0.0 -m "Release 1.0"` | Cria uma tag anotada |
| `git tag v1.0.0 <commit>` | Cria tag em um commit específico |
| `git push origin v1.0.0` | Envia uma tag para o remoto |
| `git push origin --tags` | Envia todas as tags |
| `git tag -d v1.0.0` | Deleta uma tag local |

---

## 11. Stash

Salva temporariamente alterações sem fazer commit.

| Comando | Ação |
|---------|------|
| `git stash` | Guarda as alterações atuais |
| `git stash push -m "descrição"` | Guarda com uma descrição |
| `git stash list` | Lista todos os stashes |
| `git stash pop` | Aplica e remove o stash mais recente |
| `git stash apply stash@{2}` | Aplica um stash específico sem removê-lo |
| `git stash drop stash@{0}` | Remove um stash específico |
| `git stash clear` | Remove todos os stashes |
| `git stash branch nome` | Cria uma branch a partir do stash |

---

## 12. Comandos Avançados Úteis

| Comando | Ação |
|---------|------|
| `git cherry-pick <commit>` | Aplica um commit específico na branch atual |
| `git bisect start` | Inicia busca binária por um bug |
| `git bisect good <commit>` | Marca commit como sem o bug |
| `git bisect bad <commit>` | Marca commit como com o bug |
| `git shortlog -sn` | Ranking de commits por autor |
| `git reflog` | Histórico completo de movimentos do HEAD |
| `git archive --format=zip HEAD > saida.zip` | Exporta o projeto como zip |

### Aliases úteis para o `~/.gitconfig`

```ini
[alias]
  lg = log --oneline --graph --all --decorate
  st = status -s
  undo = reset --soft HEAD~1
  oops = commit --amend --no-edit
  aliases = config --get-regexp alias
```

---

## 13. .gitignore

```bash
# Ignorar por extensão
*.log
*.env

# Ignorar pasta
node_modules/
dist/

# Ignorar arquivo específico
config/secrets.yml

# Exceção (não ignorar mesmo se a regra acima cobrir)
!config/secrets.example.yml
```

```bash
git check-ignore -v arquivo   # Descobre qual regra está ignorando o arquivo
git rm -r --cached .          # Remove tudo do cache (útil após editar .gitignore)
git add .                     # Re-adiciona respeitando o novo .gitignore
```

---

## 14. Fluxo de Trabalho Típico

```bash
# 1. Atualizar a main
git switch main
git pull

# 2. Criar branch para a feature
git switch -c feature/minha-feature

# 3. Trabalhar e commitar
git add -p
git commit -m "feat: adiciona nova funcionalidade"

# 4. Atualizar com a main antes de abrir PR
git fetch origin
git rebase origin/main

# 5. Enviar para o remoto
git push -u origin feature/minha-feature
```

---

> 💡 **Dica final:** use `git help <comando>` ou `git <comando> --help` para abrir a documentação completa de qualquer comando diretamente no terminal.
