# 📚 Task 05: Agrupamentos e Estrutura Interna do Formulário

## 🎯 Objetivo

Implementar a marcação HTML para o conteúdo principal do formulário, focando no uso semântico dos elementos. A principal estratégia é utilizar `<fieldset>` para agrupar logicamente os campos e `<legend>` para os títulos de seção, melhorando a acessibilidade e a organização.

---

## ✅ O Que Foi Implementado

### 1. Container do Formulário

```html
<div class="form-content">
  <!-- Seções do formulário -->
</div>
```

**Por que criar um container?**
- ✅ Isola o formulário do título principal
- ✅ Facilita estilização e espaçamento
- ✅ Permite controle independente do layout interno
- ✅ Modulariza o código

---

### 2. Estrutura de Seções com `<fieldset>` e `<legend>`

```html
<fieldset class="form-section">
  <legend class="section-title">
    <i data-lucide="calendar"></i>
    <span>Sobre o evento</span>
  </legend>
  <!-- Campos da seção -->
</fieldset>
```

**Três seções criadas:**
1. **"Sobre o evento"** - Ícone: `calendar`
2. **"Personalização"** - Ícone: `palette`
3. **"Dados para contato"** - Ícone: `user`

---

### 3. Input Wrapper Pattern

```html
<div class="input-wrapper">
  <label for="event-title">Título</label>
  <input type="text" id="event-title" name="event-title" placeholder="Nome do evento">
</div>
```

**Por que usar `.input-wrapper`?**
- ✅ Agrupa label + input como unidade
- ✅ Facilita espaçamento vertical consistente
- ✅ Permite estilização modular
- ✅ Melhora organização do CSS
- ✅ Facilita responsividade

**Estrutura padrão:**
```
.input-wrapper
  ├── label (texto descritivo)
  └── input/textarea (campo de entrada)
```

---

### 4. Campos Implementados

#### Seção "Sobre o Evento"
- ✅ **Título** - `<input type="text">`
- ✅ **Descrição** - `<textarea>`

#### Seção "Dados para Contato"
- ✅ **Nome** - `<input type="text">`
- ✅ **E-mail** - `<input type="email">`
- ✅ **Telefone** - `<input type="tel">`

---

## 🎓 Conceitos Aprendidos

### 1. HTML Semântico - `<fieldset>` e `<legend>`

**O que são?**
- `<fieldset>`: Agrupa campos relacionados logicamente
- `<legend>`: Título descritivo do grupo (deve ser o primeiro filho do fieldset)

**Por que usar?**
- ✅ **Acessibilidade:** Screen readers anunciam o grupo e seu título
- ✅ **Organização:** Agrupa campos relacionados visualmente
- ✅ **Validação:** Facilita validação de grupos de campos
- ✅ **UX:** Usuário entende a relação entre campos

**Exemplo prático:**
```html
<!-- ✅ BOM - Semântico e acessível -->
<fieldset>
  <legend>Dados pessoais</legend>
  <input name="nome">
  <input name="email">
</fieldset>

<!-- ❌ RUIM - Apenas visual -->
<div class="section">
  <h2>Dados pessoais</h2>
  <input name="nome">
  <input name="email">
</div>
```

**Diferença:**
- Screen readers anunciam: "Dados pessoais, grupo. Nome, campo de texto."
- No segundo caso, pode não fazer a associação correta.

---

### 2. Atributo `for` em Labels

```html
<label for="event-title">Título</label>
<input type="text" id="event-title" name="event-title">
```

**O que faz?**
- Conecta o label ao input através do `id`
- Ao clicar no label, o input recebe foco
- Melhora acessibilidade (screen readers)

**Benefícios:**
- ✅ Área clicável maior (label + input)
- ✅ Melhor UX em mobile
- ✅ Acessibilidade melhorada

**Sem `for`:**
```html
<!-- Funciona, mas menos acessível -->
<label>
  Título
  <input type="text">
</label>
```

---

### 3. Tipos de Input e Seus Propósitos

