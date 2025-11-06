# 📚 Task 03: Estrutura de Layout Grid - Painéis Lateral e Principal

## 🎯 Objetivo

Implementar a estrutura HTML principal e o CSS Grid para dividir o aplicativo em duas áreas: o **Painel Lateral Fixo (Preview)** e o **Painel Principal com o Formulário (rolável)**.

---

## ✅ O Que Foi Feito

### 1. Estrutura HTML Criada

```html
<div class="container">
    <!-- Painel Lateral: Preview do Convite -->
    <div class="preview-panel">
        <!-- Conteúdo do preview será adicionado aqui -->
    </div>

    <!-- Painel Principal: Formulário -->
    <main class="form-panel">
        <!-- Conteúdo do formulário será adicionado aqui -->
    </main>
</div>
```

**Elementos criados:**
- ✅ `.container` - Container principal que envolve toda a aplicação
- ✅ `.preview-panel` - Painel lateral esquerdo (preview do convite)
- ✅ `.form-panel` - Painel principal direito (formulário) - usando `<main>` para semântica

---

### 2. CSS Grid Implementado

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2.5fr;
  border-radius: 12px;
  overflow: hidden;
  min-height: 100vh;
}

.preview-panel {
  background: var(--shape-body);
  padding: var(--spacing-lg);
}

.form-panel {
  background: var(--shape-body);
  padding: var(--spacing-lg);
  overflow-y: auto;
}
```

---

## 🎓 Conceitos Aprendidos

### 1. CSS Grid - O Que É?

**CSS Grid** é um sistema de layout bidimensional que permite criar layouts complexos com linhas e colunas.

**Analogia:**
Imagine uma tabela do Excel, mas muito mais poderosa! Você define quantas colunas quer e como elas se comportam.

**Diferença entre Grid e Flexbox:**
- **Flexbox:** Layout unidimensional (linha OU coluna)
- **Grid:** Layout bidimensional (linhas E colunas ao mesmo tempo)

---

### 2. `display: grid`

**O que faz?**
Transforma o elemento em um **container grid**, permitindo que os filhos sejam organizados em grade.

```css
.container {
  display: grid; /* Ativa o Grid Layout */
}
```

**Por que usar?**
- ✅ Controle total sobre linhas e colunas
- ✅ Alinhamento fácil
- ✅ Responsivo nativamente
- ✅ Menos código que float/flexbox para layouts complexos

---

### 3. `grid-template-columns`

**O que faz?**
Define quantas colunas o grid terá e qual o tamanho de cada uma.

```css
grid-template-columns: 1fr 2.5fr;
```

**O que significa `fr`?**
- **`fr`** = **fraction** (fração)
- Representa uma fração do espaço disponível
- `1fr 2.5fr` significa:
  - Primeira coluna: 1 parte do espaço
  - Segunda coluna: 2.5 partes do espaço
  - Total: 3.5 partes
  - Primeira coluna = 1/3.5 ≈ 28.5% da largura
  - Segunda coluna = 2.5/3.5 ≈ 71.5% da largura

**Outras unidades possíveis:**
```css
grid-template-columns: 300px 1fr;        /* Fixo + flexível */
grid-template-columns: 1fr 1fr 1fr;     /* 3 colunas iguais */
grid-template-columns: repeat(3, 1fr);  /* 3 colunas iguais (sintaxe curta) */
grid-template-columns: minmax(200px, 1fr) 2fr; /* Mínimo 200px, máximo flexível */
```

**No nosso projeto:**
- Preview panel: ~28.5% da largura
- Form panel: ~71.5% da largura
- Isso dá mais espaço para o formulário, que precisa de mais área

---

### 4. `border-radius: 12px`

**O que faz?**
Arredonda os cantos do elemento.

```css
border-radius: 12px; /* Todos os cantos com 12px */
```

**Variações:**
```css
border-radius: 12px;                    /* Todos os cantos */
border-radius: 12px 8px;               /* Superior: 12px, Inferior: 8px */
border-radius: 12px 8px 16px 4px;      /* Topo-esquerdo, topo-direito, inferior-direito, inferior-esquerdo */
border-radius: 50%;                     /* Círculo perfeito */
```

**Por que usar?**
- ✅ Design moderno e suave
- ✅ Remove cantos "duros"
- ✅ Melhora a estética visual

---

### 5. `overflow: hidden`

**O que faz?**
Esconde qualquer conteúdo que ultrapasse os limites do elemento.

```css
overflow: hidden;
```

**Outras opções:**
```css
overflow: visible;  /* Mostra tudo (padrão) */
overflow: hidden;   /* Esconde o que ultrapassa */
overflow: scroll;   /* Sempre mostra scrollbar */
overflow: auto;     /* Mostra scrollbar só quando necessário */
```

**Por que usar no container?**
- ✅ Garante que o `border-radius` funcione corretamente
- ✅ Previne que conteúdo interno "vaze" para fora
- ✅ Mantém o design limpo

**Exemplo prático:**
```css
.container {
  border-radius: 12px;
  overflow: hidden; /* Sem isso, filhos podem "vazar" pelos cantos */
}
```

---

### 6. `min-height: 100vh`

**O que faz?**
Define a altura mínima do elemento como 100% da altura da viewport (tela).

```css
min-height: 100vh;
```

**O que é `vh`?**
- **`vh`** = **viewport height** (altura da viewport)
- `100vh` = 100% da altura da tela
- `50vh` = 50% da altura da tela

**Por que usar?**
- ✅ Garante que o container ocupe toda a altura da tela
- ✅ Layout sempre preenche a tela, mesmo com pouco conteúdo
- ✅ Melhor experiência visual

**Diferença:**
```css
height: 100vh;      /* Altura fixa de 100vh */
min-height: 100vh;  /* Altura mínima de 100vh (pode crescer se necessário) */
```

---

### 7. `overflow-y: auto`

**O que faz?**
Adiciona scrollbar vertical apenas quando o conteúdo ultrapassar a altura disponível.

```css
overflow-y: auto;
```

**Por que usar no `.form-panel`?**
- ✅ Formulário pode ser longo
- ✅ Permite rolar apenas o formulário, não toda a página
- ✅ Preview panel fica fixo enquanto formulário rola
- ✅ Melhor UX (experiência do usuário)

**Outras opções:**
```css
overflow-y: visible; /* Mostra tudo (pode ultrapassar) */
overflow-y: hidden;  /* Esconde o que ultrapassa */
overflow-y: scroll;  /* Sempre mostra scrollbar */
overflow-y: auto;    /* Mostra scrollbar só quando necessário ✅ */
```

---

### 8. Variáveis CSS nos Painéis

```css
.preview-panel {
  background: var(--shape-body);
  padding: var(--spacing-lg);
}
```

**Por que usar variáveis?**
- ✅ Consistência visual
- ✅ Fácil manutenção
- ✅ Mudança em um lugar afeta todos os painéis

**Valores:**
- `--shape-body: #212427` (cor de fundo dos painéis)
- `--spacing-lg: 2rem` (32px de padding)

