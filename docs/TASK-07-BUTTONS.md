# 📚 Task 07: Componente Botões Primário e Secundário

## 🎯 Objetivo

Implementar os estilos base para os dois tipos de botões do projeto (Primário para ações principais como "Gerar Convite" e Secundário para ações menores como "Selecionar"). Focar na criação de uma classe base (`.btn`) e classes modificadoras, garantindo a transição suave de cores no estado Hover.

---

## ✅ O Que Foi Implementado

### 1. Estrutura HTML dos Botões

#### Botão Primário (Ação Principal)
```html
<button type="submit" class="btn btn-primary">
  <i data-lucide="mail"></i>
  <span>Gerar convite</span>
</button>
```

**Localização:** Final do formulário, dentro de `.form-actions`

#### Botão Secundário (Ação Secundária)
```html
<button type="button" class="btn btn-secondary">
  <i data-lucide="upload"></i>
  <span>Selecionar</span>
</button>
```

**Localização:** Seção de Personalização (Foto de capa)

---

### 2. Classe Base `.btn`

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-xs);
  padding: var(--spacing-sm) var(--spacing-md);
  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;
  font-family: var(--font-heading);
  font-size: 1rem;
  font-weight: 600;
  line-height: 1.5;
  transition: background-color var(--transition-base);
  text-decoration: none;
}
```

**Características:**
- ✅ **Flexbox:** Alinha ícone e texto horizontalmente
- ✅ **Gap:** Espaçamento entre ícone e texto
- ✅ **Padding:** Espaçamento interno consistente
- ✅ **Cursor:** Pointer para indicar interatividade
- ✅ **Transition:** Animação suave ao mudar estados
- ✅ **Font:** Baloo 2 (heading) para consistência visual

---

### 3. Botão Primário `.btn-primary`

```css
.btn-primary {
  background-color: var(--brand-mid);
  color: var(--text-heading);
}

.btn-primary:hover {
  background-color: var(--color-brand-light);
}

.btn-primary:active {
  background-color: var(--color-brand-dark);
}
```

**Estados:**
- **Default:** Fundo azul médio (`#3487CF`), texto branco
- **Hover:** Fundo azul claro (`#59B2FF`) - mais vibrante
- **Active:** Fundo azul escuro (`#1D6FB6`) - feedback de clique

**Uso:** Ações principais (Gerar convite, Salvar, Enviar)

---

### 4. Botão Secundário `.btn-secondary`

```css
.btn-secondary {
  background-color: var(--shape-button);
  color: var(--text-body);
}

.btn-secondary:hover {
  background-color: var(--shape-hover);
}

.btn-secondary:active {
  background-color: var(--color-shape-body);
}
```

**Estados:**
- **Default:** Fundo cinza escuro (`#2D3134`), texto cinza claro
- **Hover:** Fundo cinza mais claro (`#383D42`)
- **Active:** Fundo cinza médio (`#212427`)

**Uso:** Ações secundárias (Selecionar, Cancelar, Voltar)

---

### 5. Ícones nos Botões

```css
.btn i,
.btn svg {
  width: 20px;
  height: 20px;
  stroke-width: 1.5;
}
```

**Características:**
- ✅ Tamanho consistente (20x20px)
- ✅ Stroke width de 1.5px (padrão Lucide)
- ✅ Alinhamento automático com flexbox

---

### 6. Área de Ações do Formulário

```css
.form-actions {
  margin-top: var(--spacing-xl);
  padding-top: var(--spacing-lg);
  border-top: 1px solid var(--input-stroke);
  display: flex;
  justify-content: flex-end;
}

.form-actions .btn-primary {
  min-width: 200px;
}
```

**Características:**
- ✅ Separador visual (borda superior)
- ✅ Alinhamento à direita
- ✅ Largura mínima para botão principal

---

## 🎓 Conceitos Aprendidos

### 1. Padrão BEM (Block Element Modifier)

**Estrutura:**
- **Block:** `.btn` (componente base)
- **Modifier:** `.btn-primary`, `.btn-secondary` (variações)

**Vantagens:**
- ✅ Reutilização de estilos base
- ✅ Fácil manutenção
- ✅ Escalável (fácil adicionar novos tipos)

**Exemplo:**
```css
/* Block */
.btn { /* estilos base */ }

/* Modifiers */
.btn-primary { /* variação primária */ }
.btn-secondary { /* variação secundária */ }
```

---

### 2. Display Flex para Alinhamento

```css
display: inline-flex;
align-items: center;
justify-content: center;
gap: var(--spacing-xs);
```

**Por que `inline-flex`?**
- `inline-flex`: Botão se comporta como elemento inline, mas filhos são flex
- Permite alinhar ícone e texto facilmente
- Mantém botão no fluxo do texto

**Comparação:**
```css
display: flex;        /* Bloco completo */
display: inline-flex; /* Inline, mas com flex interno ✅ */
display: inline;      /* Sem flex, difícil alinhar */
```

---

### 3. Estados de Interação

**Estados implementados:**
- `:hover` - Mouse sobre o botão
- `:active` - Botão sendo clicado
- `:focus` - Botão recebeu foco (Tab)

**Hierarquia visual:**
```
Default → Hover → Active
  ↓         ↓        ↓
Normal   Mais     Feedback
         claro    de clique
```

---

### 4. Transitions para Animações Suaves

```css
transition: background-color var(--transition-base);
```

**O que faz?**
- Anima mudança de cor de fundo
- Duração: 200ms (var(--transition-base))
- Easing: ease (aceleração suave)

**Resultado:** Mudança de cor suave, não abrupta.

---

