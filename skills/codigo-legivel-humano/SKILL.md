---
name: codigo-legivel-humano
description: Use sempre que entregar, criar, alterar ou corrigir código em qualquer projeto. Valida o código gerado (executa testes, lint e build) e ajusta nomes, estrutura, comentários e formatação para que o código pareça escrito por um desenvolvedor humano, fácil de ler e de dar continuidade.
---

# Código legível para humanos

Objetivo: o código entregue deve ser validado, funcionar e ser fácil de manter por uma pessoa que não o escreveu. Ele deve parecer escrito por um desenvolvedor humano cuidadoso, sem marcas de geração automática.

## Quando usar

Use em toda entrega de código: funcionalidade nova, correção de bug, refatoração, script, automação ou ajuste de configuração.

## Prioridade das regras

1. Convenções do projeto (arquivos de configuração, `CONTRIBUTING`, README, código existente ao redor) têm prioridade sobre esta skill.
2. Comportamento correto e validado vem antes de estilo.
3. Legibilidade vem antes de esperteza. Código curto e óbvio vence código compacto e engenhoso.

## Fluxo obrigatório

### Etapa 1: Entender o que mudou

- Liste os arquivos alterados (`git status` e `git diff`).
- Confirme que mudanças fora do escopo da tarefa não foram feitas. Se foram, reverta ou explique.

### Etapa 2: Validar

Rode o que o projeto já oferece. Descubra os comandos em `package.json`, `Makefile`, `pyproject.toml`, `README`, CI (`.github/workflows`) etc.

- Testes existentes: devem passar.
- Lint e formatação: devem passar sem erros novos.
- Build ou execução: o código deve iniciar ou compilar.
- Se o projeto não tem testes para a mudança, faça ao menos uma verificação real (executar o script, chamar a função com casos de borda, subir o servidor e testar o endpoint).

Se algum passo falhar, corrija antes de seguir. Se não for possível rodar algo, diga isso explicitamente na entrega. Não afirme que o código funciona sem evidência.

### Etapa 3: Revisar como um humano revisaria

Percorra o checklist abaixo nos arquivos alterados e corrija o que encontrar.

**Nomes**
- Variáveis, funções e arquivos descrevem o conteúdo ou a ação (`valor_total`, `calcular_frete`), não siglas nem nomes genéricos (`data2`, `tmp`, `helper`, `utils`, `manager`).
- Use o idioma que o projeto já usa. Se não houver padrão, use o idioma da conversa com o responsável pelo projeto.
- Nomes consistentes no arquivo inteiro. Não alterne `cliente`, `customer` e `usuario` para a mesma coisa.

**Estrutura**
- Funções fazem uma coisa. Se o nome precisa de "e" para ser descrito, divida.
- Remova aninhamento profundo com retornos antecipados (guard clauses).
- Remova código morto, imports não usados, variáveis não usadas, parâmetros que nada usam.
- Remova duplicação óbvia, mas não crie abstração antes de existirem ao menos dois usos reais.
- Evite classes, camadas e padrões de projeto que a tarefa não exige.

**Comentários**
- Comente o porquê, não o quê. Um comentário que repete o código deve ser apagado.
- Remova comentários de geração: "Aqui está o código", "Esta função faz...", "Nota: gerado automaticamente", "Ajuste conforme necessário".
- Comentários e docstrings em tom direto, na voz de um colega, sem exagero.
- Sem emojis em código, logs de sistema ou mensagens técnicas, a menos que o projeto já use.

**Tratamento de erros e entradas**
- Erros são tratados de forma específica. Evite `except Exception: pass` e `catch` vazio.
- Mensagens de erro dizem o que aconteceu e o que fazer, em linguagem clara.
- Valores fixos (limites, URLs, nomes de tabela) viram constantes ou configuração com nome claro.
- Nunca deixe segredos, tokens ou senhas no código.

**Formatação**
- Use o formatador do projeto (Prettier, Black, gofmt, rustfmt, etc.). Se o projeto não tem um, mantenha o estilo do arquivo.
- Linhas curtas, blocos separados por linha em branco quando ajudam a leitura, sem linhas vazias demais.

**Sinais de código gerado de forma pouco cuidadosa**
- Blocos de código com uma função que só chama outra função sem agregar nada.
- Validações repetidas ou checagens que nunca podem ser verdadeiras.
- Textos de exemplo, dados fictícios ou URLs de placeholder que ficaram no código final.
- `TODO` ou `FIXME` sem dono e sem contexto. Se for necessário, descreva o que falta e por quê.

### Etapa 4: Aplicar os ajustes e revalidar

- Faça os ajustes do checklist sem mudar o comportamento, a menos que a mudança seja uma correção deliberada e esteja descrita na entrega.
- Rode novamente os testes, lint e build da Etapa 2.
- Refatoração não deve mudar resultado. Se mudar, é um bug.

### Etapa 5: Entregar com um resumo para humanos

Termine toda entrega com este bloco, em linguagem simples:

```
## O que foi feito
- <mudança 1, em uma frase>
- <mudança 2, em uma frase>

## Arquivos alterados
- `caminho/arquivo.ext`: <o que mudou nele>

## Como validar
1. <comando para rodar testes>
2. <comando para rodar o projeto ou verificar o resultado>

## Decisões e motivos
- <decisão relevante e por que foi tomada>

## Pontos de atenção
- <limitação, risco, dívida técnica ou algo que o responsável precisa decidir>

## Não verificado
- <o que não foi possível testar e por quê; "nada" se tudo foi verificado>
```

Se a entrega for pequena (uma linha corrigida, por exemplo), o bloco pode ser reduzido a "O que foi feito" e "Como validar".

## Regras de segurança do processo

- Não altere testes para que passem. Corrija o código, ou explique por que o teste estava errado.
- Não remova validações, logs de auditoria ou tratamento de erro para "simplificar".
- Não instale dependências novas sem avisar. Se instalar, liste na entrega.
- Não faça commit, push ou abra pull request sem pedido explícito do responsável.

## Modelo de qualidade

Antes de entregar, responda mentalmente:

- Um desenvolvedor novo no projeto entenderia este código em poucos minutos?
- Alguém conseguiria mudar esta parte amanhã sem medo de quebrar outra?
- Os nomes e comentários soam como de uma pessoa do time, e não de uma ferramenta?
- Eu rodei o que é possível rodar e sei exatamente o que não foi verificado?

Se a resposta a qualquer uma for "não", volte à Etapa 3.
