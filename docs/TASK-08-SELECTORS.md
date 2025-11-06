# 📚 Task 08: Componentes Checkbox e Switch Toggle Customizados

## 🎯 Objetivo

Implementar a estilização customizada dos inputs nativos de checkbox e radio que compõem o Checkbox (Aceite de Termos) e o Switch Toggle (Estilo Escuro/Claro). A estratégia chave é esconder o input nativo e estilizar o `<label>` e pseudoelementos (`::before`, `::after`), utilizando a pseudoclasse `:checked` para o feedback visual.

---

## ✅ O Que Foi Implementado

### 1. Estrutura HTML - Checkbox

```html
<label class="checkbox-wrapper">
  <input type="checkbox" id="terms" name="terms" required>
  <span class="checkbox-label">
    Li e concordo com os 
    <a href="#" class="link">Termos e Condições</a> 
    e com a 
    <a href="#" class="link">Política de Privacidade</a>
  </span>
</label>
```

**Características:**
- ✅ Input nativo escondido (mas funcional)
- ✅ Label clicável que envolve tudo
- ✅ Links dentro do texto do checkbox

---

### 2. Estrutura HTML - Switch Toggle

```html
<label class="switch-toggle">
  <input type="checkbox" id="style-toggle" name="style-toggle">
  <span class="switch-slider"></span>
  <span class="switch-label">Escuro</span>
</label>
```

**Características:**
- ✅ Input nativo escondido
- ✅ Trilha visual (`.switch-slider`)
- ✅ Thumb (círculo que desliza) criado com `::after`
- ✅ Label de texto ao lado

---

### 3. Esconder Inputs Nativos

```css
input[type="checkbox"],
input[type="radio"] {
  opacity: 0;
  position: absolute;
  width: 0;
  height: 0;
  margin: 0;
  padding: 0;
}
```

**Por que esconder assim?**
- ✅ **Acessibilidade mantida:** Input ainda existe no DOM
- ✅ **Funcionalidade preservada:** Tab, screen readers funcionam
- ✅ **Visual customizado:** Podemos criar nosso próprio design

**Alternativas (não recomendadas):**
```css
/* ❌ RUIM - Remove do DOM */
display: none; /* Screen readers não veem */

/* ❌ RUIM - Visível mas quebrado */
visibility: hidden; /* Ainda ocupa espaço */
```

---

### 4. Checkbox Customizado

#### Estado Unchecked
```css
.checkbox-label::before {
  content: '';
  display: inline-block;
  width: 20px;
  height: 20px;
  background: var(--input-base);
  border: 2px solid var(--input-stroke);
  border-radius: var(--radius-sm);
}
```

#### Estado Checked
```css
input[type="checkbox"]:checked + .checkbox-label::before {
  background: var(--color-brand-light);
  border-color: var(--color-brand-light);
  background-image: url("data:image/svg+xml,..."); /* Ícone de check */
}
```

**Como funciona:**
- `::before` cria o quadrado visual
- `:checked` detecta quando input está marcado
- `+` (adjacent sibling) seleciona o label após o input checked
- SVG inline cria o ícone de check

---

### 5. Switch Toggle Customizado

#### Trilha (Corpo do Switch)
```css
.switch-slider {
  position: relative;
  width: 48px;
  height: 24px;
  background: var(--shape-button);
  border-radius: 12px;
}
```

#### Thumb (Círculo que Desliza)
```css
.switch-slider::after {
  content: '';
  position: absolute;
  top: 2px;
  left: 2px;
  width: 20px;
  height: 20px;
  background: var(--text-body);
  border-radius: 50%;
  transition: transform var(--transition-base);
}
```

#### Estado Checked (Thumb Move)
```css
input[type="checkbox"]:checked + .switch-slider::after {
  transform: translateX(24px);
  background: white;
}
```

**Como funciona:**
- `::after` cria o círculo (thumb)
- `translateX(24px)` move o thumb para direita
- Trilha muda de cor quando checked

---

## 🎓 Conceitos Aprendidos

### 1. Pseudo-elementos - `::before` e `::after`

**O que são?**
- Elementos virtuais criados via CSS
- Não existem no HTML
- Podem ser estilizados como elementos normais

**Sintaxe:**
```css
.elemento::before {
  content: ''; /* OBRIGATÓRIO - mesmo que vazio */
  /* estilos */
}
```

