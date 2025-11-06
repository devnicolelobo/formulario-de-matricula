# 📚 Task 09: Componentes Seleção de Cor e Tema

## 🎯 Objetivo

Implementar os componentes de seleção de cor principal (color swatches) e seleção de tema do evento (theme grid), permitindo que o usuário personalize visualmente o convite. Os componentes devem seguir o style guide com estados visuais claros (default, hover, selected).

---

## ✅ O Que Foi Implementado

### 1. Estrutura HTML - Seleção de Cor

```html
<div class="input-wrapper">
  <label>Cor principal</label>
  <div class="color-selector">
    <input type="radio" id="color-blue" name="primary-color" value="blue" checked>
    <label for="color-blue" class="color-swatch" 
           style="background-color: var(--color-brand-light);" 
           title="Azul claro"></label>
    <!-- Mais 9 cores... -->
  </div>
</div>
```

**10 cores implementadas:**
1. Azul claro (brand-light) - Padrão
2. Roxo (accent-purple)
3. Fúcsia (accent-fuschia)
4. Rosa (accent-pink)
5. Laranja (accent-orange)
6. Amarelo (accent-yellow)
7. Verde limão (accent-lime)
8. Verde (accent-green)
9. Ciano (accent-cyan)
10. Azul marinho (accent-navy)

---

### 2. Estrutura HTML - Grid de Temas

```html
<div class="input-wrapper">
  <label>Tema do evento</label>
  <div class="theme-grid">
    <input type="radio" id="theme-birthday" name="event-theme" value="birthday" checked>
    <label for="theme-birthday" class="theme-card">
      <div class="theme-image">🎂</div>
      <span class="theme-name">Aniversário</span>
    </label>
    <!-- Mais 11 temas... -->
  </div>
</div>
```

**12 temas implementados:**
1. Aniversário 🎂 - Padrão
2. Infantil 🎈
3. Formatura 🎓
4. Casamento 💍
5. Chá de bebê 👶
6. Chá de panela 🍳
7. Carnaval 🎭
8. Páscoa 🥚
9. São João 🔥
10. Halloween 🎃
11. Natal 🎄
12. Outro 🎉

---

### 3. Estilos - Color Swatches

```css
.color-selector {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-sm);
}

.color-swatch {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 3px solid var(--input-stroke);
  cursor: pointer;
  transition: all var(--transition-base);
}
```

**Estados:**
- **Default:** Borda cinza (`--input-stroke`)
- **Hover:** Borda mais clara, escala 1.1x
- **Selected:** Borda azul (`--color-brand-light`) + box-shadow (glow duplo) + escala 1.15x

---

### 4. Estilos - Theme Grid

```css
.theme-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
  gap: var(--spacing-md);
}

.theme-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: var(--spacing-md);
  background: var(--shape-button);
  border: 2px solid var(--input-stroke);
  border-radius: var(--radius-md);
  cursor: pointer;
}
```

**Estados:**
- **Default:** Borda cinza, fundo cinza escuro
- **Hover:** Borda mais clara, fundo mais claro, elevação (`translateY(-2px)`)
- **Selected:** Borda azul + box-shadow + nome em azul

---

## 🎓 Conceitos Aprendidos

### 1. CSS Grid com `auto-fill` e `minmax()`

```css
grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
```

**O que faz?**
- `repeat()`: Repete o padrão
- `auto-fill`: Cria quantas colunas couberem
- `minmax(100px, 1fr)`: Mínimo 100px, máximo flexível

**Resultado:**
- ✅ Grid responsivo automaticamente
- ✅ Cards se ajustam ao espaço disponível
- ✅ Mínimo de 100px garante legibilidade

**Exemplo prático:**
- Container 500px → 5 colunas (100px cada)
- Container 300px → 3 colunas (100px cada)
- Container 150px → 1 coluna (100px, não quebra)

---

### 2. Box Shadow Múltiplo (Glow Duplo)

```css
box-shadow: 
  0 0 0 3px rgba(89, 178, 255, 0.3),  /* Glow interno */
  0 0 0 6px rgba(89, 178, 255, 0.15); /* Glow externo */
```

