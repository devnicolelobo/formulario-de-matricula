# 📚 Task 06: Implementação de Inputs Básicos e Estado de Foco

## 🎯 Objetivo

Implementar o estilo de base para todos os inputs de texto, garantindo que o design do Dark Mode seja aplicado corretamente. O foco é na reutilização de estilos entre diferentes tipos de input e na implementação visual do estado de Active (Foco), usando a cor da marca.

---

## ✅ O Que Foi Implementado

### 1. Estilos Base para Todos os Inputs

```css
input[type="text"],
input[type="email"],
input[type="tel"],
input[type="date"],
textarea {
  width: 100%;
  background: var(--input-base);
  border: 1px solid var(--input-stroke);
  border-radius: var(--radius-md);
  padding: var(--spacing-sm);
  color: var(--text-heading);
  font-family: var(--font-body);
  font-size: 1rem;
  line-height: 1.5;
  transition: border-color var(--transition-base), box-shadow var(--transition-base);
}
```

**Características:**
- ✅ **Reutilização:** Mesmos estilos para todos os tipos de input
- ✅ **Dark Mode:** Cores escuras (`--input-base: #1C1F21`)
- ✅ **Consistência:** Mesmo padding, border-radius, font
- ✅ **Transições:** Animações suaves ao mudar estados

---

### 2. Estilização de Placeholder

```css
input[type="text"]::placeholder,
input[type="email"]::placeholder,
input[type="tel"]::placeholder,
input[type="date"]::placeholder,
textarea::placeholder {
  color: var(--input-placeholder);
  opacity: 1;
}
```

**Por que `opacity: 1`?**
- Alguns navegadores aplicam `opacity: 0.5` por padrão
- Garantimos que o placeholder tenha a cor correta (`#869198`)
- Texto de hint sempre visível e legível

---

### 3. Estado de Foco (Active)

```css
input[type="text"]:focus,
input[type="email"]:focus,
input[type="tel"]:focus,
input[type="date"]:focus,
textarea:focus {
  outline: none;
  border-color: var(--color-brand-light);
  box-shadow: 0 0 0 3px rgba(89, 178, 255, 0.1);
}
```

