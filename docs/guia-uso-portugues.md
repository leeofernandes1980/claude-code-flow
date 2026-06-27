# Guia de uso do Claude-Flow em português

Este guia resume o fluxo principal para usar o projeto localmente, especialmente no Windows.

## 1. O que é o Claude-Flow

O Claude-Flow é uma plataforma para orquestrar agentes, tarefas, memória e workflows com foco em produtividade e automação.

Ele ajuda em cenários como:
- coordenar múltiplos agentes
- organizar tarefas e dependências
- manter contexto e memória entre execuções
- executar workflows de desenvolvimento e análise

## 2. Pré-requisitos

No Windows, o caminho mais simples é:
- Node.js 18 ou 20
- npm
- PowerShell

Se você estiver com problemas de dependências nativas, o fluxo básico ainda funciona com o modo compatível do projeto.

## 3. Instalação local

Na pasta do repositório, execute:

```powershell
cd C:\Users\User\Documents\GitHub\claude-code-flow
npm install --omit=optional
```

Depois, use o wrapper local:

```powershell
.\claude-flow.cmd --help
```

### 3.1 Usar em outros projetos

Para acionar este Claude-Flow (incluindo qualquer alteração feita neste repositório) a partir de **qualquer outra pasta de projeto**, faça o link global uma única vez:

```powershell
cd C:\Users\User\Documents\GitHub\claude-code-flow
npm link
```

Isso cria o comando `claude-flow` global apontando direto para esta pasta — qualquer mudança feita aqui já vale em todos os projetos, sem precisar reinstalar.

Depois, dentro do projeto onde você quer usar (ex: `camara-dashboard`):

```powershell
cd C:\Users\User\Documents\GitHub\camara-dashboard
claude-flow init --sparc
```

O `init --sparc` cria, dentro do projeto alvo:
- wrapper local `./claude-flow`
- pasta `.claude/` com configuração
- `CLAUDE.md` (instruções de projeto para o Claude Code)
- `.roomodes` com os 17 modos SPARC

A partir daí, use normalmente dentro daquele projeto:

```powershell
.\claude-flow status
.\claude-flow sparc run coder "implementar tal funcionalidade"
```

Para desfazer o link e voltar à versão publicada no npm:

```powershell
npm uninstall -g claude-flow
npm install -g claude-flow
```

## 4. Primeiros passos

### Verificar ajuda

```powershell
.\claude-flow.cmd --help
```

### Verificar status

```powershell
.\claude-flow.cmd status
```

### Iniciar a orquestração

```powershell
.\claude-flow.cmd start --ui --port 3000
```

A interface ficará disponível em:

```text
http://localhost:3000
```

## 5. Comandos mais úteis

### 5.1 Gerenciamento de agentes

Criar um agente:

```powershell
.\claude-flow.cmd agent spawn researcher --name "BotPesquisa"
```

Listar agentes:

```powershell
.\claude-flow.cmd agent list
```

### 5.2 Gerenciamento de tarefas

Criar uma tarefa:

```powershell
.\claude-flow.cmd task create research "Analisar requisitos do projeto"
```

Listar tarefas:

```powershell
.\claude-flow.cmd task list
```

### 5.3 Memória

Guardar informação:

```powershell
.\claude-flow.cmd memory store requisitos "Autenticação com JWT"
```

Consultar memória:

```powershell
.\claude-flow.cmd memory query jwt
```

### 5.4 Workflows e swarm

Executar um workflow simples:

```powershell
.\claude-flow.cmd workflow run
```

Executar uma coordenação de swarm:

```powershell
.\claude-flow.cmd swarm "Criar uma API básica" --strategy development --max-agents 3 --parallel
```

### 5.5 SPARC

Listar modos SPARC:

```powershell
.\claude-flow.cmd sparc modes
```

Executar um modo específico:

```powershell
.\claude-flow.cmd sparc run architect "Desenhar a arquitetura do sistema"
```

## 6. Fluxos recomendados

### Fluxo de pesquisa

```powershell
.\claude-flow.cmd memory store contexto "Objetivo da pesquisa"
.\claude-flow.cmd task create research "Coletar referências"
.\claude-flow.cmd swarm "Pesquisar melhores práticas" --strategy research
```

### Fluxo de desenvolvimento

```powershell
.\claude-flow.cmd task create development "Implementar funcionalidade principal"
.\claude-flow.cmd sparc run coder "Criar a funcionalidade"
.\claude-flow.cmd sparc run tdd "Adicionar testes"
```

## 7. Solução de problemas comuns

### Problema: erro ao instalar dependências nativas

Se aparecer erro com módulos nativos como `node-pty`, tente:

```powershell
npm install --omit=optional
```

Isso mantém o fluxo básico funcional sem depender de recursos nativos.

### Problema: comando não responde

Use o entrypoint local:

```powershell
node .\cli.js --help
```

### Problema: wrapper não funciona

Use o comando direto:

```powershell
node .\cli.js status
```

## 8. Resumo prático

Para começar hoje, use este fluxo:

```powershell
cd C:\Users\User\Documents\GitHub\claude-code-flow
npm install --omit=optional
.\claude-flow.cmd status
.\claude-flow.cmd agent spawn researcher
.\claude-flow.cmd task create research "Definir o próximo passo"
```

Esse já é um bom ponto de partida para explorar o projeto sem se perder na quantidade de recursos.
