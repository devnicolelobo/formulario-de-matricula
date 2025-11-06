# 📚 Task 10: Componente Segmented Control (Seleção de Tipo)

## 🎯 Objetivo

Implementar o Segmented Control para a seleção do Tipo de Evento, utilizando `input[type="radio"]` agrupados e escondidos. A estratégia é criar um visual de botões unidos, aplicando a cor de destaque principal da marca (`var(--brand-mid)`) ao item selecionado e garantindo que os cantos arredondados sejam aplicados apenas nas extremidades corretas do grupo.

---

## ✅ O Que Foi Implementado

### 1. Estrutura HTML

```html
<div class="input-wrapper">
  <label>Tipo</label>
  <div class="segmented-control">
    <input type="radio" id="event-type-presencial" name="event-type" value="presencial" checked>
    <label for="event-type-presencial" class="segment">
      <i data-lucide="building"></i>
      <span>Presencial</span>
    </label>

    <input type="radio" id="event-type-online" name="event-type" value="online">
    <label for="event-type-online" class="segment">
      <i data-lucide="video"></i>
      <span>Online</span>
    </label>
  </div>
</div>
```

**Características:**
- ✅ Container `.segmented-control` agrupa os segmentos
- ✅ Radio buttons escondidos (mas funcionais)
- ✅ Labels clicáveis com ícones e texto
- ✅ Ícones Lucide (building para Presencial, video para Online)

---

### 2. Estilos do Container

```css
.segmented-control {
  display: flex;
  background: var(--shape-button);
  border-radius: var(--radius-md);
  padding: 2px;
  gap: 2px;
}
```

**Características:**
- ✅ **Flexbox:** Alinha segmentos horizontalmente
- ✅ **Background:** Fundo cinza escuro (container)
- ✅ **Padding:** 2px cria "moldura" ao redor dos segmentos
- ✅ **Gap:** 2px separa visualmente os segmentos
- ✅ **Border-radius:** Cantos arredondados no container externo

---

### 3. Estilos dos Segmentos

```css
.segment {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--spacing-xs);
  flex: 1;
  padding: var(--spacing-sm) var(--spacing-md);
  background: transparent;
  border-radius: var(--radius-sm);
  color: var(--text-body);
  cursor: pointer;
  transition: all var(--transition-base);
}
```

**Características:**
- ✅ **Flex:** Alinha ícone e texto
- ✅ **flex: 1:** Segmentos ocupam espaço igual
- ✅ **Background transparent:** Fundo transparente (padrão)
- ✅ **Border-radius:** Cantos arredondados (será sobrescrito)

---

### 4. Gestão de Border-Radius nas Extremidades

```css
/* Primeiro segmento - apenas esquerda */
.segmented-control .segment:first-of-type {
  border-top-left-radius: var(--radius-sm);
  border-bottom-left-radius: var(--radius-sm);
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

/* Último segmento - apenas direita */
.segmented-control .segment:last-of-type {
  border-top-right-radius: var(--radius-sm);
  border-bottom-right-radius: var(--radius-sm);
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
```

**Resultado:**
- ✅ Primeiro segmento: cantos arredondados apenas à esquerda
- ✅ Último segmento: cantos arredondados apenas à direita
- ✅ Segmentos do meio: cantos retos (se houver mais de 2)

**Visual:**
```
┌─────────────┬─────────────┐
│  Presencial │   Online    │
└─────────────┴─────────────┘
  ↑            ↑
  Esquerda    Direita
  arredondada arredondada
```

---

### 5. Estado Ativo (Checked)

```css
input[type="radio"]:checked + .segment {
  background: var(--brand-mid);
  color: var(--text-heading);
}
```

**Características:**
- ✅ **Background:** Azul médio (`#3487CF`) quando selecionado
- ✅ **Color:** Texto branco para contraste
- ✅ **Seletor:** `:checked +` detecta radio marcado

---

### 6. Estados Hover

```css
.segment:hover {
  background: var(--shape-hover);
}

input[type="radio"]:checked + .segment:hover {
  background: var(--color-brand-light);
}
```

**Comportamento:**
- **Não selecionado:** Fundo cinza mais claro ao passar mouse
- **Selecionado:** Fundo azul mais claro ao passar mouse

