# 📚 Documentação do Projeto FAQ

Guia prático para quem vai **alterar ou expandir** este projeto no futuro.

---

## 🗂️ Estrutura de Arquivos

```
PROJETO FAQ/
├── index.html      → Página inicial (cards de tópicos)
├── faq.html        → Página do FAQ (losangos + painel de resposta)
├── style.css       → TODO o visual do site (cores, tamanhos, animações)
├── faq-data.js     → BANCO DE DADOS das perguntas e respostas
├── faq.js          → Lógica dos losangos (clique, filtros, painel)
└── main.js         → Animações de entrada da página inicial
```

---

## ✏️ Tarefas Mais Comuns

### 1. Adicionar uma nova pergunta

Abra **`faq-data.js`** e adicione um bloco no array `FAQ_DATA`:

```js
{
  id: 19,                          // número único — não repita
  topic: "conta",                  // veja lista de tópicos abaixo
  topicLabel: "👤 Conta e Acesso", // texto exibido no painel
  question: "Minha nova pergunta aqui?",
  answer: `Resposta completa.
Você pode usar múltiplas linhas.
Use \\n para quebrar linha.`
},
```

**Tópicos disponíveis:**
| `topic` | Label exibido |
|---------|---------------|
| `conta` | 👤 Conta e Acesso |
| `sistema` | 🖥️ Sistema e Instalação |
| `relatorios` | 📊 Relatórios e Dados |
| `financeiro` | 💳 Financeiro |
| `integracao` | 🔗 Integrações |
| `seguranca` | 🔒 Segurança |
| `impressao` | 🖨️ Impressão |
| `outros` | 💬 Outros Assuntos |

---

### 2. Criar um novo tópico (categoria)

Você precisa editar **3 arquivos**:

**`faq-data.js`** — use o novo `topic` nas perguntas:
```js
topic: "meu_topico",
topicLabel: "🎯 Meu Tópico",
```

**`faq.html`** — adicione o botão de filtro dentro de `#filter-bar`:
```html
<button class="filter-btn" data-topic="meu_topico" id="filter-meu_topico">
  🎯 Meu Tópico
</button>
```

**`style.css`** — defina a cor do losango (no final do arquivo, seção "DIAMOND VARIAÇÕES DE COR"):
```css
.diamond.cat-meu_topico { background: linear-gradient(135deg, #cor1, #cor2); }
```

**`index.html`** *(opcional)* — adicione um card na `.topics-grid` se quiser que apareça na página inicial.

---

### 3. Mudar o e-mail de destino do suporte

Abra **`faq.js`**, linha ~317:
```js
// ⚠️ TROQUE O E-MAIL AQUI:
window.location.href = `mailto:suporte@empresa.com?subject=${assunto}&body=${corpo}`;
```
Substitua `suporte@empresa.com` pelo e-mail real.

---

### 4. Mudar cores do site

Abra **`style.css`** no topo — seção `:root`. As variáveis controlam tudo:

```css
:root {
  --clr-primary:   #7c3aed;  /* roxo principal */
  --clr-secondary: #06b6d4;  /* ciano */
  --clr-accent:    #a78bfa;  /* lilás claro */
  --clr-bg:        #0a0a14;  /* fundo escuro */
}
```

---

### 5. Mudar o comportamento dos losangos

Os losangos ficam **estáticos** com brilho pulsante. Para alterar isso, edite **`style.css`**:

| O que mudar | Onde está no CSS |
|-------------|-----------------|
| Animação padrão (pulso) | `@keyframes diamond-pulse` |
| Efeito ao passar o mouse | `.diamond-wrapper:hover .diamond` |
| Efeito quando clicado | `.diamond-wrapper.selected .diamond` |
| Velocidade de entrada | `renderDiamonds()` em `faq.js` (linha ~80) |

**Atenção:** A rotação foi **removida intencionalmente**. Se quiser reativar, adicione ao `.diamond`:
```css
animation: diamond-spin 4s linear infinite;
```
E readicione o `@keyframes diamond-spin` no CSS.

---

### 6. Mudar textos fixos da interface

| Texto | Onde editar |
|-------|-------------|
| Título "Perguntas Frequentes" | `faq.html` linha 58-60 |
| Subtítulo da página | `faq.html` linha 63 |
| Botões do painel (▶ / 👍 / 👎) | `faq.html` linhas 139-151 |
| Texto padrão no painel | `faq.html` linhas 123, 129 |
| Rodapé | `faq.html` linha 215 e `index.html` |

---

## ⚙️ Como Funciona o Fluxo Principal

```
Usuário abre faq.html
    ↓
faq.js roda: checkUrlParams() → renderDiamonds() → setupFilters()
    ↓
renderDiamonds() lê FAQ_DATA (faq-data.js) e cria os losangos no #diamonds-track
    ↓
Usuário clica num losango → selectDiamond() → showPanel()
    ↓
Painel (#answer-panel) recebe a pergunta/resposta e fica visível
    ↓
Usuário clica "▶ Continuar" → resumeAll() → painel some
```

---

## 🚫 O que NÃO fazer

- **Não repita `id`** no `FAQ_DATA` — vai causar bugs na seleção.
- **Não mude a ordem dos `<script>`** no `faq.html` — `faq-data.js` deve vir antes de `faq.js`.
- **Não remova os `id=`** dos elementos HTML — o JavaScript depende deles para funcionar.

---

## 📞 Suporte e Contato

Para alterar o e-mail de suporte, veja o item 3 acima.
Todos os dados das perguntas ficam em `faq-data.js` — esse é o único arquivo que o time de conteúdo precisa editar no dia a dia.
