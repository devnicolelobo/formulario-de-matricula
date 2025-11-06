# 📚 Task 11: Componente File Input (Foto de Capa)

## 🎯 Objetivo

Implementar o campo de upload de arquivo para a "Foto de Capa". A estratégia principal é esconder o `input type="file"` nativo e usar um `<label>` customizado (estilizado como um Botão Secundário) para acionar o clique. Deve-se criar um elemento visual para exibir o nome do arquivo após o upload (o estado filled).

---

## ✅ O Que Foi Implementado

### 1. Estrutura HTML

```html
<div class="input-wrapper">
  <label for="cover-photo">Foto de capa</label>
  <div class="file-upload-wrapper">
    <input type="file" id="cover-photo" name="cover-photo" accept="image/*" aria-label="Selecionar foto de capa">
    <label for="cover-photo" class="file-upload-button btn btn-secondary">
      <i data-lucide="upload"></i>
      <span>Selecionar</span>
    </label>
    <span class="file-status" id="file-status">Nenhum arquivo selecionado</span>
  </div>
</div>
```

**Características:**
- ✅ Input file nativo escondido (mas funcional)
- ✅ Label estilizado como botão secundário
- ✅ Elemento de status para mostrar nome do arquivo
- ✅ Atributo `accept="image/*"` para aceitar apenas imagens
- ✅ `aria-label` para acessibilidade

---

### 2. Esconder Input Nativo

```css
input[type="file"] {
  opacity: 0;
  position: absolute;
  width: 1px;
  height: 1px;
  margin: 0;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
```

**Por que esconder assim?**
- ✅ **Acessibilidade mantida:** Input ainda existe no DOM
- ✅ **Funcionalidade preservada:** Clique no label aciona o input
- ✅ **Visual customizado:** Podemos criar nosso próprio design
- ✅ **Clip rect:** Garante que não ocupe espaço

**Métodos combinados:**
- `opacity: 0` - Invisível
- `position: absolute` - Remove do fluxo
- `width/height: 1px` - Tamanho mínimo
- `clip: rect(0,0,0,0)` - Corta completamente

---

### 3. Wrapper e Layout

```css
.file-upload-wrapper {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  flex-wrap: wrap;
}
```

**Características:**
- ✅ **Flexbox:** Alinha botão e status horizontalmente
- ✅ **Gap:** Espaçamento entre botão e status
- ✅ **Flex-wrap:** Quebra linha em mobile se necessário

---

### 4. Botão de Upload

```css
.file-upload-button {
  margin: 0;
}
```

**Características:**
- ✅ Usa classes `.btn` e `.btn-secondary` existentes
- ✅ Herda todos os estilos do botão secundário
- ✅ Ícone de upload já incluído no HTML

**Estilos herdados:**
- Background: `var(--shape-button)`
- Color: `var(--text-body)`
- Hover: `var(--shape-hover)`
- Padding, border-radius, transitions

---

### 5. Status do Arquivo

```css
.file-status {
  color: var(--text-body);
  font-family: var(--font-body);
  font-size: 0.875rem;
  line-height: 1.5;
  user-select: none;
}

/* Estado filled - quando arquivo selecionado */
.file-status.filled {
  color: var(--text-heading);
  font-weight: 600;
}
```

**Estados:**
- **Default:** Cor do corpo (`--text-body`), texto "Nenhum arquivo selecionado"
- **Filled:** Cor do título (`--text-heading`), nome do arquivo, negrito

**Nota:** A classe `.filled` será adicionada via JavaScript quando arquivo for selecionado.

---

## 🎓 Conceitos Aprendidos

### 1. Input File Nativo - Limitações

**Problemas do input file nativo:**
- ❌ Aparência limitada pelo navegador
- ❌ Difícil customizar
- ❌ Inconsistente entre navegadores
- ❌ Texto "Escolher arquivo" não pode ser mudado facilmente

