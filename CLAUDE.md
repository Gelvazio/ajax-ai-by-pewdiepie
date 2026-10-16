# ajax-ai-by-pewdiepie

Repositório: https://github.com/Gelvazio/ajax-ai-by-pewdiepie
Licença: MIT (Gelvazio Camargo, 2026).

## Estado atual

- O projeto está no início. O README tem só o título, sem descrição.
- Não há código-fonte ainda. O histórico tem um único commit, "Initial commit".
- O `.gitignore` é um modelo para C++ com CMake e JetBrains (CLion). Isso sugere uma base C++, mas ainda não está confirmado.

## Projetos clonados neste repositório

Cada pasta abaixo é uma cópia dos arquivos de outro repositório, sem o `.git`. Não são submódulos.

| Pasta | Origem | O que é |
|---|---|---|
| `odysseus/` | odysseus-dev/odysseus | Workspace de IA self-hosted: chat, agentes, pesquisa profunda, documentos, email, notas e calendário |
| `i-have-adhd/` | ayghri/i-have-adhd | Skill para agentes de código que evita que respostas importantes fiquem escondidas em respostas longas |
| `OmniRoute/` | diegosouzapw/OmniRoute | Gateway de IA local que expõe uma API compatível com a da OpenAI e faz fallback entre provedores |
| `ponytail/` | DietrichGebert/ponytail | Skill para Claude Code (detalhes não verificados) |
| `matt-pocock-skills/` | mattpocock/skills | Coleção de skills para engenharia de software: PRDs, planos, TDD, modelagem de domínio |
| `superpowers/` | obra/superpowers | Conjunto de skills para desenvolvimento com Claude Code |
| `diagram-design/` | cathrynlavery/diagram-design | Skill que gera diagramas técnicos a partir de linguagem natural |
| `humanizer/` | blader/humanizer | Skill para reescrever textos de IA para soarem mais naturais (pelo nome e pela busca) |
| `graphify/` | Graphify-Labs/graphify | Skill para Claude Code (detalhes não verificados) |
| `addy-osmani-skills/` | addyosmani/agent-skills | Skills de engenharia de produção para agentes de código |
| `impeccable/` | pbakaus/impeccable | Skill (detalhes não verificados) |
| `repolyze/` | OssiumOfficial/Repolyze | Ferramenta para analisar repositórios, feita com Next.js e pnpm |
| `foreman/` | VisionForge-OU/foreman | Orquestrador em terminal que supervisiona agentes headless do Claude Code em um pipeline com etapas de aprovação |
| `mineru/` | opendatalab/MinerU | Converte PDFs e documentos para Markdown ou JSON, com foco em layouts complexos, tabelas e fórmulas |
| `openrig/` | mvschwarz/openrig | Runtime para rodar um time de agentes (Claude Code e Codex) definido em YAML, com um comando de inicialização |
| `hindsight/` | vectorize-io/hindsight | Camada de memória para agentes, com API, cliente e integrações (detalhes pela busca e pelo README) |
| `crm/` | trycompai/crm | CRM de código aberto feito para ser usado por agentes de IA (Comp AI CRM) |
| `paddleocr/` | PaddlePaddle/PaddleOCR | Kit de OCR e engine de IA para documentos, com API, SDK e integrações |

Não clonado ainda: "Security Audit Skill" (vários candidatos, sem confirmação).

## Regras por projeto

Como as pastas não têm `.git`, para atualizar uma delas é preciso recopiar o repositório original.

- **`odysseus/`:** rode com Docker (`docker compose up -d --build`) e mantenha `AUTH_ENABLED=true` em qualquer rede acessível.
- **`i-have-adhd/`:** leia o `AGENTS.md` do próprio repositório antes de instalar a skill.
- **`OmniRoute/`:** nunca commite chaves de API. Use o `.env.example` como modelo e leia o `SECURITY.md` antes de expor o gateway.
- **`ponytail/`:** leia o README antes de usar. Os detalhes ainda não foram verificados aqui.
- **`matt-pocock-skills/`:** use as skills como ponto de partida e adapte ao projeto. Confira a licença antes de redistribuir.
- **`superpowers/`:** compare os nomes das skills com as que já existem antes de instalar, para evitar conflito.
- **`diagram-design/`:** revise o diagrama gerado antes de usá-lo em documentação ou apresentação.
- **`humanizer/`:** use para revisar a escrita, não para ocultar que um texto foi gerado por IA.
- **`graphify/`:** leia o README antes de usar. Os detalhes ainda não foram verificados aqui.
- **`addy-osmani-skills/`:** use como checklist de engenharia e adapte ao time, sem seguir tudo ao pé da letra.
- **`impeccable/`:** leia o README antes de usar. Os detalhes ainda não foram verificados aqui.
- **`repolyze/`:** nunca commite o `.env` nem credenciais do banco Prisma.
- **`foreman/`:** copie o `config.sample.yaml` para configurar, e revise o escopo antes de deixar o supervisor rodar agentes.
- **`mineru/`:** confira manualmente tabelas e fórmulas na conversão, que são as partes com mais erro.
- **`hindsight/`:** leia o `.env.example` e a pasta `docker` antes de subir o serviço, e não exponha a API de memória sem autenticação.
- **`paddleocr/`:** instale o pacote com as dependências do `requirements.txt` ou `pyproject.toml`, e teste o OCR com um documento seu antes de usar em produção.
- **`crm/`:** leia o `AGENTS.md` e o `.env.example` antes de subir o projeto, e nunca commite o `.env` com credenciais.
- **`openrig/`:** leia o `docs/reference/getting-started.md` e a seção "What OpenRig changes on your machine" do README antes de rodar, porque ele grava hooks e configurações de confiança nos provedores.

## Para quem trabalhar aqui

- Antes de criar estrutura, confirme com o dono do projeto qual é o objetivo, a linguagem e o público.
- Quando o projeto ganhar descrição e código, atualize este arquivo com: o que o sistema faz, como compilar e rodar, a estrutura de pastas e as convenções do time.