---

## 🎓 Conceitos Aprendidos

### 1. Segmented Control - O Que É?

**Definição:**
- Componente de UI que divide opções em segmentos visuais
- Apenas uma opção pode estar selecionada
- Visual de botões unidos/contíguos

**Uso comum:**
- Seleção de tipo (Presencial/Online)
- Filtros (Todos/Ativos/Inativos)
- Modos de visualização (Lista/Grid)

**Exemplos reais:**
- iOS Settings (Wi-Fi, Bluetooth)
- Tabs em aplicativos
- Filtros de busca

---

### 2. Seletores `:first-of-type` e `:last-of-type`

**O que fazem?**
- `:first-of-type` - Seleciona o primeiro elemento do tipo
- `:last-of-type` - Seleciona o último elemento do tipo

**Sintaxe:**
```css
.segment:first-of-type {
  /* Estilos para primeiro segmento */
}

.segment:last-of-type {
  /* Estilos para último segmento */
}
```

**Diferença de `:first-child`:**
- `:first-child` - Primeiro filho (qualquer tipo)
- `:first-of-type` - Primeiro elemento do tipo específico ✅

**Exemplo:**
```html
<div>
  <span>Texto</span>  <!-- :first-child -->
  <label class="segment">1</label>  <!-- :first-of-type para .segment -->
  <label class="segment">2</label>
</div>
```

---

### 3. Border-Radius Individual por Canto

**Sintaxe completa:**
```css
border-radius: top-left top-right bottom-right bottom-left;
```

**Exemplo:**
```css
border-radius: 8px 0 0 8px; /* Esquerda arredondada */
border-radius: 0 8px 8px 0; /* Direita arredondada */
```

**Propriedades individuais:**
```css
border-top-left-radius: 8px;
border-top-right-radius: 0;
border-bottom-right-radius: 0;
border-bottom-left-radius: 8px;
```

**No nosso caso:**
- Primeiro segmento: `border-radius: 8px 0 0 8px;`
- Último segmento: `border-radius: 0 8px 8px 0;`

---

### 4. Padding no Container para "Moldura"

```css
.segmented-control {
  padding: 2px;
  gap: 2px;
}
```

**O que faz?**
- **Padding:** Cria espaço entre container e segmentos
- **Gap:** Cria espaço entre segmentos
- **Resultado:** Visual de "moldura" ao redor dos segmentos

**Visual:**
```
┌─────────────────────────┐ ← Container (padding: 2px)
│ ┌─────────┬─────────┐  │
│ │ Seg 1   │ Seg 2   │  │ ← Segmentos (gap: 2px)
│ └─────────┴─────────┘  │
└─────────────────────────┘
```

---

### 5. Flex: 1 para Distribuição Igual

```css
.segment {
  flex: 1;
}
```

**O que faz?**
- Segmentos ocupam espaço igual
- Distribui espaço disponível uniformemente
- Adapta-se automaticamente ao tamanho do container

**Equivalente a:**
```css
flex-grow: 1;
flex-shrink: 1;
flex-basis: 0;
```

**Resultado:** Ambos os segmentos têm exatamente 50% da largura.

---

### 6. Background Transparent vs Colored

**Estado padrão:**
```css
background: transparent;
```

**Estado ativo:**
```css
background: var(--brand-mid);
```

**Por quê?**
- Transparent permite ver o fundo do container
- Quando ativo, segmento se destaca com cor
- Cria contraste visual claro

---

## 🔍 Detalhes Técnicos

### Por Que Padding de 2px?

**Efeito visual:**
- Cria "moldura" sutil ao redor dos segmentos
- Separa visualmente container de segmentos
- Dá profundidade ao componente

**Se fosse 0:**
- Segmentos colariam nas bordas
- Visual menos polido
- Sem separação visual

---

### Estrutura do Seletor `:checked +`

**HTML:**
```html
<input type="radio" id="presencial" checked>
<label for="presencial" class="segment">Presencial</label>
```

**CSS:**
```css
input[type="radio"]:checked + .segment {
  background: var(--brand-mid);
}
```

**Fluxo:**
1. Input está checked? (`:checked`)
2. Se sim, seleciona próximo elemento (`+`)
3. Aplica estilos no label

