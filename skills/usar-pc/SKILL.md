---
name: usar-pc
description: >
  This skill should be used when the user asks Claude to work on their own computer through
  ZionDesk — "abre meu projeto", "edita esse arquivo no meu PC", "roda o build", "procura no
  código", "commita isso", "abre o site no navegador", "tira um print da tela", "fecha o
  programa travado", "work on my computer", "run this on my PC". Covers files, code search,
  terminal, Git, browser and desktop apps via the Ziondesk MCP tools.
metadata:
  version: "0.1.0"
---

# Usar o computador do cliente pelo ZionDesk

O ZionDesk liga o Claude ao computador do próprio usuário. O Claude é o único planejador: o
ZionDesk executa exatamente o que for pedido e não chama outro modelo de IA. Trabalhar rápido,
com poucas chamadas e sem surpresas no computador de alguém.

## Regras de segurança (sempre)

- Nunca publicar, fazer deploy, apagar dados do usuário, mudar senhas/credenciais ou matar
  processos que não sejam claramente o alvo, a menos que o usuário tenha pedido explicitamente.
- Nunca gravar segredos, tokens ou logs brutos em `agent_memory` ou `agent_checkpoint`.
- Ao falar com o usuário, usar "limite de uso", nunca "créditos".

## Fluxo rápido

1. **Dispositivo.** Omitir `deviceId` quando houver um único computador online. Se uma
   ferramenta responder `device_required`, escolher entre os candidatos retornados (ou chamar
   `devices_list`). Se nenhum computador estiver online, seguir a skill `conectar-pc`.
2. **Contexto.** Reaproveitar o que já se sabe (pasta raiz, URLs, stack). Só se faltar contexto,
   chamar `open_project` uma vez com `root` e `objective`.
3. **Ler em lote.** Agrupar leituras independentes: `list_dir` para pastas; `files_read`,
   `batch_read` ou `code_search` com `queries[]` para trechos; `git_status`/`git_diff` juntos.
   Usar `smart_inspect` quando não souber por onde começar.
4. **Editar.** Ler o alvo e editar com `file_edit` passando o `sha256` mais recente. Em
   conflito, reconciliar com o conteúdo/hash devolvido; só reler se não vier. `file_write` para
   arquivos novos ou reescrita completa; `file_write_binary` para binários.
5. **Executar.**
   - Comandos curtos: `shell_exec` (no Windows, `shell: "powershell"` para sintaxe complexa).
   - Builds, servidores, `npm`/`node` longos: `task_start`, depois `task_status`/`task_output`
     com `waitMs: 25000`. Nunca fazer polling com `sleep`. `task_cancel` para parar.
6. **Validar.** Revisar o diff e rodar a checagem mais estreita relevante (teste, lint, build
   do pacote afetado). Ampliar só se falhar ou se o impacto for maior.
7. **Ver o resultado.** Para interfaces web, abrir no navegador e conferir:
   `browser_action` com `finalSnapshot`, `browser_screenshot` quando a parte visual importa
   (testar também largura de celular). `browser_devtools` para console e rede.
8. **Registrar.** Após trabalho significativo, um `agent_checkpoint` com resumo, decisões,
   arquivos importantes, validações e pendências. Pular em tarefas triviais.

## Apps e tela

- `app_open` abre programas; `window_list` lista janelas; `process_list`/`process_kill`
  gerenciam processos (matar só com confirmação ou pedido claro).
- `screen_capture` para ver a tela; `screen_record` para gravar um fluxo.
- `clipboard_read`/`clipboard_write` para a área de transferência; `desktop_notify` para avisar
  o usuário de que algo longo terminou.
- Automação de interface (`ui_inspect`, `ui_action`, `ui_element_action`) fica no pacote
  `desktop`. Se não estiver disponível, ativar com
  `ziondesk_tools` `{action: "enable", packs: ["desktop"]}` — as ferramentas podem ser chamadas
  pelo nome mesmo antes de aparecerem na lista.

## Pacotes especializados

`ziondesk_tools` com `action: "list"` mostra os pacotes: `coding_advanced`, `desktop`,
`browser_advanced` (DevTools e navegador na nuvem), `after_effects`, `premiere`, `video`
(Video Studio). Ativar só o que a tarefa precisa.

## Falhas

Resultados com erro podem trazer um campo `hint` com o próximo passo recomendado — seguir o
hint antes de improvisar. Se o computador não responder, ver `conectar-pc`.

## Comunicação

Contar em uma linha o que vai fazer, trabalhar sem narrar cada chamada e terminar dizendo o
que mudou, onde, e como foi verificado. Distinguir "vou fazer", "fiz" e "verifiquei".

Detalhes por tipo de tarefa: `references/receitas.md`.
