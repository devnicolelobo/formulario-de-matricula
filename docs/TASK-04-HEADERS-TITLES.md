# 📚 Task 04: Estilização do Header Lateral e Títulos do Formulário

## 🎯 Objetivo
Aplicar as variáveis de tipografia e cores para estilizar o painel lateral de preview e os títulos das seções do formulário, mantendo a hierarquia do style guide.

---

## ✅ O que foi implementado

### 1) Estrutura HTML do Header (Painel Lateral)
```html
<div class="preview-panel">
  <header class="preview-header">
    <h1 class="logo-title">Festivite</h1>
    <p class="logo-subtitle">Crie um convite digital para o seu evento</p>
  </header>

  <div class="preview-cover" aria-label="Preview de capa">Imagem de capa</div>
</div>
```

- `.logo-title`: usa a fonte display (Leckerli One) — destaque visual do branding
- `.logo-subtitle`: usa a fonte body (Open Sans) — apoio/descrição

### 2) Estrutura dos Títulos de Seção no Formulário
```html
<fieldset class="form-section">
  <legend class="section-title">
    <i data-lucide="calendar"></i>
    <span>Sobre o evento</span>
  </legend>
  <!-- Campos da seção -->
</fieldset>
```

- `<fieldset>` agrupa campos semanticamente
- `<legend>` é o título da seção (acessível para screen readers)
- Ícones via Lucide (SVG), alinhados ao texto

### 3) Estilos aplicados no `_layout.css`
```css
/* Header lateral */
.preview-header { display: grid; gap: var(--spacing-xs); margin-bottom: var(--spacing-lg); }
.logo-title { font-family: var(--font-display); color: var(--text-heading); font-size: 2.5rem; line-height: 1.1; }
.logo-subtitle { font-family: var(--font-body); color: var(--text-body); font-size: 0.9375rem; }

/* Seções do formulário */
.form-section { border: 0; margin-top: var(--spacing-lg); }
.section-title { display: flex; align-items: center; gap: var(--spacing-sm); font-family: var(--font-heading); color: var(--text-heading); margin-bottom: var(--spacing-sm); }
.section-title svg { width: 20px; height: 20px; stroke: var(--brand-mid); }
```

### 4) Lucide Icons
Adicionamos o script para renderizar os ícones:
```html
<script src="https://unpkg.com/lucide@latest"></script>
<script> if (window.lucide) { lucide.createIcons(); } </script>
```

---

## 🎓 Conceitos aprendidos

- Hierarquia tipográfica com tokens: `--font-display` > `--font-heading` > `--font-body`
- Uso semântico de `<fieldset>` e `<legend>`
- Alinhamento de ícone + texto com `display: flex` e `gap`
- Ícones como SVG (Lucide) com stroke customizável via CSS

---

## 🧪 Exercícios
1. Troque o ícone da seção para `paintbrush` e ajuste a cor com `stroke: var(--color-brand-light)`.
2. Crie uma segunda seção (ex.: "Personalização") com sua própria `<legend>` e verifique o espaçamento.
3. Aumente o tamanho do título do header para `3rem` e veja o impacto visual.

---

## 📎 Arquivos alterados
- `index.html` — header do painel lateral, fieldset/legend e script do Lucide
- `styles/_layout.css` — estilos do header e dos títulos de seção

---

Pronto! Agora o layout transmite a identidade visual e a hierarquia de títulos conforme o style guide. 🚀
