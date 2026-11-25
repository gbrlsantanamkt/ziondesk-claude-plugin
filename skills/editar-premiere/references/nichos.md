# Edição por nicho

## YouTube (talking head / vlog)
- Gancho nos primeiros 5–8 s; cortar qualquer introdução morna.
- Jump cuts nos silêncios, com respiro curto; punch-in leve (105–115%) a cada troca de ideia.
- B-roll a cada 5–10 s quando a fala descreve algo visual.
- Legendas `youtube_clean`; música de fundo com ducking.
- Marcadores de capítulo (`marker.add` tipo `Chapter`) nas viradas de assunto.

## Tutorial / screencast
- Ritmo mais calmo: não cortar pausas que o espectador usa para acompanhar.
- Zoom (`transform.set` com keyframes) na área da tela onde está a ação.
- Sem B-roll decorativo; títulos de etapa em lower-thirds.

## Podcast / entrevista
- `multicam_podcast_complete`: sync por waveform, troca automática de câmera pela fala.
- Corte de câmera só em fim de frase; plano aberto nas reações e risadas.
- Cadeia de voz `podcast_warm_broadcast`; lower-third com nome e cargo de cada convidado.

## Reels / Shorts / TikTok
- 9:16, 1080×1920; rosto no terço superior; área segura livre para a interface do app.
- Legenda `hormozi_short` (palavra a palavra, grande, central).
- Ritmo rápido: cortar todas as pausas; trocar enquadramento a cada 2–3 s.
- Duração alvo 20–45 s; primeira frase é o gancho.

## VSL (vídeo de vendas)
- Clareza acima de efeito: poucos cortes chamativos, legenda sempre legível.
- Destacar promessa, prova e oferta com texto na tela.
- Áudio limpo e constante; música discreta.
- Nada de transições "de template".
