---
name: editar-premiere
description: >
  This skill should be used when the user wants Claude to edit video in Adobe Premiere Pro on
  their computer through ZionDesk — "edita meu vídeo no Premiere", "corta os silêncios", "tira
  os 'éé' e gaguejadas", "coloca legenda", "faz cortes para Reels/Shorts", "sincroniza as
  câmeras do podcast", "adiciona b-roll e efeitos sonoros", "corrige a cor", "exporta para o
  YouTube", "edit my video in Premiere".
metadata:
  version: "0.1.0"
---

# Editar no Premiere Pro pelo ZionDesk

O Claude planeja cada decisão editorial; o ZionDesk só executa operações nativas no Premiere.
Editar como um editor profissional do nicho (vlog, tutorial, podcast, VSL, Reels).

## Preparação

1. Se as ferramentas `premiere_*` não estiverem disponíveis, ativar:
   `ziondesk_tools` `{action: "enable", packs: ["premiere"]}`.
2. Premiere precisa estar aberto com o projeto. Começar **sempre** por `premiere_context`
   (somente leitura). Se vier marcado como desatualizado (edição em andamento), aguardar e ler de
   novo — nunca editar a partir de um snapshot desatualizado.
3. `premiere_inspect` para obter os `nodeId` estáveis dos clipes antes de mexer neles.
4. `premiere_checkpoint` antes de qualquer edição grande. Se der errado: `premiere_rollback`.

## Escolher o caminho

| Pedido | Ferramenta |
|---|---|
| Edição completa a partir do bruto | `premiere_autopilot_edit` (`youtube_complete`, `multicam_podcast_complete`, `reels_shorts_factory`) — rodar antes com `dryRun: true` e mostrar o plano |
| Limpar "éé", repetições, gaguejadas | `premiere_clean_disfluencies` |
| Legendas | `premiere_auto_captions` (estilos `hormozi_short`, `youtube_clean`, `broadcast_tv`) |
| Cortes virais / Shorts | `premiere_extract_viral_highlights` + `premiere_smart_reframe` (9:16) |
| Podcast multicâmera | `premiere_sync_multicam_by_waveform` → `premiere_multicam_autoswitch` |
| B-roll e efeitos sonoros | `premiere_auto_broll_sfx` |
| Igualar cor entre câmeras | `premiere_auto_color_match` |
| Montagem no ritmo da música | `premiere_beat_sync_montage` |
| Acabamento de áudio/vídeo e QC | `premiere_broadcast_finish`, `premiere_scene_detect_and_qc` |
| Receitas editoriais prontas | `premiere_apply_editorial_recipe` |
| Ajustes finos | `premiere_apply_operations` (até 64 operações atômicas por transação) |

## Regras de ajuste fino (`premiere_apply_operations`)

- Dar um `transactionId` único por lote; manter `atomic: true`.
- Mirar clipes por `nodeId`, não por índice, sempre que possível.
- B-roll: `clip.append` com `mediaSelect: "video_only"` numa trilha acima, para **nunca**
  sobrescrever o áudio da fala.
- Silêncios: `timeline.cut_silences` com `paddingSeconds` ~0.08 para manter a respiração.
- Música sob voz: `audio.duck` em vez de baixar o volume inteiro.
- Diálogo: manter a voz perto de 0 dB de ganho e ajustar a música; usar `clip.j_l_cut` para
  transições naturais entre falas.
- Vertical: `sequence.settings` 1080×1920 e reenquadrar com `transform.set`/`crop.set`.

## Revisar antes de entregar

- `premiere_capture_frames` nos pontos editados e olhar os quadros: corte no meio de palavra,
  legenda cobrindo rosto, B-roll fora de contexto, salto de cor.
- Corrigir e capturar de novo. Mostrar ao usuário os quadros-chave.

## Exportar

`premiere_render` **somente quando o usuário pedir a exportação final**. Escolher o
`presetAlias` pelo destino (`youtube_1080p`, `youtube_4k`, `h264_1080p_hq`, `prores_422_hq`…) e
confirmar o caminho de saída.

Boas práticas por nicho: `references/nichos.md`.
