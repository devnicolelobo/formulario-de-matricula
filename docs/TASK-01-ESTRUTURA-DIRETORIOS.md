# 📚 Task 01: Estrutura de Diretórios e Arquitetura CSS

## 🎯 Objetivo da Task

Definir a estrutura de diretórios do projeto para garantir modularidade e escalabilidade do CSS, seguindo uma arquitetura BEM/SMACSS simplificada. Criar todos os arquivos CSS vazios e configurar o `main.css` para importá-los na ordem correta.

---

## ✅ O Que Foi Feito

### 1. Criação da Estrutura de Pastas

```
formulario-de-matricula/
├── assets/
│   ├── fonts/          # Fontes personalizadas
│   ├── icons/          # Ícones SVG
│   └── images/         # Imagens do projeto
│
├── styles/
│   ├── main.css        # Arquivo principal (importa todos)
│   ├── _config.css     # Variáveis e estilos globais
│   ├── _layout.css     # Estrutura da página
│   └── components/
│       ├── _buttons.css
│       ├── _inputs.css
│       ├── _selectors.css
│       └── _theme.css
│
└── index.html          # HTML principal
```

### 2. Configuração do `main.css`

Criamos o arquivo principal que importa todos os outros na ordem correta:

```css
/* Configuração */
@import url('./_config.css');

/* Layout */
@import url('./_layout.css');

/* Componentes */
@import url('./components/_buttons.css');
@import url('./components/_inputs.css');
@import url('./components/_selectors.css');
@import url('./components/_theme.css');
```

### 3. Documentação do Style Guide

No `_config.css`, documentamos:
- ✅ Todas as cores do projeto (Brand, Accent, Feedback, Input, Shape, Text)
- ✅ Tipografia (Leckerli One, Baloo 2, Open Sans)
- ✅ Especificações de todos os componentes
- ✅ Estrutura completa do layout
- ✅ Variáveis CSS para espaçamento, border-radius e transições

---

## 🎓 Conceitos Aprendidos

### 1. Arquitetura CSS Modular

**O que é?**
Uma forma de organizar CSS dividindo em arquivos menores e específicos, cada um com uma responsabilidade clara.

**Por que usar?**
- ✅ Facilita manutenção
- ✅ Melhora organização
- ✅ Permite trabalho em equipe
- ✅ Torna o código escalável

**Analogia:**
Imagine uma biblioteca. Em vez de ter todos os livros em uma pilha gigante, você organiza por gênero (ficção, não-ficção, etc.). Assim fica fácil encontrar o que precisa!

### 2. SMACSS (Simplificado)

**SMACSS** = Scalable and Modular Architecture for CSS

**Categorias principais:**

| Categoria | Arquivo | Propósito |
|-----------|---------|-----------|
| **Base** | `_config.css` | Reset, variáveis, estilos globais |
| **Layout** | `_layout.css` | Estrutura da página (grid, containers) |
| **Módulos** | `components/` | Componentes reutilizáveis |

**Exemplo prático:**
```css
/* _config.css - BASE */
:root {
  --color-primary: #59B2FF;
}

/* _layout.css - LAYOUT */
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

/* components/_buttons.css - MÓDULO */
.button {
  background-color: var(--color-primary);
}
```

### 3. BEM (Conceito)

**BEM** = Block Element Modifier

**Estrutura:**
- **Block:** Componente independente (`.button`)
- **Element:** Parte do componente (`.button__icon`)
- **Modifier:** Variação do componente (`.button--primary`)

**Exemplo:**
```css
/* Block */
.button { }

/* Element */
.button__icon { }

/* Modifier */
.button--primary { }
.button--primary__icon { }
```

**No nosso projeto:**
Embora não usemos nomenclatura BEM estrita, seguimos o conceito de separar componentes.

### 4. Variáveis CSS (Custom Properties)

**O que são?**
Variáveis que você define uma vez e usa em vários lugares.

**Sintaxe:**
```css
:root {
  --nome-da-variavel: valor;
}

.elemento {
  propriedade: var(--nome-da-variavel);
}
```

**Exemplo real do projeto:**
```css
:root {
  --color-brand-light: #59B2FF;
  --spacing-md: 1.5rem;
}

.button {
  background-color: var(--color-brand-light);
  padding: var(--spacing-md);
}
```

**Vantagens:**
- ✅ Mudança em um lugar afeta todo o projeto
- ✅ Facilita criação de temas (claro/escuro)
- ✅ Código mais limpo e legível

### 5. @import no CSS

**O que é?**
Permite importar um arquivo CSS dentro de outro.

**Sintaxe:**
```css
@import url('./caminho/do/arquivo.css');
```

**Ordem importa!**
```css
/* ✅ CORRETO - Ordem lógica */
@import url('./_config.css');      /* 1. Variáveis primeiro */
@import url('./_layout.css');      /* 2. Layout depois */
@import url('./components.css');   /* 3. Componentes por último */

/* ❌ ERRADO - Componentes precisam das variáveis */
@import url('./components.css');    /* Vai dar erro! */
@import url('./_config.css');
```