**O que faz?**
- Cria dois "anéis" de brilho ao redor do elemento
- Primeiro anel: 3px, 30% opacidade
- Segundo anel: 6px, 15% opacidade

**Resultado:** Efeito de "glow" profissional, como no style guide.

**Sintaxe:**
```css
box-shadow: sombra1, sombra2, sombra3;
```

Cada sombra é independente e pode ser combinada.

---

### 3. Transform Scale

```css
transform: scale(1.1);  /* Hover */
transform: scale(1.15); /* Selected */
```

**O que faz?**
- Aumenta o tamanho do elemento
- `scale(1.1)` = 110% do tamanho original
- `scale(1.15)` = 115% do tamanho original

**Por que usar?**
- ✅ Feedback visual claro
- ✅ Performance melhor que mudar width/height
- ✅ Funciona bem com transitions

**Comparação:**
```css
/* ❌ Pode causar reflow */
width: 44px; /* era 40px */

/* ✅ Melhor performance */
transform: scale(1.1); /* 40px * 1.1 = 44px */
```

---

### 4. Transform TranslateY (Elevação)

```css
transform: translateY(-2px);
```

**O que faz?**
- Move elemento 2px para cima
- Cria efeito de "elevação" ou "flutuação"

**Uso comum:**
- Hover em cards
- Botões pressionados
- Feedback visual de interação

**Resultado:** Card parece "levantar" ao passar o mouse.

---

### 5. Flexbox Wrap

```css
display: flex;
flex-wrap: wrap;
gap: var(--spacing-sm);
```

**O que faz?**
- `flex-wrap: wrap`: Permite quebra de linha
- Itens que não cabem vão para próxima linha
- `gap`: Espaçamento consistente entre itens

**Uso:** Perfeito para listas de itens que precisam quebrar linha.

**Comparação:**
```css
/* Sem wrap - itens comprimem */
flex-wrap: nowrap;

/* Com wrap - itens quebram linha ✅ */
flex-wrap: wrap;
```

---

### 6. Inline Styles para Cores Dinâmicas

```html
<label class="color-swatch" 
       style="background-color: var(--color-brand-light);">
```

**Por que inline style?**
- Cada swatch tem cor diferente
- Não precisamos criar 10 classes CSS
- Usa variáveis CSS do sistema

**Alternativa (mais verbosa):**
```css
.color-swatch-blue { background: var(--color-brand-light); }
.color-swatch-purple { background: var(--color-accent-purple); }
/* ... 10 classes ... */
```

**Inline style é mais prático neste caso!**

---

## 🔍 Detalhes Técnicos

### Por Que Radio Buttons e Não Checkboxes?

**Radio buttons:**
- ✅ Apenas uma cor pode ser selecionada
- ✅ Apenas um tema pode ser selecionado
- ✅ Comportamento nativo correto

**Se fossem checkboxes:**
- ❌ Múltiplas cores selecionadas (não faz sentido)
- ❌ Múltiplos temas selecionados (não faz sentido)
- ❌ Comportamento incorreto

**Regra:** Use radio quando apenas uma opção pode ser selecionada.

---

### Estrutura do Seletor `:checked +`

**HTML:**
```html
<input type="radio" id="color-blue" checked>
<label for="color-blue" class="color-swatch"></label>
```

**CSS:**
```css
input[type="radio"]:checked + .color-swatch {
  /* Estilos quando radio está checked */
}
```

**Fluxo:**
1. Input está checked? (`:checked`)
2. Se sim, seleciona próximo elemento (`+`)
3. Aplica estilos no label

**Importante:** Input e label devem ser irmãos adjacentes!

---

### Cálculo do Box Shadow Duplo

**Glow interno:**
```css
0 0 0 3px rgba(89, 178, 255, 0.3)
```
- Offset: 0, 0 (sem deslocamento)
- Blur: 0 (sem desfoque)
- Spread: 3px (expansão de 3px)
- Cor: Azul com 30% opacidade