**Importante:** Input e label devem ser irmãos adjacentes!

---

### Por Que Gap de 2px?

**Efeito:**
- Cria separação visual entre segmentos
- Mantém unidade visual (não separa demais)
- Visual limpo e profissional

**Se fosse maior:**
- Segmentos pareceriam desconectados
- Perderia visual de "unidos"

**Se fosse 0:**
- Segmentos colariam
- Sem separação visual

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Border-Radius Apenas nas Extremidades

```css
.segment:first-of-type {
  border-radius: 8px 0 0 8px; /* Apenas esquerda */
}

.segment:last-of-type {
  border-radius: 0 8px 8px 0; /* Apenas direita */
}
```

**Benefício:** Visual de botões unidos, não separados.

---

### 2. ✅ Flex: 1 para Distribuição Igual

```css
.segment {
  flex: 1;
}
```

**Benefício:** Segmentos sempre têm tamanho igual, independente do conteúdo.

---

### 3. ✅ Transitions Suaves

```css
transition: all var(--transition-base);
```

**Benefício:** Mudança de estado suave e profissional.

---

### 4. ✅ Estados Hover Diferentes

```css
.segment:hover { /* Não selecionado */ }
input:checked + .segment:hover { /* Selecionado */ }
```

**Benefício:** Feedback visual claro em cada estado.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Adicionar Terceiro Segmento

Adicione um terceiro segmento "Híbrido":
```html
<input type="radio" id="event-type-hybrid" name="event-type" value="hybrid">
<label for="event-type-hybrid" class="segment">Híbrido</label>
```

O que acontece com os border-radius? Precisam ajustar?

**Resposta:** 
- Primeiro: border-radius à esquerda
- Meio: sem border-radius (retos)
- Último: border-radius à direita

---

### Exercício 2: Modificar Cores

Mude a cor do estado ativo para:
```css
background: var(--color-accent-pink);
```

O que mudou visualmente?

**Resposta:** Segmento selecionado fica rosa em vez de azul.

---

### Exercício 3: Entender Flex: 1

Remova `flex: 1` e adicione `width: 50%`:
```css
.segment {
  width: 50%;
  /* flex: 1; removido */
}
```

Funciona igual? Qual a diferença?

**Resposta:** 
- `flex: 1` é mais flexível (adapta-se melhor)
- `width: 50%` é fixo (pode quebrar em alguns casos)

---

## 📊 Comparação: Antes e Depois

### ❌ Sem Segmented Control
- Radio buttons padrão do navegador
- Visual inconsistente
- Difícil de usar

### ✅ Com Segmented Control
- Visual moderno e unificado
- Feedback visual claro
- UX profissional
- Design system seguido

---

## 🚀 Próximos Passos

Agora que o segmented control está implementado, podemos:

1. **Adicionar mais opções**
   - Se necessário, adicionar mais segmentos
   - Manter mesma estrutura

2. **Conectar com lógica**
   - Mostrar/ocultar campos baseado no tipo
   - Validar campos específicos por tipo

3. **Melhorar acessibilidade**
   - Adicionar aria-labels
   - Melhorar navegação por teclado

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] O que é um Segmented Control?
- [ ] Como funciona `:first-of-type` e `:last-of-type`?
- [ ] Por que usar `flex: 1` nos segmentos?
- [ ] Como aplicar border-radius apenas nas extremidades?
- [ ] Por que usar padding no container?
- [ ] Como funciona o seletor `:checked +`?

---

## 📚 Recursos Adicionais

- **CSS Selectors:** https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
- **Flexbox:** https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- **Border Radius:** https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius
- **Segmented Control Pattern:** https://www.nngroup.com/articles/segmented-controls/

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Como criar Segmented Control customizado
- ✅ Gestão de border-radius nas extremidades
- ✅ Seletores `:first-of-type` e `:last-of-type`
- ✅ Flex: 1 para distribuição igual
- ✅ Padding e gap para visual de moldura
- ✅ Estados hover e checked

**Isso é conhecimento fundamental para criar componentes de seleção modernos e profissionais!** 🚀

---

**Próxima Task:** Implementar validação de formulário e estados de erro.

