# Tema Nookdeck (tablet)

Visual do design system "Nookdeck Tablet" aplicado ao painel do PhoneBox. Alvo: tablet em paisagem, 1280×800, grade 12×8.

## Ativar

Nas configurações do agente (`http://127.0.0.1:8765`), em **Display**:

1. **Theme**: `Nookdeck`.
2. **More rows on a tablet**: ligado (a grade passa de 12×6 para 12×8).
3. **Page navigation**: `Page bar, always shown` (abas com ícone e nome embaixo).
4. Salve.

Com o agente oficial (sem este fork), a opção `Nookdeck` não aparece na lista. Coloque `"theme": "nookdeck"` em `display` no `config.json`.

## Layout pronto

`layouts/nookdeck-tablet.json` tem quatro páginas: Visão geral, Sistema, Live e Atalhos.
Em **Pages**, use **Import** e escolha o arquivo. Ajuste a tela do editor para tablet largo (12×8) antes de importar.

A página Live usa:

- cenas, gravação/transmissão e mixer do OBS (com "Allow OBS controls from the phone" ligado);
- quatro widgets "Pushed value" com as chaves `jogo_cpu`, `jogo_gpu`, `jogo_ram` e `jogo_temp`, alimentados pelo script do PC de jogo via `POST /api/push/<chave>`;
- uma grade de atalhos com 3 colunas.

## Arquivos

- `android/app/src/main/assets/www/nookdeck.css`: o tema inteiro, sob `[data-theme="nookdeck"]`.
- `main.js`: barra de status do topo (`renderNdHead`), tema replicado no `<html>` para os gráficos e gráfico com área cheia neste tema.
- `widgets/pc.js`: o cartão de cota (`quotaring`) ganha a versão em barra horizontal, mostrada só neste tema.
