---
name: projeto-manutencao
description: Organiza arquivos com segurança, revisa o código da tarefa e mantém a documentação de contexto em projetos de qualquer stack. Use durante entregas de desenvolvimento ou em pedidos de organização e manutenção, respeitando o escopo solicitado.
---

# Manutenção de projetos

Adapte a rotina ao projeto real. Descubra a raiz, leia `AGENTS.md` e os documentos
de orientação existentes, como README e guia de contribuição. Se houver um documento
oficial de contexto, leia as partes relevantes e seus links. Não imponha um nome de
arquivo, linguagem, framework, banco ou arquitetura.

Em uma entrega de desenvolvimento, revise as alterações e o contexto afetado e
inspecione a organização da raiz. Isso não autoriza reorganizar arquivos alheios à
tarefa. Em pedidos de análise ou espera, limite-se ao diagnóstico.

## Delimitar a manutenção

- Confira o estado inicial e o diff quando houver Git. Distinga as alterações desta
  tarefa do trabalho anterior; não reverta, esconda ou publique trabalho alheio.
- Revise o código alterado e dependências diretas. Auditoria completa e refatoração
  ampla só fazem parte do trabalho quando solicitadas.
- Inspecione a raiz sem recursão e prefira buscas direcionadas com `rg --files` e `rg`.
  Não varra dependências, backups, worktrees ou repositórios vizinhos em massa.
- Registre problemas fora do escopo com localização, impacto e sugestão, sem
  transformar a descoberta em autorização para corrigi-los.

## Organizar sem quebrar caminhos

Preserve na raiz os pontos de entrada, configurações, manifests, lockfiles e documentos
necessários às ferramentas do projeto. Arquivos antigos, ignorados ou sem referência
textual não são automaticamente descartáveis. Preserve links simbólicos, junctions
e itens de finalidade incerta.

Antes de mover algo, identifique produtor e consumidores: scripts, atalhos, CI,
documentação e ferramentas. Confira arquivos ocultos e ignorados relevantes sem abrir
segredos. Logs e outros arquivos gerados permanecem no caminho esperado até que seus
produtores sejam ajustados dentro do escopo.

Use a estrutura existente para documentos, scripts, histórico e temporários; crie
pastas apenas quando necessárias. Não mova bancos, backups, certificados, segredos,
uploads, dependências, metadados do controle de versão ou artefatos de implantação
como simples limpeza. Scripts temporários podem representar trabalho em andamento.

Mova somente itens cuja finalidade e referências foram confirmadas. Verifique caminhos
absolutos de origem e destino dentro da área autorizada, não sobrescreva destinos e
atualize consumidores no mesmo conjunto de mudanças. No Windows, use operações nativas
com caminhos literais. Esta rotina de organização não inclui exclusão de arquivos;
pedidos de exclusão exigem escopo próprio explícito. Relate origem, destino e motivo.

## Revisar o código da tarefa

Siga as convenções locais e a arquitetura existente, incluindo limites de tamanho
quando definidos pelo projeto. Priorize intenção nos nomes, responsabilidades claras,
tipagem conforme a linguagem, comentários para decisões não óbvias e erros descritivos.
Não imponha camadas ou bibliotecas de outra stack.

Confira conforme o código afetado:

- Validação das entradas, autorização e isolamento por usuário, organização ou outra
  unidade de acesso definida pelo domínio; consultas parametrizadas quando houver SQL.
- Paridade com o legado quando a tarefa traduzir regras existentes; consulte os
  fontes e contratos originais antes de alterar o comportamento.
- N+1, consultas repetidas, paginação, concorrência e efeitos colaterais.
- Em interfaces, padrões compartilhados, acessibilidade, carregamento, vazio, falha
  e recuperação de erros apropriada ao framework.
- Ausência de segredos e dados sensíveis em logs, documentos e arquivos versionados.

Corrija problemas ligados à tarefa dentro do escopo autorizado. Em alterações de banco,
consulte o esquema e o fluxo de migrations do projeto. Esta skill não autoriza executar
migrations, escrever dados operacionais, mudar regras de negócio ou implantar versões.

## Manter o contexto útil

Identifique qual documento contém as regras vigentes. Preserve essa autoridade e
evite cópias normativas concorrentes em arquivos de orientação de outros agentes.
Registros recentes podem esclarecer regras antigas; divergências exigem evidência,
especialmente quando descrevem ambientes diferentes.

Atualize o documento responsável quando houver decisões duradouras, contratos ou
caminhos alterados, validações relevantes e pendências reais. Não acrescente histórico
sem mudança relevante nem crie um sistema de documentação só para cumprir a rotina.

Divida documentos quando a mistura de regras, histórico e domínios prejudicar a leitura
seletiva. Extraia seções completas, mantenha invariantes na entrada e vincule os detalhes
indicando quando lê-los. Não aplique limites de linhas de código à documentação.

Antes de retirar texto, confira a preservação no destino e ajuste links, âncoras e
referências. Preserve pendências e diferenças entre ambientes. Histórico permanece
datado; regras vigentes indicam decisões substituídas quando houver confirmação.

## Validar e entregar

Descubra os comandos reais em manifests, scripts, documentação ou CI. Execute lint,
testes e build proporcionais às camadas alteradas; valide scripts e fluxos afetados
com evidência observável. Não execute comandos de produção como simples verificação.

Para mudanças exclusivamente documentais, confira diff, links e preservação do texto
movido. Valide skills com o validador disponível quando elas forem alteradas. Não
declare testes de código que não executou.

Confira o status final e `git diff --check` nos arquivos da tarefa quando houver Git.
Informe o que mudou, verificações realizadas e pendências. Diferencie revisão do diff
de auditoria completa. Commit e push dependem do pedido do usuário.