### 5. Cursor Pointer

```css
cursor: pointer;
```

**Por quê?**
- Indica que o elemento é clicável
- Melhora UX (usuário sabe que pode clicar)
- Padrão para elementos interativos

---

## 🔍 Detalhes Técnicos

### Por Que Classe Base + Modificadores?

**Abordagem modular:**
```css
/* ✅ BOM - Reutilização */
.btn { /* estilos comuns */ }
.btn-primary { /* apenas diferenças */ }
.btn-secondary { /* apenas diferenças */ }

/* ❌ RUIM - Repetição */
.btn-primary { /* todos os estilos */ }
.btn-secondary { /* todos os estilos repetidos */ }
```

**Benefícios:**
- ✅ DRY (Don't Repeat Yourself)
- ✅ Manutenção fácil
- ✅ Consistência garantida

---

### Por Que `inline-flex` e Não `flex`?

**Diferença:**
- `flex`: Botão ocupa largura total (bloco)
- `inline-flex`: Botão ocupa apenas espaço necessário (inline)

**Exemplo:**
```html
<!-- Com flex -->
<button class="btn">Texto</button>
<!-- Botão ocupa 100% da largura -->

<!-- Com inline-flex -->
<button class="btn">Texto</button>
<!-- Botão ocupa apenas largura do conteúdo ✅ -->
```

---

### Hierarquia de Cores

**Botão Primário:**
- Default: `--brand-mid` (#3487CF) - Azul médio
- Hover: `--color-brand-light` (#59B2FF) - Azul claro (mais vibrante)
- Active: `--color-brand-dark` (#1D6FB6) - Azul escuro (feedback)

**Botão Secundário:**
- Default: `--shape-button` (#2D3134) - Cinza escuro
- Hover: `--shape-hover` (#383D42) - Cinza mais claro
- Active: `--color-shape-body` (#212427) - Cinza médio

**Lógica:** Hover sempre mais claro/claro, Active sempre mais escuro (feedback de clique).

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Reutilização com Classe Base

```css
.btn { /* estilos compartilhados */ }
.btn-primary { /* apenas diferenças */ }
```

**Benefício:** Código limpo e manutenível.

---

### 2. ✅ Uso de Variáveis CSS

```css
background-color: var(--brand-mid);
color: var(--text-heading);
```

**Benefício:** Fácil theming e manutenção.

---

### 3. ✅ Estados de Interação Completos

```css
.btn-primary:hover { }
.btn-primary:active { }
.btn-primary:focus { }
```

**Benefício:** UX profissional e acessível.

---

### 4. ✅ Acessibilidade com Focus

```css
.btn:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(89, 178, 255, 0.2);
}
```

**Benefício:** Feedback visual para navegação por teclado.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Adicionar Novo Tipo de Botão

Crie um botão de "danger" (perigo):
```css
.btn-danger {
  background-color: var(--feedback-danger);
  color: var(--text-heading);
}

.btn-danger:hover {
  background-color: #ff7777; /* vermelho mais claro */
}
```

**O que você aprendeu?**
- Padrão de modificadores
- Reutilização da classe base

---

### Exercício 2: Entender Estados

Teste os estados:
1. Passe o mouse sobre o botão (hover)
2. Clique e segure (active)
3. Use Tab para focar (focus)

O que você observa em cada estado?

**Resposta:** Cores mudam suavemente, dando feedback visual claro.

---

### Exercício 3: Modificar Tamanho

Adicione uma variante de tamanho:
```css
.btn-small {
  padding: var(--spacing-xs) var(--spacing-sm);
  font-size: 0.875rem;
}
```

Use: `<button class="btn btn-primary btn-small">Pequeno</button>`

**O que você aprendeu?**
- Múltiplos modificadores podem ser combinados
- Flexibilidade do padrão BEM

---

## 📊 Comparação: Antes e Depois

### ❌ Antes (Sem Padrão)
- Botões com estilos duplicados
- Difícil manter consistência
- Código repetitivo

### ✅ Depois (Com Padrão BEM)
- Classe base reutilizável
- Modificadores claros
- Código limpo e escalável

---

## 🚀 Próximos Passos

Agora que os botões estão implementados, podemos:

1. **Adicionar mais estados**
   - Disabled
   - Loading
   - Success/Error

2. **Implementar File Input real**
   - Conectar botão secundário ao input de arquivo
   - Mostrar nome do arquivo selecionado

3. **Adicionar validação**
   - Desabilitar botão se formulário inválido
   - Feedback visual de erro

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Por que usar classe base + modificadores?
- [ ] Qual a diferença entre `flex` e `inline-flex`?
- [ ] Por que usar `cursor: pointer`?
- [ ] Como funcionam os estados `:hover`, `:active`, `:focus`?
- [ ] Por que usar `transition` nos botões?
- [ ] Qual a hierarquia de cores (default → hover → active)?

---

## 📚 Recursos Adicionais

- **BEM Methodology:** http://getbem.com/
- **CSS Flexbox:** https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- **Button States:** https://developer.mozilla.org/en-US/docs/Web/CSS/:hover
- **Accessibility:** https://www.w3.org/WAI/WCAG21/Understanding/

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Padrão BEM (Block Element Modifier)
- ✅ Classe base reutilizável
- ✅ Estados de interação (hover, active, focus)
- ✅ Display flex para alinhamento
- ✅ Transitions para animações suaves
- ✅ Hierarquia visual de botões

**Isso é conhecimento fundamental para criar componentes reutilizáveis e profissionais!** 🚀

---

**Próxima Task:** Implementar seletores (radio buttons, checkboxes, switch toggles).

