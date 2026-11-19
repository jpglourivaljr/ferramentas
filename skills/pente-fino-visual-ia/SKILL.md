---
name: pente-fino-visual-ia
description: Passa um pente fino na interface (tela, modal, card, página, componente de UI) para tirar os sinais de design feito por IA e deixar a aparência de um projeto feito à mão. Use quando o usuário disser que algo "parece feito com IA", "tem cara de IA", "muito badge", "template", "genérico", "pente fino visual", "tira esses efeitos", "melhora o visual", ou pedir para revisar o design de uma tela. Vale para qualquer projeto de front-end (React, Vue, HTML/CSS, Tailwind).
---

# Pente fino visual contra cara de IA

Objetivo: a tela deve parecer desenhada por alguém que pensou no conteúdo, não por um gerador de cards. Cada elemento precisa responder a uma pergunta: **isso ajuda a pessoa a entender ou a agir?** Se não ajuda, sai.

## Sinais que denunciam IA

Procure estes padrões no código (JSX, CSS, templates) e na tela renderizada.

**Excesso de etiquetas**
- Badge, pill ou tag em quase tudo (status, categoria, "novo", contagem). Um badge por tela, no máximo, e só para estado que muda a decisão.
- Chips coloridos para informação que cabe numa frase.

**Rótulos e textos de template**
- Rótulo em caixa-alta com espaçamento (`text-transform: uppercase; letter-spacing: 1px`) em cada título de seção.
- Eyebrow (texto pequeno acima do título) sem função.
- Metadados unidos por ponto médio: `Ativo · 12 dias · Zona 2`.
- Rótulo no formato `PALAVRA — fragmento` ou travessão com espaço em volta.
- Seta `→` no fim de links e botões.
- Frases de vitrine ("tudo o que você precisa", "poderoso e intuitivo", "simples assim").
- Placeholders e textos de exemplo que sobraram ("Lorem", "Exemplo", "Texto aqui").
- Emoji em título, botão ou mensagem de sistema.

**Estrutura repetida**
- Todo conteúdo em cartões iguais, com o mesmo raio de borda, a mesma sombra e o mesmo padding.
- Grade de cartões de métrica (número grande + rótulo pequeno + variação) sem dado que justifique.
- Numeração `01 / 02 / 03` em itens que não são sequência.
- Linha divisória ou borda em cada elemento, mesmo quando o espaço já separa.

**Efeitos decorativos**
- Gradiente de fundo ou de texto sem função.
- Sombra pesada ou `rgba(0,0,0,.1)` em todo card.
- Animação de entrada (fade + slide) em cada seção, ou hover com elevação em todo card.
- Ícone colocado em todo título, sem ligação com o conteúdo.

**Cor e tipografia**
- Cor de destaque espalhada (botões, títulos, ícones, bordas ao mesmo tempo).
- Mais de duas famílias de fonte, ou uma fonte "de display" usada só para um título.
- Uma palavra do título destacada em cor ou itálico.

## Procedimento

1. **Inventário.** Liste no arquivo alvo: quantos badges, ícones, cards, sombras, gradientes, textos em caixa-alta, `·`, `—`, `→`, emojis. Use Grep (ou `rg`) com esses padrões. O número mostra o tamanho do problema.

2. **Decisão por elemento.** Para cada item, responda: a pessoa perde algo se isso sumir? Se não, remova. Se sim, troque por texto simples ou por uma forma mais natural (frase, lista, tabela, linha do tempo).

3. **Badge vira frase.** Estado que cabe numa frase vai para o texto: "Aguardando vaga há 5 dias, na posição 3". Mantenha badge apenas para um estado que precisa ser visto de relance em uma lista.

4. **Estrutura segue o conteúdo.**
   - Sequência real (eventos com ordem) → linha do tempo.
   - Pares de campo e valor → lista com linha fina entre as linhas, não grade de cartões.
   - Explicação → parágrafo curto.
   - Itens iguais e comparáveis → tabela.
   Não use a mesma estrutura para tudo.

5. **Ícones com função.** Um ícone por seção, pequeno, na cor secundária do texto. Ele ajuda a bater o olho. Não coloque ícone em botão que já tem texto claro, nem em todo item de lista.

6. **Texto.** Frase curta, verbo no imperativo ou na ação ("Trocar a unidade", "Confirmar troca"), sentence case, sem vitrine. Nomeie pelo que a pessoa entende, não pelo nome técnico do campo. Se um texto só repete o título, apague.

7. **Cor e sombra.** Use só os tokens do projeto. Destaque (cor de ação) só em ação principal e em foco. Sombra leve ou nenhuma. Sem gradiente decorativo.

8. **Movimento.** Remova animações de entrada. Mantenha só o que responde a uma ação da pessoa (abrir, expandir, confirmar).

9. **Respeite o projeto.** Se o projeto tem guia de identidade visual (CLAUDE.md, README, design tokens, componentes existentes), ele vence esta skill. Reaproveite os componentes do projeto antes de criar outros.

10. **Valide.** Rode lint e build do projeto. Se a interface puder ser vista no navegador, abra a tela e confira em largura de desktop e de celular, sem rolagem horizontal. Se não der para ver, diga isso.

## Entrega

Responda em poucas linhas:
- o que saiu (com números: "de 14 badges para 1", "5 textos em caixa-alta removidos");
- o que entrou no lugar (frase, linha do tempo, lista);
- o que ficou de propósito e por quê;
- o que não foi verificado no navegador.

## Armadilhas

- Não troque badge por outro componente com a mesma cara (um chip cinza no lugar de um chip colorido não resolve).
- Não remova informação para "limpar". Mova o que é importante para o texto.
- Não crie um estilo novo com a mesma cara de IA em outra cor. Pergunte-se qual é o uso real da tela antes de desenhar.
- Não mexa em lógica, dados ou regras de negócio durante o pente fino. Só apresentação.