**Solução:**
- ✅ Esconder input nativo
- ✅ Criar label customizado
- ✅ Manter funcionalidade nativa

---

### 2. Label Como Botão

**Estratégia:**
```html
<input type="file" id="cover-photo">
<label for="cover-photo" class="btn btn-secondary">Selecionar</label>
```

**Como funciona:**
- Label conectado ao input via `for` e `id`
- Clique no label aciona o input file
- Label pode ser estilizado como botão
- Funcionalidade nativa preservada

**Vantagens:**
- ✅ Design totalmente customizado
- ✅ Funcionalidade nativa mantida
- ✅ Acessibilidade preservada

---

### 3. Atributo `accept`

```html
<input type="file" accept="image/*">
```

**O que faz?**
- Filtra tipos de arquivo no seletor
- `image/*` aceita qualquer imagem
- Melhora UX (usuário vê apenas imagens)

**Outros exemplos:**
```html
accept="image/png,image/jpeg"  /* Apenas PNG e JPEG */
accept=".pdf,.doc,.docx"        /* Apenas documentos */
accept="video/*"                /* Apenas vídeos */
```

---

### 4. Clip Rect - Técnica de Ocultação

```css
clip: rect(0, 0, 0, 0);
```

**O que faz?**
- Corta o elemento completamente
- Sintaxe: `rect(top, right, bottom, left)`
- `rect(0, 0, 0, 0)` = corta tudo

**Por que usar?**
- Garante que elemento não ocupe espaço
- Mais robusto que apenas `opacity: 0`
- Funciona bem com `position: absolute`

**Nota:** `clip` é legado, mas ainda funciona. Alternativa moderna: `clip-path`.

---

### 5. User Select None

```css
user-select: none;
```

**O que faz?**
- Impede seleção de texto
- Melhor UX em elementos interativos
- Evita seleção acidental

**Uso:** Perfeito para status de arquivo que não deve ser selecionado.

---

### 6. Previsão de JavaScript

**Estrutura preparada para JS:**
```html
<span class="file-status" id="file-status">Nenhum arquivo selecionado</span>
```

**JavaScript futuro:**
```javascript
const fileInput = document.getElementById('cover-photo');
const fileStatus = document.getElementById('file-status');

fileInput.addEventListener('change', (e) => {
  if (e.target.files.length > 0) {
    fileStatus.textContent = e.target.files[0].name;
    fileStatus.classList.add('filled');
  } else {
    fileStatus.textContent = 'Nenhum arquivo selecionado';
    fileStatus.classList.remove('filled');
  }
});
```

**CSS preparado:**
- Classe `.filled` já estilizada
- Cores diferentes para default/filled
- Transição suave

---

## 🔍 Detalhes Técnicos

### Por Que Esconder Input e Não Remover?

**Abordagem correta:**
```css
opacity: 0;
position: absolute;
width: 1px;
height: 1px;
clip: rect(0, 0, 0, 0);
```

**Por quê?**
- ✅ Input ainda existe no DOM
- ✅ Funcionalidade nativa preservada
- ✅ Label conectado funciona
- ✅ Acessibilidade mantida

**Se removêssemos:**
```css
display: none; /* ❌ RUIM */
```
- ❌ Label não funcionaria
- ❌ Funcionalidade quebrada
- ❌ Acessibilidade quebrada

---

### Estrutura do Label Conectado

**HTML:**
```html
<input type="file" id="cover-photo">
<label for="cover-photo">Selecionar</label>
```

**Como funciona:**
1. Label tem `for="cover-photo"`
2. Input tem `id="cover-photo"`
3. Clique no label → aciona input file
4. Dialog de seleção abre

**Benefício:** Área clicável maior (todo o label, não apenas input pequeno).

---

### Por Que `accept="image/*"`?

