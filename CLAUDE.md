# Lojinha DD — instruções para o Claude Code

Este repositório é PÚBLICO (GitHub Pages). Nada de chave, token, ID de planilha
ou dado de cliente entra aqui. Acesso, IDs e histórico completo estão no
documento privado de handover — peça o link ao Marcelo.

## Como funciona

- `index.html` é o site inteiro (HTML + CSS + JS). É o único arquivo que se edita.
- Os produtos vêm do CSV publicado da planilha Google; o `data.csv` deste
  repositório é só a reserva, gravado por um Apps Script a cada 10 minutos.
  **Nunca editar `data.csv` à mão** — é sobrescrito.
- Desconto do site = linha `__CONFIG__` da planilha (coluna B, %).
- Outlet = produto há N dias no site ganha piso de X% (linha `__OUTLET__`:
  B = %, C = dias; padrão 35% / 90). A data vem da coluna `Entrada`, que o
  Apps Script carimba sozinho. Vale sempre o maior desconto aplicável.
- Campanha com data: bloco `const PROMO_CAMP` (datas em `-03:00`, vira sozinha
  no navegador do visitante).
- Visual: bloco CSS "v7 — LAYOUT NOVO" no fim do `<style>` (camada aditiva).

## Regras

1. `git pull --rebase origin main` antes de commitar e antes de enviar — o
   Apps Script grava no `main` a cada 10 minutos. Nunca `push --force`.
2. Mudança aditiva: não reescrever o que funciona para consertar outra coisa.
3. Produto sem preço válido não aparece (de propósito). A coluna H da planilha
   ("Comprado por") nunca pode ir para o repositório.
4. Antes de dizer "ok": testar de ponta a ponta com a planilha real (servir
   local com `python3 -m http.server 8791`), no celular e no tema escuro.
5. Publicar só depois do "bora" do Marcelo; explicar em linguagem simples.
6. Mudança no Apps Script: backup, teste com dublê, `clasp push`, conferir que
   o próximo "Auto-sync" aparece no `git log origin/main`.