---

## 🔍 Detalhes Técnicos

### Por Que Grid e Não Flexbox?

**Grid é melhor para:**
- ✅ Layouts de duas colunas (como o nosso)
- ✅ Quando precisa controlar linhas E colunas
- ✅ Layouts mais complexos

**Flexbox é melhor para:**
- ✅ Alinhar itens em uma direção (linha OU coluna)
- ✅ Componentes individuais
- ✅ Menus, botões, cards

**No nosso caso:**
Grid é perfeito porque temos duas colunas bem definidas!

---

### Estrutura Semântica HTML

**Por que `<main>` no form-panel?**
```html
<main class="form-panel">
```

**Razões:**
- ✅ Semântica HTML5 correta
- ✅ `<main>` indica conteúdo principal
- ✅ Melhor para acessibilidade (screen readers)
- ✅ Melhor para SEO

**Elementos semânticos:**
- `<header>` - Cabeçalho
- `<nav>` - Navegação
- `<main>` - Conteúdo principal ✅
- `<aside>` - Conteúdo lateral
- `<footer>` - Rodapé

---

### Responsividade (Próximos Passos)

**Atualmente:**
```css
grid-template-columns: 1fr 2.5fr; /* Sempre duas colunas */
```

**Para mobile (futuro):**
```css
@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr; /* Uma coluna no mobile */
  }
}
```