#### `type="text"`
```html
<input type="text" id="event-title" placeholder="Nome do evento">
```
- **Uso:** Texto livre (título, nome)
- **Validação:** Nenhuma (aceita qualquer texto)
- **Mobile:** Teclado padrão

#### `type="email"`
```html
<input type="email" id="contact-email" placeholder="exemplo@email.com">
```
- **Uso:** Endereços de e-mail
- **Validação:** Navegador valida formato básico (@, domínio)
- **Mobile:** Teclado com @ e .com

#### `type="tel"`
```html
<input type="tel" id="contact-phone" placeholder="(99) 99999-9999">
```
- **Uso:** Números de telefone
- **Validação:** Nenhuma (aceita qualquer texto)
- **Mobile:** Teclado numérico

#### `<textarea>`
```html
<textarea id="event-description" rows="4" placeholder="Escreva sobre os detalhes do evento"></textarea>
```
- **Uso:** Texto longo (descrições, comentários)
- **Atributos:** `rows` define altura inicial
- **Diferença:** Permite múltiplas linhas, input não

---

### 4. Atributos Importantes

#### `name`
```html
<input name="event-title">
```
- **Propósito:** Identifica o campo no envio do formulário
- **Uso:** Backend recebe dados com esse nome
- **Obrigatório:** Sim, para formulários funcionais

#### `id`
```html
<input id="event-title">
```
- **Propósito:** Identificador único no HTML
- **Uso:** Conectar com `<label for="...">`
- **Regra:** Deve ser único na página

#### `placeholder`
```html
<input placeholder="Nome do evento">
```
- **Propósito:** Texto de exemplo/hint
- **Comportamento:** Some quando usuário digita
- **⚠️ Atenção:** Não substitui `<label>`! Placeholder é apenas hint.

**Diferença:**
- **Label:** Sempre visível, descreve o campo
- **Placeholder:** Texto de exemplo, some ao digitar

---

### 5. Estrutura Hierárquica

```
main.form-panel
  └── h1 (Título principal)
  └── div.form-content
      ├── fieldset.form-section (Sobre o evento)
      │   ├── legend.section-title
      │   └── div.input-wrapper
      │       ├── label
      │       └── input/textarea
      │
      ├── fieldset.form-section (Personalização)
      │   └── legend.section-title
      │
      └── fieldset.form-section (Dados para contato)
          ├── legend.section-title
          └── div.input-wrapper (múltiplos)
              ├── label
              └── input
```

**Por que essa hierarquia?**
- ✅ Semântica clara
- ✅ Fácil navegação (screen readers)
- ✅ Organização lógica
- ✅ CSS modular

---

## 🔍 Estratégias Aplicadas

### 1. **Modularidade com Wrappers**

Cada campo é envolvido em `.input-wrapper`:
- Facilita estilização consistente
- Permite reutilização
- Isola responsabilidades

**CSS futuro:**
```css
.input-wrapper {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xs);
  margin-bottom: var(--spacing-md);
}
```

---

### 2. **Separação de Responsabilidades**

- **HTML:** Estrutura e semântica
- **CSS:** Visual e layout (será implementado depois)
- **JavaScript:** Comportamento (será implementado depois)

**Benefício:** Código limpo e manutenível.

---

### 3. **Acessibilidade First**

- ✅ Labels conectados com `for`
- ✅ Fieldsets agrupando campos
- ✅ Legends descrevendo grupos
- ✅ Tipos de input corretos
- ✅ Atributos `name` para formulários

**Resultado:** Formulário acessível desde o início.

---

## 💡 Boas Práticas Aplicadas

### 1. ✅ Nomenclatura Consistente

```html
id="event-title"      name="event-title"
id="contact-name"     name="contact-name"
id="contact-email"    name="contact-email"
```

**Padrão:** `seção-campo` (kebab-case)

---

### 2. ✅ Comentários Organizados

```html
<!-- Seção: Sobre o Evento -->
<!-- Campos de personalização serão adicionados nas próximas tasks -->
```

Facilita navegação e manutenção.

---

### 3. ✅ Ícones com Lucide

```html
<i data-lucide="calendar"></i>
```

- Biblioteca leve
- Ícones SVG (escaláveis)
- Fácil customização via CSS

