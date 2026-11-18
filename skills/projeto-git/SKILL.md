---
name: projeto-git
description: Baixa atualizações ou publica alterações com Git em um ou mais projetos, preservando trabalho local e verificando os destinos. Use quando o usuário solicitar sincronização, commit ou push.
---

# Git de projetos

Distinga baixar atualizações de publicar alterações. Se o pedido disser apenas
"atualizar o Git" e o contexto não resolver a intenção, pergunte qual operação o
usuário deseja. Não presuma caminhos, provedor Git, nome do remoto ou branch.

## Identificar escopo e destino

- Leia as instruções locais aplicáveis e a documentação de contribuição/Git existente.
  Use a raiz indicada pelo usuário ou confirme a raiz com `git rev-parse --show-toplevel`.
- Confira `git status --short --branch`, branch atual, upstream e remotos. Não exponha
  credenciais eventualmente presentes nas URLs dos remotos.
- Use o destino autorizado na conversa e as convenções do projeto. Um upstream ajuda
  a identificar o destino, mas não autoriza publicar em uma branch de produção.
- Em múltiplos repositórios, confira cada raiz separadamente. Pastas vizinhas,
  submódulos e worktrees não são automaticamente parte do pedido.
- Não troque de branch com trabalho local nem use outro checkout por suposição.
  Em erro de propriedade, verifique a origem da pasta antes de considerar confiança
  limitada àquele comando; não altere a confiança global do Git automaticamente.

## Baixar atualizações

1. Confira alterações rastreadas, não rastreadas e staged. Execute `git fetch` do remoto
   confirmado e compare HEAD com a referência remota da branch pretendida.
2. Na branch correta, integre apenas por fast-forward, usando
   `git merge --ff-only <remoto>/<branch>` com os valores confirmados.
3. Preserve o trabalho local. Se houver divergência, conflito ou arquivos que impeçam
   a atualização, pare nesse repositório e informe o impedimento. Não use reset,
   limpeza, stash ou resolução destrutiva automaticamente. Continue nos demais
   repositórios independentes quando possível.
4. Confira status e `git rev-list --left-right --count HEAD...<remoto>/<branch>`.
   Diferencie commits locais de commits ainda não integrados.

Baixar fontes não autoriza commit, push, instalação de dependências, build,
migration, implantação ou reinício de serviços.

## Publicar alterações

1. Confirme o escopo autorizado, branch e remoto; inspecione o diff de trabalho e o
   diff staged. Busque atualizações e compare com o destino antes de publicar.
2. Selecione explicitamente os arquivos ou trechos da tarefa. Não use `git add .`
   ou equivalentes que incluam mudanças sem revisão. Se um arquivo misturar trabalho
   de outras tarefas, separe os trechos antes de incluir.
3. Preserve o index preexistente. Se houver conteúdo staged fora do escopo, prepare
   um commit isolado sem alterar esse estado ou esclareça o impedimento. Não inclua
   nem remova silenciosamente esses itens.
4. Exclua segredos, arquivos de ambiente privados, bancos, backups e artefatos locais.
   Exemplos de configuração só entram após revisão do conteúdo. Execute as
   verificações previstas para a mudança e `git diff --check` nos arquivos da tarefa;
   revise `git diff --cached` para confirmar o conteúdo exato do commit.
5. Faça commit e push quando autorizados pelo pedido. Uma solicitação para publicar
   as alterações pode autorizar ambos; um pedido apenas de commit não autoriza push.
   Não force push nem promova mudanças entre branches por suposição.
6. Em rejeição ou conflito, preserve o estado e informe o que falta; não repita a
   tentativa sem resolver a causa. Após o envio, confira o SHA da branch remota,
   o commit local e o status final. Diferencie commit local de publicação confirmada.

Relate de forma concisa repositório, branch, commit, resultado e pendências.
Não exponha credenciais, segredos ou conteúdo sensível nas saídas.
