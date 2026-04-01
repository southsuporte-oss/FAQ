# 📘 Guia Rápido de Edição — PROJETO FAQ

Este guia foi feito para você alterar o site de forma simples, sem precisar de conhecimentos avançados de programação.

---

## 🙋‍♂️ 1. Como adicionar ou mudar Perguntas e Respostas
**Arquivo:** `faq-data.js`

Tudo o que aparece nos losangos e no painel de texto vem deste arquivo. Ele é uma lista de blocos como este:

```javascript
{
  id: 1,
  topic: "conta",
  topicLabel: "👤 Conta e Acesso",
  question: "Como redefinir minha senha?",
  answer: `Escreva sua resposta aqui...`
},
```

*   **Para mudar uma pergunta:** Altere o que está entre as aspas em `question`.
*   **Para mudar a resposta:** Altere o que está entre as crases ( ` ) em `answer`. Você pode pular linhas normalmente dentro das crases.
*   **Para adicionar nova:** Copie um bloco inteiro, cole embaixo (antes do último `];`) e mude o `id` para o próximo número.

---

## 🎨 2. Como mudar as CORES do site (Identidade Visual)
**Arquivo:** `style.css` (logo no início do arquivo)

Procure por `:root` (está bem lá em cima). Lá estão as "caixas mágicas" de cores:

*   `--clr-primary`: Cor principal (Roxo). Mude o código (ex: `#7c3aed`) para a cor que desejar.
*   `--clr-secondary`: Cor secundária (Ciano/Azul).
*   `--clr-bg`: Cor do fundo (Escuro).

---

## 📧 3. Como mudar o E-MAIL de Suporte
**Arquivo:** `faq.js` (quase no final do arquivo na função `sendToSupport`)

Procure pela linha que tem o `mailto:`:
`window.location.href = 'mailto:suporte@empresa.com?...'`

*   Basta apagar `suporte@empresa.com` e colocar o seu e-mail de trabalho.

---

## 🚀 Resumo de Arquivos:
*   `index.html`: A carinha do site (Página 1).
*   `faq.html`: Onde ficam os losangos (Página 2).
*   `style.css`: A "maquiagem" (Cores, Tamanhos, Fontes).
*   `faq-data.js`: O "cérebro" (As perguntas e respostas).
*   `faq.js`: O "motor" (Faz os losangos girarem e pararem).

---
**Boa sorte com as alterações amanhã! Basta salvar os arquivos e dar F5 no navegador.**
