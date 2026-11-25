# ZionDesk para Claude

Conecta o Claude ao seu computador pelo [ZionDesk](https://ziondesk.app) e ensina o Claude a
trabalhar nele com rapidez e segurança.

## O que vem no plugin

| Componente | Para quê |
|---|---|
| Conexão ZionDesk (`https://mcp.ziondesk.app/mcp`) | Acesso aos seus arquivos, terminal, Git, navegador, apps, Premiere Pro e After Effects |
| Skill **usar-pc** | Fluxo rápido para arquivos, código, terminal, Git, navegador e apps |
| Skill **conectar-pc** | Parear o computador, resolver "PC offline" e ver o que foi feito nele |
| Skill **editar-premiere** | Cortes, limpeza de fala, legendas, Shorts, multicâmera, cor e exportação |
| Skill **motion-after-effects** | Motion graphics por nicho (VSL, SaaS, logo, Reels…) com revisão quadro a quadro |

## Como começar

1. Instale o plugin e faça login na sua conta ZionDesk quando o Claude pedir.
2. Abra o **ZionDesk Desktop** no seu computador.
3. Diga ao Claude: "conectar meu PC" e informe o código de pareamento exibido no app.

## Exemplos

- "Abre meu projeto em C:\\meu-site, roda o dev server e me mostra no celular."
- "Corta os silêncios e os 'éé' do vídeo aberto no Premiere e coloca legenda estilo Shorts."
- "Cria um motion de 30 s em 9:16 para a minha VSL com as cores da marca."
- "O que foi feito no meu PC hoje?"

## Segurança

O Claude não publica, não faz deploy, não apaga seus dados e não muda senhas sem você pedir.
Exportações finais no Premiere/After Effects só acontecem quando você solicita.

## Dados e privacidade

Este plugin não roda nenhum script nem instala pacotes. Ele contém apenas instruções (skills)
e uma única conexão: o servidor MCP do ZionDesk em `https://mcp.ziondesk.app/mcp`, que exige
login na sua conta ZionDesk. Os comandos que o Claude envia (ler e editar arquivos, rodar
comandos, controlar o navegador, Premiere Pro e After Effects) passam por esse servidor e são
executados apenas no computador que você pareou. Nenhum dado é enviado a outro serviço. Você
pode ver o histórico de ações no seu computador pedindo "o que foi feito no meu PC?".
Política de privacidade: https://cloud.ziondesk.app/privacy
Suporte: https://cloud.ziondesk.app/support

## Licença

MIT — veja o arquivo LICENSE.
