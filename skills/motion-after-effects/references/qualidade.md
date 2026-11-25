# Padrão de qualidade de motion

## Movimento
- Easing em tudo que entra e sai; evitar interpolação linear, exceto em loops mecânicos.
- Entradas rápidas (8–14 quadros a 30 fps), saídas mais rápidas que as entradas.
- Escalonar elementos relacionados em 2–4 quadros (stagger), não todos juntos.
- Um movimento principal por vez; o olho precisa saber onde olhar.
- Cortes e batidas alinhados com a trilha/efeitos sonoros.

## Tipografia
- No máximo 2 famílias; hierarquia clara por peso e tamanho.
- Frases curtas na tela (até ~7 palavras por bloco em vídeos curtos).
- Tempo de leitura: ~0,3 s por palavra + 0,5 s de folga.
- Área segura: 5% das bordas em 16:9; em 9:16, livrar topo (~12%) e base (~20%) da interface.

## Cor e composição
- Paleta da marca: fundo, superfície, texto, texto secundário, um único acento.
- Contraste de texto equivalente a WCAG AA no mínimo.
- Grid consistente; alinhar elementos ao mesmo eixo entre cenas.

## Originalidade
- Não reaproveitar a mesma composição/arquétipo entre clientes diferentes.
- Derivar formas e movimentos do produto/marca (ex.: ícone do app vira elemento de transição).

## QC final
- Nenhum erro de digitação; preços e números conferidos com o usuário.
- Nada piscando por 1 quadro; nenhuma camada esquecida fora da tela que apareça no render.
- Áudio sem clipping; música e efeitos equilibrados.
