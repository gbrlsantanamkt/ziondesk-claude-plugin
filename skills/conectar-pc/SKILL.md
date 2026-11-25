---
name: conectar-pc
description: >
  This skill should be used when the user needs to connect, pair or troubleshoot their computer
  with ZionDesk — "conectar meu PC", "parear o computador", "meu código de pareamento é…",
  "o ZionDesk não acha meu computador", "PC offline", "device_required", "qual computador está
  conectado", "o que o Claude fez no meu PC", "pair my device", "my computer is offline".
metadata:
  version: "0.1.0"
---

# Conectar e diagnosticar o computador no ZionDesk

## Parear um computador novo

1. Pedir ao usuário que abra o **ZionDesk Desktop** no computador e copie o **código de
   pareamento** exibido.
2. Chamar `pair_device` com `code` **somente** com um código que o próprio usuário digitou na
   conversa. Nunca inventar, adivinhar nem reaproveitar códigos de outro lugar.
3. Confirmar com `devices_list` que o computador aparece online.
4. Fazer um teste leve (`device_info`) e informar nome do computador e sistema.

## Diagnóstico: "não encontra meu computador"

Seguir em ordem e parar quando resolver:

1. `devices_list` — está listado? Está online?
   - **Não listado:** precisa parear (seção acima).
   - **Revogado:** só aparece com `includeRevoked: true`; precisa parear de novo.
   - **Offline:** pedir que o usuário confira se o PC está ligado e acordado, conectado à
     internet e com o ZionDesk Desktop aberto e logado na mesma conta.
2. **Vários computadores online:** as ferramentas retornam `device_required` com candidatos.
   Perguntar qual usar (pelo nome) e passar `deviceId` nas próximas chamadas.
3. **Online mas falhando:** `device_info` para checar o estado; ler o campo `hint` do erro e
   seguir a recomendação. Tentar de novo uma única vez se o erro sugerir; nunca repetir uma ação
   que talvez já tenha sido executada.
4. **Ferramenta não aparece** (Premiere, After Effects, automação de tela): ativar o pacote com
   `ziondesk_tools` `{action: "enable", packs: [...]}`.

## Auditoria: "o que foi feito no meu PC?"

`device_audit` (com `limit` até 100) lista os eventos recentes. Resumir em linguagem simples:
quando, o que foi lido/alterado/executado. Não expor IDs internos sem necessidade.

## Tom com o cliente

Linguagem simples, sem jargão de infraestrutura. Falar em "limite de uso", nunca "créditos".
Se algo depender de uma ação física do usuário (ligar o PC, abrir o app), dizer exatamente o que
fazer, em uma ou duas frases.