**Efeitos visuais:**
- ✅ **Borda azul:** `border-color: var(--color-brand-light)` (#59B2FF)
- ✅ **Glow sutil:** `box-shadow` com cor azul translúcida
- ✅ **Sem outline padrão:** `outline: none` remove o outline do navegador

**Por que remover outline?**
- Outline padrão do navegador não segue o design
- Criamos nosso próprio feedback visual (borda + shadow)
- ⚠️ **Importante:** Sempre fornecer feedback visual alternativo!

---

### 4. Textarea com Resize Controlado

```css
textarea {
  resize: vertical;
  min-height: 100px;
}
```

**Opções de resize:**
- `resize: vertical` - Permite redimensionar apenas verticalmente ✅
- `resize: horizontal` - Apenas horizontalmente
- `resize: both` - Ambos os lados (padrão)
- `resize: none` - Não permite redimensionar

**Por que `vertical`?**
- ✅ Usuário pode ajustar altura conforme necessário
- ✅ Largura permanece consistente (100% do container)
- ✅ Melhor UX para textos longos

---

### 5. Input Wrapper - Layout Vertical

```css
.input-wrapper {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
  margin-bottom: var(--spacing-md);
}

.input-wrapper label {
  color: var(--text-body);
  font-family: var(--font-body);
  font-size: 0.875rem;
  font-weight: 600;
}
```

**Estrutura:**
- **Flexbox column:** Label acima, input abaixo
- **Gap:** Espaçamento consistente entre label e input
- **Margin-bottom:** Espaçamento entre campos

---

### 6. Inputs Lado a Lado (Grid)

```css
.input-group {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--spacing-md);
}

@media (max-width: 768px) {
  .input-group {
    grid-template-columns: 1fr;
  }
}
```

**Uso no HTML:**
```html
<div class="input-group">
  <div class="input-wrapper">
    <label for="event-start">Início</label>
    <input type="date" id="event-start">
  </div>
  <div class="input-wrapper">
    <label for="event-end">Fim</label>
    <input type="date" id="event-end">
  </div>
</div>
```

**Características:**
- ✅ **Grid 2 colunas:** `1fr 1fr` divide espaço igualmente
- ✅ **Responsivo:** Uma coluna no mobile (< 768px)
- ✅ **Gap:** Espaçamento entre os campos

---

## 🎓 Conceitos Aprendidos

### 1. Seletores CSS - Agrupamento

**Agrupando seletores:**
```css
input[type="text"],
input[type="email"],
textarea {
  /* Estilos comuns */
}
```

**Vantagens:**
- ✅ DRY (Don't Repeat Yourself)
- ✅ Manutenção fácil (mudança em um lugar)
- ✅ Código limpo e organizado

**Alternativa (ruim):**
```css
input[type="text"] { /* estilos */ }
input[type="email"] { /* mesmos estilos */ }
textarea { /* mesmos estilos */ }
/* Repetição desnecessária! */
```

---

### 2. Pseudo-elementos - `::placeholder`

**O que são pseudo-elementos?**
- Elementos que não existem no HTML
- Criados via CSS
- Representam partes específicas de elementos

**Sintaxe:**
```css
input::placeholder {
  color: var(--input-placeholder);
}
```

**Outros pseudo-elementos comuns:**
- `::before` - Conteúdo antes do elemento
- `::after` - Conteúdo depois do elemento
- `::first-line` - Primeira linha de texto
- `::selection` - Texto selecionado

---

### 3. Pseudo-classes - `:focus`

**O que são pseudo-classes?**
- Estados especiais de elementos
- Aplicadas automaticamente pelo navegador
- Não precisam ser adicionadas no HTML

**Estados comuns:**
- `:hover` - Mouse sobre o elemento
- `:focus` - Elemento recebeu foco (Tab ou clique)
- `:active` - Elemento está sendo clicado
- `:disabled` - Elemento desabilitado
- `:checked` - Checkbox/radio selecionado

**Exemplo prático:**
```css
input:focus {
  border-color: blue; /* Aplica quando input recebe foco */
}
```

---

### 4. Box Shadow - Criando Glow

**Sintaxe:**
```css
box-shadow: offset-x offset-y blur-radius spread-radius color;
```

**Nosso exemplo:**
```css
box-shadow: 0 0 0 3px rgba(89, 178, 255, 0.1);
```

**Breakdown:**
- `0` - offset-x (sem deslocamento horizontal)
- `0` - offset-y (sem deslocamento vertical)
- `0` - blur-radius (sem desfoque)
- `3px` - spread-radius (expansão de 3px)
- `rgba(89, 178, 255, 0.1)` - Cor azul com 10% de opacidade

**Resultado:** Um "glow" azul sutil ao redor do input focado.

**Outros exemplos:**
```css
box-shadow: 0 2px 4px rgba(0,0,0,0.1); /* Sombra suave */
box-shadow: 0 0 10px rgba(89, 178, 255, 0.5); /* Glow mais forte */
box-shadow: inset 0 2px 4px rgba(0,0,0,0.1); /* Sombra interna */
```

---

### 5. Transitions - Animações Suaves

```css
transition: border-color var(--transition-base), box-shadow var(--transition-base);
```

**O que faz?**
- Anima mudanças de `border-color` e `box-shadow`
- Duração: `var(--transition-base)` (200ms)
- Easing: `ease` (aceleração suave)

**Sintaxe completa:**
```css
transition: propriedade duração timing-function delay;
```

**Benefícios:**
- ✅ Feedback visual suave
- ✅ UX melhorada
- ✅ Profissionalismo

**Sem transition:**
- Mudanças instantâneas (pode parecer "duro")
- Menos polido

---

### 6. CSS Grid para Layout de 2 Colunas

```css
.input-group {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--spacing-md);
}
```

**Por que Grid e não Flexbox?**
- Grid é perfeito para layouts de 2 dimensões (linhas E colunas)
- Flexbox é melhor para 1 dimensão (linha OU coluna)

**Comparação:**
```css
/* Grid - 2 colunas iguais */
display: grid;
grid-template-columns: 1fr 1fr;

/* Flexbox - 2 colunas iguais */
display: flex;
gap: var(--spacing-md);
/* Mas precisa definir width nos filhos */
```

**Grid é mais simples para este caso!**

---

### 7. Media Queries - Responsividade

```css
@media (max-width: 768px) {
  .input-group {
    grid-template-columns: 1fr;
  }
}
```

**O que faz?**
- Quando a tela tem **menos de 768px de largura**
- Muda o grid de 2 colunas para 1 coluna
- Melhor UX em mobile

**Breakpoints comuns:**
- `768px` - Tablet/Mobile
- `1024px` - Desktop pequeno
- `1440px` - Desktop grande

**Sintaxe:**
```css
@media (condição) {
  /* Estilos aplicados quando condição é verdadeira */
}
```

---

## 🔍 Detalhes Técnicos

### Por Que `outline: none`?

**Outline padrão do navegador:**
- Cor: azul (varia por navegador)
- Estilo: não segue nosso design
- Acessibilidade: importante manter feedback visual

**Nossa solução:**
- Removemos outline padrão
- Criamos nosso próprio feedback (borda azul + shadow)
- ✅ Mantém acessibilidade (feedback visual claro)

**⚠️ Regra de ouro:**
Sempre que remover `outline`, forneça feedback visual alternativo!

---

### Por Que `width: 100%`?

**Problema sem width:**
- Inputs podem ter largura inconsistente
- Depende do conteúdo (placeholder, texto)

**Solução:**
```css
width: 100%;
```

**Resultado:**
- ✅ Inputs ocupam 100% do container
- ✅ Largura consistente
- ✅ Responsivo automaticamente

---

### Por Que `resize: vertical` no Textarea?

**Opções:**
- `resize: both` (padrão) - Pode quebrar layout
- `resize: none` - Usuário não pode ajustar
- `resize: vertical` ✅ - Permite ajuste sem quebrar layout

**Benefício:**
- Usuário pode expandir para textos longos
- Largura permanece consistente
- Melhor UX

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Reutilização de Estilos

Agrupamos todos os inputs com mesmos estilos:
```css
input[type="text"],
input[type="email"],
input[type="tel"],
input[type="date"],
textarea {
  /* Estilos comuns */
}
```

**Benefício:** DRY (Don't Repeat Yourself)

---

### 2. ✅ Uso de Variáveis CSS

```css
background: var(--input-base);
border-color: var(--color-brand-light);
```

**Benefício:** Fácil manutenção e theming

---

### 3. ✅ Transitions para Suavidade

```css
transition: border-color var(--transition-base), box-shadow var(--transition-base);
```

**Benefício:** UX profissional

---

### 4. ✅ Responsividade Mobile-First

```css
.input-group {
  grid-template-columns: 1fr 1fr; /* Desktop */
}

@media (max-width: 768px) {
  .input-group {
    grid-template-columns: 1fr; /* Mobile */
  }
}
```

**Benefício:** Funciona bem em todos os dispositivos

---

## 🧪 Exercícios de Fixação

### Exercício 1: Entender Box Shadow

Mude o box-shadow do foco para:
```css
box-shadow: 0 0 0 5px rgba(89, 178, 255, 0.2);
```

O que mudou? Por quê?

**Resposta:** O glow ficou maior (5px) e mais visível (20% opacidade).

---

### Exercício 2: Testar Resize

Mude o textarea para:
```css
textarea {
  resize: both;
}
```

O que acontece? Por que isso pode ser problemático?

**Resposta:** Permite redimensionar em ambos os lados, pode quebrar o layout.

---

### Exercício 3: Adicionar Estado Hover

Adicione um estado hover aos inputs:
```css
input:hover {
  border-color: var(--color-brand-mid);
}
```

Teste passando o mouse sobre os inputs. O que você observa?

**Resposta:** Borda muda de cor ao passar o mouse, dando feedback visual.

---

## 📊 Comparação: Antes e Depois

### ❌ Antes (Sem Estilos)
- Inputs com estilo padrão do navegador
- Sem feedback visual de foco
- Placeholders com cor padrão
- Layout inconsistente

### ✅ Depois (Com Estilos)
- Inputs com design dark mode consistente
- Feedback visual claro no foco (borda azul + glow)
- Placeholders estilizados
- Layout responsivo e organizado

---

## 🚀 Próximos Passos

Agora que os inputs básicos estão estilizados, podemos:

1. **Adicionar estado de erro**
   - Borda vermelha
   - Mensagem de erro
   - Ícone de alerta

2. **Implementar validação**
   - Campos obrigatórios
   - Validação em tempo real
   - Feedback visual

3. **Adicionar mais campos**
   - Seletores (select)
   - File input
   - Checkboxes e radios

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Por que agrupar seletores CSS?
- [ ] O que são pseudo-elementos (`::placeholder`)?
- [ ] O que são pseudo-classes (`:focus`)?
- [ ] Como funciona `box-shadow` para criar glow?
- [ ] Por que usar `transition`?
- [ ] Quando usar Grid vs Flexbox?
- [ ] Por que `outline: none` + feedback visual alternativo?

---

## 📚 Recursos Adicionais

- **CSS Selectors:** https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
- **Pseudo-classes:** https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes
- **Pseudo-elementos:** https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements
- **Box Shadow:** https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow
- **CSS Transitions:** https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Estilização base de inputs (reutilização)
- ✅ Estados visuais (`:focus` com borda e glow)
- ✅ Pseudo-elementos (`::placeholder`)
- ✅ Transitions para animações suaves
- ✅ Layout responsivo com Grid
- ✅ Boas práticas de CSS

**Isso é conhecimento fundamental para criar formulários profissionais e acessíveis!** 🚀

---

**Próxima Task:** Implementar estado de erro e validação visual.

