# 📚 Task 02: Configuração Global (Tokens CSS, Reset e Dark Mode)

## 🎯 Objetivo
Implementar o arquivo `_config.css` com variáveis (tokens) de cor e tipografia, aplicar o reset e configurar os estilos base do modo escuro. Também importar as fontes no `index.html`.

---

## ✅ O que foi feito

### 1) Fonts no `index.html`
Usamos Google Fonts para carregar as famílias exigidas.

```html
<!-- Google Fonts: Leckerli One, Baloo 2, Open Sans -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@400;500;600;700&family=Leckerli+One&family=Open+Sans:wght@400;600;700&display=swap" rel="stylesheet">
```

- **preconnect**: antecipa a conexão com os domínios de fontes para melhorar performance.
- **href do Google Fonts**: entrega os arquivos de fontes otimizados.

Linkamos o CSS principal normalmente:
```html
<link rel="stylesheet" href="styles/main.css">
```

---

### 2) Tokens de Tipografia
Definimos variáveis (tokens) para fontes no `:root` — facilita troca de fontes em todo o projeto.

```css
:root {
  --font-body: 'Open Sans', sans-serif;            /* textos gerais */
  --font-heading: 'Baloo 2', system-ui, sans-serif;/* títulos e headings */
  --font-display: 'Leckerli One', cursive;         /* logotipo/branding */
}
```

Uso prático:
```css
body { font-family: var(--font-body); }
h1, h2, legend { font-family: var(--font-heading); }
.logo { font-family: var(--font-display); }
```

---

### 3) Tokens de Cor (Shape/Fundo, Texto, Marca)
Tokens são nomes semânticos que representam valores — padrão DRY e escalável.

```css
:root {
  /* Estrutura (fundo/painéis) */
  --shape-background: #131516; /* fundo da página (dark) */
  --shape-body: #212427;        /* cartões/painéis */
  --shape-button: #2D3134;      /* botões neutros */

  /* Texto e destaque */
  --text-heading: #F9F9F9;
  --text-body: #C8CDD0;
  --brand-mid: #3487CF;         /* azul de destaque */
}
```

Uso prático:
```css
body { background: var(--shape-background); color: var(--text-body); }
.card { background: var(--shape-body); }
.button-secondary { background: var(--shape-button); }
.title { color: var(--text-heading); }
.link { color: var(--brand-mid); }
```

---

### 4) Tokens de Input e Feedback
```css
:root {
  --input-base: #1C1F21;     /* fundo do input */
  --input-stroke: #363B40;   /* borda/traço */
  --feedback-danger: #FF5959;/* erros/alertas */
}
```

Uso prático:
```css
.input { background: var(--input-base); border-color: var(--input-stroke); }
.input--error { border-color: var(--feedback-danger); }
```

---

### 5) Reset + Base de Dark Mode
Reset simples e estilos globais aplicados.

```css
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  background-color: var(--shape-background);
  color: var(--text-body);
  font-family: var(--font-body);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1, h2, legend {
  font-family: var(--font-heading);
  color: var(--text-heading);
}
```

- **box-sizing: border-box** — torna cálculo de layout mais previsível.
- **antialiased/grayscale** — suaviza renderização de fontes.
- **Dark Mode**: a página já nasce com fundo escuro e textos claros.

---

## 🧩 Por que usar Tokens (Variáveis CSS)?
- **DRY**: um único ponto de mudança (cores, fontes, espaçamentos).
- **Consistência**: mantém visual uniforme em toda a aplicação.
- **Theming**: fácil criar tema claro/escuro alterando só o `:root` (ou adicionando `[data-theme="light"]`).
- **Escalabilidade**: componentes usam nomes semânticos em vez de valores fixos.

Exemplo de tema claro opcional:
```css
[data-theme="light"] {
  --shape-background: #F6F7F8;
  --shape-body: #FFFFFF;
  --text-body: #3A3A3A;
  --text-heading: #1C1C1C;
}
```

---

## 🔎 Mapa rápido dos principais tokens atuais

| Token | Valor | Uso típico |
|---|---|---|
| `--shape-background` | `#131516` | Fundo da página (dark) |
| `--shape-body` | `#212427` | Cards/painéis |
| `--shape-button` | `#2D3134` | Botões neutros |
| `--text-heading` | `#F9F9F9` | Títulos, headings |
| `--text-body` | `#C8CDD0` | Texto geral |
| `--brand-mid` | `#3487CF` | Ações/links/destaques |
| `--input-base` | `#1C1F21` | Fundo do input |
| `--input-stroke` | `#363B40` | Bordas de input |
| `--feedback-danger` | `#FF5959` | Erros/alertas |
| `--font-body` | Open Sans | Texto geral |
| `--font-heading` | Baloo 2 | Títulos |
| `--font-display` | Leckerli One | Logo |

---

## 🧠 Dicas práticas
- Prefira tokens semânticos (`--text-body`) a valores literais (`#C8CDD0`) nos componentes.
- Centralize mudanças de UI no `:root`.
- Use tokens também para espaçamentos, radius e animações (já existem `--spacing-*`, `--radius-*`, `--transition-*`).

---

## 🧪 Exercícios de fixação
1. Crie `--brand-light` e use em um estado `:hover` de botão.
2. Adicione `[data-theme="light"]` e troque `body` para esse tema via atributo no HTML para testar.
3. Crie `--border-radius-input` e utilize nos inputs.

---

## 📎 Arquivos tocados nesta task
- `index.html` — inclusão dos links do Google Fonts
- `styles/_config.css` — definição de tokens, reset e estilos base

---

Pronto! Agora o projeto está padronizado por tokens e preparado para escalar com consistência visual. 🚀