**Por quê?**
Os componentes usam variáveis definidas em `_config.css`, então precisam ser importados depois.

### 6. Convenção de Nomenclatura

**Underscore (`_`) no início:**
- `_config.css`
- `_layout.css`

**O que significa?**
Indica que são arquivos "parciais" ou "utilitários" que não devem ser usados diretamente, apenas importados.

**Analogia:**
É como um arquivo "privado" que só é usado internamente pelo `main.css`.

---

## 🔍 Detalhes Técnicos

### Por Que Separar em Múltiplos Arquivos?

**Problema com arquivo único:**
```css
/* styles.css - 2000 linhas! 😱 */
/* Cores */
/* Reset */
/* Layout */
/* Botões */
/* Inputs */
/* ... */
/* Difícil encontrar coisas! */
```

**Solução modular:**
```css
/* _config.css - 100 linhas */
/* _layout.css - 50 linhas */
/* _buttons.css - 80 linhas */
/* _inputs.css - 70 linhas */
/* Fácil encontrar! ✅ */
```

### Ordem de Especificidade CSS

**Regra geral:**
1. Estilos mais genéricos primeiro
2. Estilos mais específicos depois

**No nosso projeto:**
1. `_config.css` → Estilos globais (mais genérico)
2. `_layout.css` → Estrutura (médio)
3. `components/` → Componentes específicos (mais específico)

**Por quê?**
Se você definir `.button` em `_config.css` e depois em `_buttons.css`, o último vai sobrescrever (cascata do CSS).

### Performance e @import

**⚠️ Atenção:**
`@import` pode ter impacto na performance porque:
- Cada `@import` é uma requisição HTTP adicional
- Bloqueia o carregamento da página

**Solução em produção:**
- Use ferramentas de build (Webpack, Vite, etc.)
- Elas combinam todos os arquivos em um só
- Minificam o código
- Resultado: um único arquivo otimizado

**Para desenvolvimento:**
- `@import` é perfeito! Facilita organização
- Browsers modernos lidam bem com isso

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Separação de Responsabilidades

Cada arquivo tem **uma única responsabilidade**:
- `_config.css` → Configurações
- `_layout.css` → Layout
- `_buttons.css` → Botões

**Benefício:** Fácil encontrar onde fazer mudanças.

### 2. ✅ Nomenclatura Descritiva

```css
/* ✅ BOM */
--color-brand-light
--spacing-md
.button-primary

/* ❌ RUIM */
--c1
--s1
.btn1
```

### 3. ✅ Documentação com Comentários

```css
/* ============================================
   BOTÕES - PRIMARY
   ============================================ */
```

Facilita navegação em arquivos grandes.

### 4. ✅ Organização Hierárquica

```
styles/
├── main.css           # Nível raiz
├── _config.css        # Nível raiz
├── _layout.css        # Nível raiz
└── components/        # Subdiretório
    └── _buttons.css   # Componente específico
```

---

## 🚀 Próximos Passos

Agora que a estrutura está pronta, podemos:

1. **Implementar o layout** (`_layout.css`)
   - Grid de duas colunas
   - Containers e espaçamentos

2. **Criar os componentes** (`components/`)
   - Estilizar botões
   - Estilizar inputs
   - Criar seletores

3. **Adicionar variáveis** (`_config.css`)
   - Já temos as cores documentadas
   - Agora vamos usar nas implementações

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Por que separar CSS em múltiplos arquivos?
- [ ] O que é SMACSS e suas categorias?
- [ ] Como funcionam variáveis CSS (`:root`)?
- [ ] Por que a ordem de `@import` importa?
- [ ] O que significa o `_` no início dos arquivos?
- [ ] Qual a diferença entre `_config.css` e `_layout.css`?
- [ ] Por que componentes ficam em uma pasta separada?

---

## 🎯 Exercícios de Fixação

### Exercício 1: Criar Nova Variável

Adicione uma nova variável de cor em `_config.css`:
```css
--color-success: #59FF91;
```

Use ela em um componente (mesmo que ainda não exista).

### Exercício 2: Entender a Ordem

Tente inverter a ordem dos imports no `main.css`. O que acontece? Por quê?

### Exercício 3: Criar Novo Componente

Crie um arquivo `_cards.css` em `components/` e importe no `main.css`. Onde você colocaria estilos de cards de tema?

---

## 📚 Recursos Adicionais

- **SMACSS:** https://smacss.com/
- **BEM:** http://getbem.com/
- **CSS Variables:** https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties
- **CSS @import:** https://developer.mozilla.org/en-US/docs/Web/CSS/@import

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Como estruturar um projeto CSS profissional
- ✅ Conceitos de arquitetura modular (SMACSS)
- ✅ Uso de variáveis CSS
- ✅ Organização de código escalável

**Isso é conhecimento que você vai usar em TODOS os seus projetos futuros!** 🚀

---

**Próxima Task:** Implementar o layout de duas colunas e estrutura HTML básica.

