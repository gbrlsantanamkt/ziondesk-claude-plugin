# Receitas rápidas

## Corrigir um bug num projeto
1. `git_status` + `code_search` (queries com o texto do erro e o nome da função) em paralelo.
2. `files_read` dos 1–3 arquivos suspeitos.
3. `file_edit` com o `sha256` lido.
4. `shell_exec` do teste afetado (ex.: `npm test -- caminho/do/teste`).
5. `git_diff` para revisar. Commitar só se o usuário pediu.

## Subir o projeto e conferir no navegador
1. `task_start` com o comando do servidor de desenvolvimento (ex.: `npm run dev`).
2. `task_output` com `waitMs: 25000` até aparecer a URL local.
3. `browser_action` navegando para a URL com `finalSnapshot: true`.
4. `browser_screenshot` em desktop e em largura de celular (~390px).
5. `browser_devtools` para erros de console se algo estiver quebrado.
6. Deixar o servidor rodando ou `task_cancel`, conforme o usuário preferir.

## Organizar arquivos
1. `list_dir` da pasta.
2. Propor o plano (o que vai para onde) antes de mover muita coisa.
3. Mover com `shell_exec`. Nunca apagar sem pedido explícito — mover para uma pasta
   `_para_apagar` e avisar.

## Ver o que está acontecendo na tela
1. `screen_capture`.
2. Se precisar clicar em um app desktop: ativar o pacote `desktop` e usar `ui_inspect` antes de
   `ui_element_action` (preferir elementos identificados a coordenadas).

## Retomar trabalho de outra conversa
1. `agent_memory` / `project_context` para recuperar o último checkpoint.
2. Confirmar com `git_status` que o estado bate com o registrado antes de continuar.