**Glow externo:**
```css
0 0 0 6px rgba(89, 178, 255, 0.15)
```
- Spread: 6px (expansão maior)
- Cor: Azul com 15% opacidade (mais sutil)

**Resultado:** Dois anéis concêntricos de brilho.

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Grid Responsivo com auto-fill

```css
grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
```

**Benefício:** Adapta-se automaticamente a qualquer largura.

---

### 2. ✅ Estados Visuais Claros

```css
/* Default */
border-color: var(--input-stroke);

/* Hover */
border-color: var(--text-body);
transform: scale(1.1);

/* Selected */
border-color: var(--color-brand-light);
box-shadow: /* glow duplo */;
```

**Benefício:** Feedback visual claro em cada estado.

---

### 3. ✅ Transitions Suaves

```css
transition: all var(--transition-base);
```

**Benefício:** Animações profissionais.

---

### 4. ✅ Acessibilidade Mantida

```html
<input type="radio" id="color-blue" name="primary-color">
<label for="color-blue" class="color-swatch" title="Azul claro">
```

**Benefício:** Screen readers e navegação por teclado funcionam.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Entender auto-fill

Mude o grid para:
```css
grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
```

O que acontece? Quantas colunas aparecem?

**Resposta:** Cards ficam maiores (mínimo 150px), menos colunas cabem.

---

### Exercício 2: Modificar Box Shadow

Remova o glow externo:
```css
box-shadow: 0 0 0 3px rgba(89, 178, 255, 0.3);
```

O que mudou visualmente?

**Resposta:** Glow fica menos intenso, apenas um anel.

---

### Exercício 3: Adicionar Nova Cor

Adicione uma 11ª cor (vermelho) no HTML:
```html
<input type="radio" id="color-red" name="primary-color" value="red">
<label for="color-red" class="color-swatch" 
       style="background-color: #FF0000;" 
       title="Vermelho"></label>
```

Funciona automaticamente? Por quê?

**Resposta:** Sim! Os estilos CSS são genéricos, funcionam para qualquer cor.

---

## 📊 Comparação: Antes e Depois

### ❌ Sem Componentes
- Sem personalização visual
- Formulário genérico
- Sem feedback visual de seleção

### ✅ Com Componentes
- Personalização completa (cor + tema)
- Feedback visual claro
- UX profissional
- Design system seguido

---

## 🚀 Próximos Passos

Agora que seleção de cor e tema estão implementados, podemos:

1. **Conectar com preview**
   - Atualizar preview quando cor/tema mudar
   - JavaScript para aplicar estilos dinamicamente

2. **Adicionar mais opções**
   - Mais cores (se necessário)
   - Mais temas (se necessário)

3. **Implementar validação**
   - Garantir que cor e tema sejam selecionados
   - Feedback visual se não selecionado

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Como funciona `repeat(auto-fill, minmax())`?
- [ ] Por que usar radio buttons e não checkboxes?
- [ ] Como criar box-shadow múltiplo (glow duplo)?
- [ ] Por que usar `transform: scale()` em vez de width/height?
- [ ] Como funciona `translateY()` para elevação?
- [ ] Por que usar inline style para cores dos swatches?

---

## 📚 Recursos Adicionais

- **CSS Grid:** https://css-tricks.com/snippets/css/complete-guide-grid/
- **Box Shadow:** https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow
- **Transform:** https://developer.mozilla.org/en-US/docs/Web/CSS/transform
- **Flexbox Wrap:** https://css-tricks.com/almanac/properties/f/flex-wrap/

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Grid responsivo com `auto-fill` e `minmax()`
- ✅ Box-shadow múltiplo para glow duplo
- ✅ Transform scale e translateY para feedback visual
- ✅ Flexbox wrap para listas responsivas
- ✅ Inline styles para valores dinâmicos
- ✅ Estados visuais (default, hover, selected)

**Isso é conhecimento fundamental para criar componentes interativos e responsivos!** 🚀

---

**Próxima Task:** Implementar validação de formulário e estados de erro.

