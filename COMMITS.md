# 📝 Histórico de Commits - Festivite

## Estrutura de Commits

Todos os commits seguem o padrão **Conventional Commits**:

```
tipo(escopo): descrição

Corpo explicativo (opcional)
```

### Tipos de Commit:
- `feat`: Nova funcionalidade
- `docs`: Documentação
- `chore`: Tarefas de manutenção
- `fix`: Correção de bugs
- `style`: Formatação (não afeta código)

---

## 📋 Commits Organizados por Task

### Task 01: Estrutura de Diretórios
- ✅ `chore: adiciona .gitignore`
- ✅ `feat(task-01): cria estrutura de diretórios e arquitetura CSS`
- ✅ `docs(task-01): documenta estrutura de diretórios e arquitetura CSS`

### Task 02: Configuração Global
- ✅ `feat(task-02): implementa configuração global com tokens CSS`
- ✅ `docs(task-02): documenta configuração global e tokens CSS`

### Task 03: Layout Grid
- ✅ `feat(task-03): implementa layout Grid de duas colunas`
- ✅ `docs(task-03): documenta estrutura de layout Grid`

### Task 04: Headers e Títulos
- ✅ `feat(task-04): estiliza header lateral e títulos do formulário`
- ✅ `docs(task-04): documenta estilização de headers e títulos`

### Task 05: Estrutura do Formulário
- ✅ `feat(task-05): implementa estrutura interna do formulário`
- ✅ `docs(task-05): documenta estrutura semântica do formulário`

### Task 06: Estilização de Inputs
- ✅ `feat(task-06): implementa estilos de inputs e estado de foco`
- ✅ `docs(task-06): documenta estilização de inputs e estados`

---

## 🚀 Como Fazer Push para o GitHub

### 1. Criar Repositório no GitHub
1. Acesse https://github.com
2. Clique em "New repository"
3. Nome: `formulario-de-matricula` (ou o nome que preferir)
4. **NÃO** inicialize com README, .gitignore ou license
5. Clique em "Create repository"

### 2. Adicionar Remote e Fazer Push

```bash
# Adicionar remote (substitua SEU_USUARIO pelo seu username do GitHub)
git remote add origin https://github.com/SEU_USUARIO/formulario-de-matricula.git

# Renomear branch para main (se preferir)
git branch -M main

# Fazer push de todos os commits
git push -u origin main
```

### 3. Verificar Push

```bash
# Ver remotes configurados
git remote -v

# Ver histórico de commits
git log --oneline --graph --all
```

---

## 📊 Estatísticas

**Total de Commits:** 15 commits
- 1 chore
- 6 feat
- 8 docs

**Estrutura:**
- Cada task tem 2 commits: 1 feat + 1 docs
- Commits organizados e descritivos
- Histórico limpo e fácil de entender

---

## 💡 Dicas

### Para Próximas Tasks:
1. Sempre faça commits separados para código e documentação
2. Use mensagens descritivas
3. Commite frequentemente (após cada task)
4. Faça push regularmente para backup

### Comandos Úteis:
```bash
# Ver status
git status

# Ver histórico
git log --oneline --graph

# Ver diferenças
git diff

# Adicionar todos os arquivos
git add .

# Commit
git commit -m "tipo(escopo): descrição"

# Push
git push origin main
```

---

**Última atualização:** Task 06 concluída