---

### 4. ✅ Placeholders Descritivos

```html
placeholder="Nome do evento"
placeholder="exemplo@email.com"
placeholder="(99) 99999-9999"
```

Dão contexto e formato esperado.

---

## 🧪 Exercícios de Fixação

### Exercício 1: Adicionar Novo Campo

Adicione um campo "Data de início" na seção "Sobre o evento":
```html
<div class="input-wrapper">
  <label for="event-start-date">Data de início</label>
  <input type="date" id="event-start-date" name="event-start-date">
</div>
```

**O que você aprendeu?**
- Estrutura do input-wrapper
- Tipo `date` para datas
- Nomenclatura consistente

---

### Exercício 2: Entender Fieldset

Remova o `<fieldset>` e `<legend>`, substitua por `<div>` e `<h2>`:
```html
<div class="form-section">
  <h2 class="section-title">Sobre o evento</h2>
  <!-- campos -->
</div>
```

Teste com um screen reader (ou extensão do navegador). O que mudou?

**Resposta:** Screen readers não fazem a associação correta entre título e campos.

---

### Exercício 3: Testar Acessibilidade

1. Use apenas o teclado (Tab) para navegar
2. Verifique se os labels focam os inputs corretos
3. Teste com leitor de tela (se disponível)

**O que você observou?**
- Labels focam inputs? ✅
- Navegação lógica? ✅
- Grupos são anunciados? ✅

---

## 📊 Comparação: Semântico vs Não-Semântico

### ❌ Abordagem Não-Semântica
```html
<div class="section">
  <h2>Dados pessoais</h2>
  <div class="field">
    <span>Nome</span>
    <input>
  </div>
</div>
```

**Problemas:**
- Screen readers não entendem a relação
- Sem agrupamento lógico
- Menos acessível
- HTML genérico

---

### ✅ Abordagem Semântica (Nossa)
```html
<fieldset class="form-section">
  <legend class="section-title">Dados pessoais</legend>
  <div class="input-wrapper">
    <label for="name">Nome</label>
    <input id="name" name="name">
  </div>
</fieldset>
```

**Vantagens:**
- ✅ Screen readers entendem grupos
- ✅ Agrupamento lógico claro
- ✅ Altamente acessível
- ✅ HTML semântico e moderno

---

## 🚀 Próximos Passos

Agora que a estrutura está pronta, podemos:

1. **Estilizar os inputs** (`_inputs.css`)
   - Estados (default, focus, error)
   - Cores e bordas
   - Placeholders

2. **Adicionar mais campos**
   - Datas (início/fim)
   - Tipo de evento (presencial/online)
   - Local

3. **Implementar validação**
   - Campos obrigatórios
   - Mensagens de erro
   - Feedback visual

---

## 📝 Checklist de Aprendizado

Marque o que você entendeu:

- [ ] Por que usar `<fieldset>` e `<legend>`?
- [ ] Qual a diferença entre `id` e `name`?
- [ ] Por que usar `.input-wrapper`?
- [ ] Qual a diferença entre `label` e `placeholder`?
- [ ] Quando usar `type="email"` vs `type="text"`?
- [ ] Como funciona a conexão `label for` + `input id`?
- [ ] Por que HTML semântico é importante para acessibilidade?

---

## 📚 Recursos Adicionais

- **HTML Forms:** https://developer.mozilla.org/en-US/docs/Learn/Forms
- **Fieldset/Legend:** https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset
- **Input Types:** https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input
- **Accessibility:** https://www.w3.org/WAI/tutorials/forms/

---

## 🎉 Conclusão

Nesta task, você aprendeu:
- ✅ Estrutura semântica de formulários
- ✅ Uso de `<fieldset>` e `<legend>`
- ✅ Padrão input-wrapper
- ✅ Tipos de input e seus propósitos
- ✅ Acessibilidade em formulários
- ✅ Boas práticas de HTML semântico

**Isso é conhecimento fundamental para criar formulários profissionais e acessíveis!** 🚀

---

**Próxima Task:** Estilizar os componentes de input com CSS.