**Uso comum:**
- `::before` - Conteúdo antes do elemento
- `::after` - Conteúdo depois do elemento

**No nosso caso:**
- Checkbox: `::before` cria o quadrado
- Switch: `::after` cria o thumb

---

### 2. Pseudo-classes - `:checked`

**O que são?**
- Estados especiais de elementos
- Aplicadas automaticamente pelo navegador
- Não precisam ser adicionadas no HTML

**Estados comuns:**
- `:checked` - Checkbox/radio selecionado
- `:hover` - Mouse sobre o elemento
- `:focus` - Elemento recebeu foco
- `:disabled` - Elemento desabilitado

**Exemplo:**
```css
input:checked + label {
  /* Estilos quando input está marcado */
}
```

---

### 3. Seletores Adjacentes - `+`

**O que faz?**
- Seleciona elemento imediatamente após outro
- Deve ser irmão direto (mesmo nível)

**Sintaxe:**
```css
elemento1 + elemento2 {
  /* Estilos para elemento2 que vem logo após elemento1 */
}
```

**Exemplo prático:**
```html
<input type="checkbox" id="test">
<label for="test">Texto</label>
```

```css
input:checked + label {
  /* Seleciona o label que vem logo após o input checked */
}
```

**Outros seletores:**
- `+` - Irmão adjacente (logo após)
- `~` - Irmão geral (qualquer irmão após)
- `>` - Filho direto
- ` ` (espaço) - Descendente (qualquer nível)

---

### 4. Transform - `translateX()`

**O que faz?**
- Move elemento horizontalmente
- Não afeta layout (não empurra outros elementos)
- Performance melhor que `left`/`right`

**Sintaxe:**
```css
transform: translateX(24px); /* Move 24px para direita */
transform: translateY(10px);  /* Move 10px para baixo */
transform: translate(24px, 10px); /* Move X e Y */
```

**Por que usar?**
- ✅ Animações mais suaves
- ✅ Não causa reflow (melhor performance)
- ✅ Funciona bem com transitions

**Comparação:**
```css
/* ❌ Pode causar reflow */
left: 24px;

/* ✅ Melhor performance */
transform: translateX(24px);
```

---

### 5. SVG Inline em CSS (Data URI)

**Checkbox checked usa SVG inline:**
```css
background-image: url("data:image/svg+xml,%3Csvg...%3E");
```

**O que é?**
- SVG codificado diretamente no CSS
- Não precisa de arquivo externo
- Funciona como imagem de fundo

**Vantagens:**
- ✅ Sem requisição HTTP adicional
- ✅ Escalável (SVG)
- ✅ Fácil de customizar

**Desvantagens:**
- ❌ Código longo no CSS
- ❌ Difícil de ler

**Alternativa:**
- Usar ícone de fonte (Lucide, Font Awesome)
- Usar arquivo SVG externo

---

### 6. User Select - `user-select: none`

```css
user-select: none;
```

**O que faz?**
- Impede seleção de texto
- Melhor UX em elementos interativos
- Evita seleção acidental ao clicar

**Valores:**
- `none` - Não pode selecionar
- `auto` - Seleção normal (padrão)
- `all` - Seleciona tudo ao clicar

---

## 🔍 Detalhes Técnicos

### Por Que Esconder Input e Não Remover?

**Abordagem correta:**
```css
opacity: 0;
position: absolute;
```

**Por quê?**
- ✅ Input ainda existe no DOM
- ✅ Screen readers podem acessar
- ✅ Navegação por teclado funciona
- ✅ Validação HTML funciona

**Se removêssemos:**
```css
display: none; /* ❌ RUIM */
```
- ❌ Screen readers não veem
- ❌ Acessibilidade quebrada
- ❌ Validação não funciona

---

### Estrutura do Seletor `:checked +`

**HTML:**
```html
<input type="checkbox" id="test">
<label for="test">Texto</label>
```

**CSS:**
```css
input:checked + label {
  /* Seleciona label que vem logo após input checked */
}
```

**Fluxo:**
1. Input está checked? (`:checked`)
2. Se sim, seleciona o próximo elemento (`+`)
3. Aplica estilos no label

**Importante:** Input e label devem ser irmãos adjacentes!

---

### Cálculo do `translateX` no Switch

