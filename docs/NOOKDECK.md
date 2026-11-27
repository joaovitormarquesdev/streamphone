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

`layouts/nookdeck-tablet.json` tem cinco páginas: Visão geral, Sistema, Live, Atalhos e Processos.
Em **Pages**, use **Import** e escolha o arquivo. Ajuste a tela do editor para tablet largo (12×8) antes de importar.

A Visão geral mostra os widgets "Pushed value" `jogo_cpu`, `jogo_gpu`, `jogo_ram` e `jogo_temp`, alimentados pelo script
do PC de jogo via `POST /api/push/<chave>`. A mídia ocupa 4 colunas: é a largura mínima dela, com 3 ela invadia a vizinha.

A página Live usa:

- cenas, gravação/transmissão e mixer do OBS (com "Allow OBS controls from the phone" ligado);
- as estatísticas que o agente do fork lê do OBS a cada 2 s e publica como valores (expiram em 10 s):
  `obs_dropped` (quadros perdidos na rede, %), `obs_lag` (quadros atrasados no render/encoder, %), `obs_cpu`, `obs_fps`
  e `obs_kbps`. Cada valor traz `level` (ok/warn/error), que colore o cartão, e serve de gatilho para regras do tipo "valor enviado";
- uma grade de atalhos (5 colunas) com os ids dos botões do OBS.

## Atalhos do OBS

Os botões apertam hotkeys globais configuradas no OBS (perfil › Configurações › Atalhos), em teclas que jogos não usam:

| Tecla | Ação |
|---|---|
| F13 … F21 | as cenas, na ordem da lista do OBS |
| Ctrl+F13 / F14 / F15 | live, gravação, pausar gravação (mesma tecla liga e desliga) |
| Ctrl+F16 / F17 | mutar o mic / o som do PC |
| Ctrl+F18 / F19 / F20 / F21 | print, marcador de capítulo, replay buffer, câmera virtual |

O agente segura cada tecla 50 ms: o OBS consulta o teclado a cada ~25 ms e perdia toques instantâneos.
Os atalhos ficam no `config.json` do agente, não no layout: a grade só mostra os ids que existirem lá.

## Arquivos

- `android/app/src/main/assets/www/nookdeck.css`: o tema inteiro, sob `[data-theme="nookdeck"]`.
- `main.js`: barra de status do topo (`renderNdHead`), tema replicado no `<html>` para os gráficos e gráfico com área cheia neste tema.
- `widgets/pc.js`: o cartão de cota (`quotaring`) ganha a versão em barra horizontal, mostrada só neste tema.
