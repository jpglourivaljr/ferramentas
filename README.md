# ferramentas

Repositório de skills pessoais para uso em vários projetos.

## Estrutura

```
skills/
  <nome-da-skill>/
    SKILL.md
```

## Skills

- `codigo-legivel-humano`: valida e ajusta código entregue para que seja legível e fácil de manter por humanos.
- [projeto-git](skills/projeto-git/SKILL.md): baixa atualizações ou publica alterações em um ou mais repositórios, preservando o trabalho local.
- [projeto-manutencao](skills/projeto-manutencao/SKILL.md): confere a organização dos arquivos, revisa o código da tarefa e mantém o contexto do projeto.
- [pente-fino-visual-ia](skills/pente-fino-visual-ia/SKILL.md): tira da interface os sinais de design feito por IA (badges em excesso, rótulos em caixa-alta, cartões iguais, gradientes) e devolve uma aparência feita à mão.

As skills `projeto-git` e `projeto-manutencao` foram generalizadas a partir das rotinas
do SigehWeb. Elas descobrem caminhos, branches, stack e regras na documentação de cada
projeto, sem exigir a estrutura do projeto de origem. As instruções locais e o escopo
solicitado pelo usuário orientam sua aplicação.

## Como usar em um projeto

Copie ou vincule a pasta completa da skill para o diretório usado pelo seu agente:

| Agente | Todos os seus projetos | Apenas um projeto |
| --- | --- | --- |
| Codex | `~/.agents/skills/` | `.agents/skills/` |
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |

Instalar uma skill não executa suas ações. Os pedidos do usuário e as instruções de
cada projeto determinam o escopo. Reinicie a sessão do agente após a instalação.

Exemplo no PowerShell, executado na raiz deste repositório, para instalar as duas
skills no Codex do usuário. O comando interrompe se já houver uma cópia instalada;
compare versões antes de substituir uma skill existente.

```powershell
$nomesSkills = @('projeto-git', 'projeto-manutencao')
$pastaSkills = Join-Path $env:USERPROFILE '.agents/skills'
foreach ($nomeSkill in $nomesSkills) {
    $destinoSkill = Join-Path $pastaSkills $nomeSkill
    if (Test-Path -LiteralPath $destinoSkill) {
        throw "A skill já existe: $destinoSkill. Compare as versões antes de atualizar."
    }
}
New-Item -ItemType Directory -Path $pastaSkills -Force | Out-Null
foreach ($nomeSkill in $nomesSkills) {
    Copy-Item -LiteralPath (Join-Path 'skills' $nomeSkill) -Destination $pastaSkills -Recurse
}
```

Exemplo de vínculo no Claude Code (Linux/macOS):

```bash
mkdir -p ~/.claude/skills
ln -s "$HOME/ferramentas/skills/codigo-legivel-humano" ~/.claude/skills/codigo-legivel-humano
```
