---
name: motion-after-effects
description: >
  This skill should be used when the user wants Claude to create or edit motion graphics in
  Adobe After Effects on their computer through ZionDesk — "faz uma animação no After Effects",
  "cria um motion para minha VSL", "anima meu logo", "texto animado / kinetic typography",
  "vídeo de lançamento do meu SaaS", "gráfico animado de dados", "abertura para o YouTube",
  "motion para Reels", "renderiza a composição", "make a motion graphic in After Effects".
metadata:
  version: "0.1.0"
---

# Motion graphics no After Effects pelo ZionDesk

O Claude é o diretor criativo: escreve todo o texto, escolhe a marca e cada movimento. O
ZionDesk só executa operações nativas no After Effects. Meta: acabamento de estúdio, original
para cada cliente, nunca cara de template.

## Preparação

1. Se as ferramentas `after_effects_*` não estiverem disponíveis, ativar:
   `ziondesk_tools` `{action: "enable", packs: ["after_effects"]}`.
2. After Effects precisa estar aberto. Ler o estado com `after_effects_context`.
3. `after_effects_checkpoint` antes de mudanças grandes; `after_effects_rollback` se precisar
   voltar.

## Peça nova

1. Identificar o nicho e carregar o playbook:
   `after_effects_capabilities` com `skill` = `vsl` | `saas_launch` | `kinetic_type` |
   `data_story` | `logo_reveal` | `youtube` | `tutorial` | `reels` e `section: "core"`.
   Ler formatos, narrativa, regras de copy, tipografia, cor, grid, tempos e QC.
2. Coletar do usuário (ou do material dele) o que faltar: texto/oferta, cores da marca (hex),
   fontes, formato (16:9, 9:16, 1:1), duração.
3. `section: "blueprint"` para ver a estrutura cena a cena e os campos de copy exigidos.
4. Montar com `after_effects_build_from_skill`: `skill`, um nome de `composition` **novo**,
   `copy` com **todos** os campos preenchidos e `brand` (`bg`, `surface`, `text`, `muted`,
   `accent`, `fontDisplay`, `fontText`). Ele recusa antes de tocar no AE se faltar algo.
5. Para peças fora dos blueprints, usar `section: "moves"` e montar com
   `after_effects_apply_operations` (consultar o schema de uma operação com
   `after_effects_capabilities` `operationType: "<tipo>"`).

## Revisar (obrigatório antes de entregar)

- `after_effects_motion_review` na composição, por trechos (até 10 s, até 8 quadros): olhar
  pixels e tempos de keyframe.
- Conferir: texto legível e dentro da área segura, contraste, hierarquia, nada cortado, ritmo
  coerente com a trilha, easing (sem movimentos lineares duros), nada sobreposto sem querer.
- `after_effects_timeline_diagnostics` para problemas de timeline; `after_effects_quicklook`
  com `motion: true` para uma olhada rápida; `after_effects_live_preview` para o usuário
  acompanhar ao vivo.
- Corrigir com `after_effects_apply_operations` **pelo nome da camada** e revisar de novo.

## Renderizar

- `after_effects_render` com `mode: "preview"` (até 12 s) para o usuário aprovar.
- `mode: "master"` **somente quando o usuário pedir a versão final**.

## Recursos avançados

Tracking de tela (`after_effects_track_screen`, `after_effects_track_review_frames`), matte de
oclusão (`after_effects_occlusion_matte`, `after_effects_occlusion_review`), envio de mídia
(`after_effects_send_asset`) e projeto de vídeo completo (`after_effects_build_video_project`,
`after_effects_apply_edit_plan`). Ler `after_effects_capabilities` com o `topic` correspondente
(`tracking`, `compositing`, `assets`, `audio`, `delivery`) antes de usar.

Critérios de qualidade: `references/qualidade.md`.