Isso será implementado em uma task futura de responsividade!

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Uso de Variáveis CSS

```css
background: var(--shape-body);
padding: var(--spacing-lg);
```

**Benefício:** Consistência e fácil manutenção.

### 2. ✅ Semântica HTML

```html
<main class="form-panel">
```

**Benefício:** Melhor acessibilidade e SEO.

### 3. ✅ Comentários Organizados

```css
/* ============================================
   CONTAINER PRINCIPAL
   ============================================ */
```

**Benefício:** Fácil navegação no código.

### 4. ✅ Overflow Controlado

```css
.container { overflow: hidden; }      /* Contém tudo */
.form-panel { overflow-y: auto; }    /* Rola quando necessário */
```

**Benefício:** UX melhorada com scroll controlado.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Entender `fr`

Mude `grid-template-columns` para:
```css
grid-template-columns: 1fr 1fr;
```

O que acontece? Por quê?

**Resposta:** As duas colunas ficam iguais (50% cada), porque ambas têm `1fr`.

---

### Exercício 2: Testar Overflow

Remova `overflow: hidden` do `.container` e adicione uma borda:
```css
.container {
  border: 2px solid red;
}
```

O que acontece com o `border-radius`?

**Resposta:** O `border-radius` pode não funcionar corretamente se os filhos ultrapassarem os limites.

---

### Exercício 3: Testar Scroll

Adicione muito conteúdo no `.form-panel`:
```html
<div class="form-panel">
  <p>Conteúdo</p>
  <p>Conteúdo</p>
  <!-- Repita 20 vezes -->
</div>
```

O que acontece? O preview panel rola também?

**Resposta:** Não! Apenas o `.form-panel` rola, porque só ele tem `overflow-y: auto`.

---

## 📊 Estrutura Visual Criada

```
┌─────────────────────────────────────────┐
│         .container (Grid)               │
│  ┌──────────┐  ┌──────────────────┐   │
│  │ Preview  │  │   Form Panel     │   │
│  │  Panel   │  │   (rolável)      │   │
│  │          │  │                  │   │
│  │  Fixo    │  │  ┌────────────┐ │   │
│  │          │  │  │ Formulário │ │   │
│  │          │  │  │            │ │   │
│  │          │  │  │   ...      │ │   │
│  │          │  │  │            │ │   │
│  │          │  │  └────────────┘ │   │
│  └──────────┘  └──────────────────┘   │
└─────────────────────────────────────────┘
   1fr (28.5%)    2.5fr (71.5%)
```

---

## 🚀 Próximos Passos

Agora que o layout está pronto, podemos:

1. **Adicionar conteúdo ao preview-panel**
   - Logo Festivite
   - Tagline
   - Preview do convite

2. **Adicionar conteúdo ao form-panel**
   - Título "Crie seu convite"
   - Seções do formulário
   - Campos de input

3. **Implementar responsividade**
   - Grid de uma coluna no mobile
   - Ajustes de padding e espaçamento

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] O que é CSS Grid e quando usar?
- [ ] O que significa `fr` em `grid-template-columns`?
- [ ] Por que usar `overflow: hidden` no container?
- [ ] Por que usar `overflow-y: auto` no form-panel?
- [ ] O que é `vh` e por que usar `min-height: 100vh`?
- [ ] Qual a diferença entre Grid e Flexbox?
- [ ] Por que usar `<main>` em vez de `<div>`?

---

## 📚 Recursos Adicionais

- **CSS Grid Guide:** https://css-tricks.com/snippets/css/complete-guide-grid/
- **Grid vs Flexbox:** https://css-tricks.com/css-grid-vs-flexbox/
- **Viewport Units:** https://developer.mozilla.org/en-US/docs/Web/CSS/length#viewport-percentage_lengths
- **Overflow Property:** https://developer.mozilla.org/en-US/docs/Web/CSS/overflow

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Como criar layouts com CSS Grid
- ✅ Como dividir espaço com `grid-template-columns`
- ✅ Como controlar overflow e scroll
- ✅ Boas práticas de semântica HTML
- ✅ Uso de variáveis CSS no layout

**Isso é conhecimento fundamental para criar layouts profissionais!** 🚀

---

**Próxima Task:** Adicionar conteúdo aos painéis e criar a estrutura do formulário.