**Benefícios:**
- ✅ Filtra apenas imagens no seletor
- ✅ Melhor UX (usuário não vê outros arquivos)
- ✅ Validação básica no navegador
- ✅ Reduz erros de upload

**Alternativas:**
```html
accept="image/png,image/jpeg,image/jpg"  /* Específico */
accept=".png,.jpg,.jpeg"                  /* Extensões */
```

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Acessibilidade Mantida

```html
<input type="file" aria-label="Selecionar foto de capa">
```

**Benefício:** Screen readers anunciam corretamente.

---

### 2. ✅ Reutilização de Estilos

```html
<label class="file-upload-button btn btn-secondary">
```

**Benefício:** Usa estilos existentes, não duplica código.

---

### 3. ✅ Estrutura Preparada para JS

```html
<span class="file-status" id="file-status">
```

**Benefício:** Fácil adicionar JavaScript depois sem mudar HTML.

---

### 4. ✅ Estados Visuais Claros

```css
.file-status { /* default */ }
.file-status.filled { /* filled */ }
```

**Benefício:** Feedback visual claro em cada estado.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Entender Label Conectado

Remova o atributo `for` do label:
```html
<label class="file-upload-button">Selecionar</label>
```

O que acontece ao clicar?

**Resposta:** Label não aciona o input, funcionalidade quebrada.

---

### Exercício 2: Modificar Accept

Mude para aceitar apenas PNG:
```html
<input type="file" accept="image/png">
```

Teste selecionar um arquivo. O que você observa?

**Resposta:** Seletor mostra apenas arquivos PNG (se disponíveis).

---

### Exercício 3: Adicionar JavaScript Básico

Adicione este script no final do HTML:
```javascript
document.getElementById('cover-photo').addEventListener('change', function(e) {
  const status = document.getElementById('file-status');
  if (this.files.length > 0) {
    status.textContent = this.files[0].name;
    status.classList.add('filled');
  }
});
```

Teste selecionar um arquivo. O que acontece?

**Resposta:** Status muda para nome do arquivo e fica em negrito.

---

## 📊 Comparação: Nativo vs Customizado

### ❌ Input File Nativo
- Aparência limitada
- Texto "Escolher arquivo" não customizável
- Inconsistente entre navegadores
- Difícil estilizar

### ✅ Input File Customizado
- Design totalmente controlado
- Botão customizado
- Consistente em todos navegadores
- Fácil estilizar
- Status visual claro

---

## 🚀 Próximos Passos

Agora que o file input está implementado, podemos:

1. **Adicionar JavaScript**
   - Interceptar evento `change`
   - Atualizar status com nome do arquivo
   - Adicionar classe `.filled`

2. **Preview da imagem**
   - Mostrar preview quando imagem selecionada
   - Atualizar preview no painel lateral

3. **Validação**
   - Validar tamanho do arquivo
   - Validar tipo de arquivo
   - Mensagens de erro

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Por que esconder input file em vez de removê-lo?
- [ ] Como funciona a conexão `label for` + `input id`?
- [ ] O que faz o atributo `accept`?
- [ ] Por que usar `clip: rect(0,0,0,0)`?
- [ ] Como preparar estrutura para JavaScript futuro?
- [ ] Por que usar `user-select: none` no status?

---

## 📚 Recursos Adicionais

- **File Input:** https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file
- **Label Element:** https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label
- **Accept Attribute:** https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#accept
- **Clip Property:** https://developer.mozilla.org/en-US/docs/Web/CSS/clip

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Como esconder input file mantendo funcionalidade
- ✅ Usar label como botão customizado
- ✅ Atributo `accept` para filtrar arquivos
- ✅ Técnica `clip: rect()` para ocultação
- ✅ Preparar estrutura para JavaScript
- ✅ Estados visuais (default, filled)

**Isso é conhecimento fundamental para criar uploads de arquivo profissionais e acessíveis!** 🚀

---

**Próxima Task:** Implementar validação de formulário e estados de erro.