**Dimensões:**
- Trilha: 48px de largura
- Thumb: 20px de largura
- Padding: 2px de cada lado

**Cálculo:**
```
Posição inicial: left: 2px
Posição final: 48px - 20px - 2px = 26px
Movimento: 26px - 2px = 24px
```

**Resultado:**
```css
transform: translateX(24px);
```

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Acessibilidade Mantida

```css
opacity: 0; /* Esconde visualmente */
position: absolute; /* Remove do fluxo */
/* Mas input ainda existe no DOM! */
```

**Benefício:** Screen readers e navegação por teclado funcionam.

---

### 2. ✅ Transitions Suaves

```css
transition: transform var(--transition-base);
transition: background-color var(--transition-base);
```

**Benefício:** Animações profissionais e suaves.

---

### 3. ✅ Estados Hover

```css
.checkbox-wrapper:hover .checkbox-label::before {
  border-color: var(--color-brand-light);
}
```

**Benefício:** Feedback visual antes de clicar.

---

### 4. ✅ Estrutura Semântica

```html
<label class="checkbox-wrapper">
  <input type="checkbox">
  <span class="checkbox-label">Texto</span>
</label>
```

**Benefício:** HTML semântico e acessível.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Entender Pseudo-elementos

Adicione um `::after` no checkbox que mostra um tooltip:
```css
.checkbox-label::after {
  content: 'Campo obrigatório';
  /* estilos do tooltip */
}
```

O que acontece? Onde aparece?

**Resposta:** Aparece após o texto do label, criando um tooltip visual.

---

### Exercício 2: Modificar Switch

Mude o tamanho do switch:
```css
.switch-slider {
  width: 60px; /* era 48px */
  height: 30px; /* era 24px */
}
```

Ajuste o `translateX` para funcionar corretamente. Qual o novo valor?

**Resposta:** 
- Novo cálculo: 60px - 20px - 2px = 38px
- `transform: translateX(38px);`

---

### Exercício 3: Adicionar Estado Disabled

Crie estilos para checkbox desabilitado:
```css
input[type="checkbox"]:disabled + .checkbox-label::before {
  opacity: 0.5;
  cursor: not-allowed;
}
```

Teste com: `<input type="checkbox" disabled>`

**O que você observa?**
- Checkbox fica com aparência desabilitada
- Cursor muda para "not-allowed"

---

## 📊 Comparação: Nativo vs Customizado

### ❌ Input Nativo
- Aparência limitada pelo navegador
- Difícil customizar
- Inconsistente entre navegadores
- Não segue design system

### ✅ Input Customizado
- Design totalmente controlado
- Consistente em todos navegadores
- Segue design system
- Acessibilidade mantida

---

## 🚀 Próximos Passos

Agora que checkbox e switch estão implementados, podemos:

1. **Adicionar mais checkboxes**
   - Aceitar e-mails de marketing
   - Aceitar SMS de marketing

2. **Implementar radio buttons**
   - Tipo de evento (Presencial/Online)
   - Mesma técnica de customização

3. **Adicionar validação visual**
   - Checkbox obrigatório não marcado
   - Feedback de erro

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Por que esconder input com `opacity: 0` e não `display: none`?
- [ ] O que são pseudo-elementos (`::before`, `::after`)?
- [ ] Como funciona o seletor `:checked +`?
- [ ] Por que usar `transform: translateX()` em vez de `left`?
- [ ] Como funciona SVG inline em CSS (data URI)?
- [ ] Por que usar `user-select: none`?

---

## 📚 Recursos Adicionais

- **Pseudo-elementos:** https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements
- **Pseudo-classes:** https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes
- **CSS Selectors:** https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
- **Transform:** https://developer.mozilla.org/en-US/docs/Web/CSS/transform
- **Accessibility:** https://www.w3.org/WAI/tutorials/forms/

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Como esconder inputs nativos mantendo acessibilidade
- ✅ Uso de pseudo-elementos (`::before`, `::after`)
- ✅ Pseudo-classes (`:checked`, `:hover`)
- ✅ Seletores adjacentes (`+`)
- ✅ Transform para animações (`translateX`)
- ✅ SVG inline em CSS
- ✅ Criação de componentes customizados

**Isso é conhecimento fundamental para criar componentes interativos e acessíveis!** 🚀

---

**Próxima Task:** Implementar seletores de cor e temas de evento.

