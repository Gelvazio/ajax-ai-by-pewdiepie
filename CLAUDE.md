# Odysseus (odysseus-dev/odysseus)

Repositório de referência: https://github.com/odysseus-dev/odysseus (licença AGPL-3.0-or-later).

## O que é

Odysseus é um workspace de IA **self-hosted** (rodando na sua própria máquina ou servidor) que reúne:

- Chat e agentes, com modelos locais ou de API, tools, MCP, arquivos, shell, skills e memória
- Cookbook: recomendações de modelos conforme o hardware, download e serving
- Deep Research: pesquisa web em várias etapas, com leitura de fontes e geração de relatório
- Compare: teste cego lado a lado de modelos
- Documents: editor focado em escrita, com edições por IA, Markdown, HTML e CSV
- Email: inbox IMAP/SMTP com triagem, tags, resumos, lembretes e rascunhos de resposta
- Notes, Tasks e Calendar: lembretes, to-dos, tarefas agendadas para agentes e sync CalDAV
- Extras: galeria, temas, uploads, busca web, presets, sessões e 2FA

## Stack e estrutura

- **Backend:** Python 3.11+ com FastAPI/uvicorn. Entrada principal em `app.py`.
- **Frontend:** JavaScript/CSS estático em `static/` e `frontend/`. Testes de UI com Playwright (`package.json`).
- **Camadas principais:**
  - `core/`: auth, banco, middleware, sessões, I/O atômico e utilitários base
  - `routes/`: endpoints HTTP, um módulo ou pasta por área (chat, email, cookbook, memory, research, task, vault etc.)
  - `services/`: lógica de domínio (docs, memory, research, search, shell, skills, stt, tts, youtube, hwfit, faces)
  - `src/`: runtime de agentes, chat, deep research, integrações e helpers
  - `mcp_servers/`, `integrations/`, `companion/`, `swift/`: servidores MCP, integrações externas, app companion e código macOS
- **Testes:** pasta `tests/`, com marcadores de taxonomia (`area_security`, `area_routes`, `area_services`, `area_js` etc.) definidos em `pyproject.toml`.
- **Docs:** `docs/`, `website/` (guia de setup em `website/setup.md`), `ROADMAP.md`, `THREAT_MODEL.md`, `SECURITY.md`.

## Como rodar

Via Docker (recomendado):

```bash
cp .env.example .env
docker compose up -d --build
```

Depois, abrir `http://localhost:7011`. A senha inicial do admin aparece em `docker compose logs odysseus`.

Manual (Python 3.11+):

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python -m uvicorn app:app --host 127.0.0.1 --port 7000
```

## Branches e contribuição

- **`dev`:** branch padrão, onde todos os PRs entram. Muda com frequência.
- **`main`:** versão curada, atualizada a cada release.
- **Abra PRs contra `dev`**, não contra `main`.
- Prefira um bug fix ou uma feature por PR. Evite reescritas amplas e mudanças só de formatação.
- Para features grandes, abra uma issue antes com a abordagem.
- Veja `CONTRIBUTING.md` para o fluxo completo.

## Segurança (importante)

- Mantenha `AUTH_ENABLED=true` em qualquer deployment acessível pela rede.
- Mantenha `LOCALHOST_BYPASS=false` fora de desenvolvimento local.
- Não exponha portas brutas de modelos ou serviços publicamente.
- Não commite dados privados. O repo usa `.gitleaks.toml`.
- O projeto trata skills, notas, documentos, páginas buscadas e memórias como **dados não confiáveis** (prompt injection). Ao mexer nesses fluxos, mantenha essa premissa.
- Leia `THREAT_MODEL.md` antes de mudar auth, SSRF, shell, uploads ou confinamento de arquivos.

## Prioridades abertas (ROADMAP.md)

- Estabilizar bugs e fazer smoke tests de instalação em Linux, macOS e Windows (Docker, Python nativo e WSL)
- Auditar integrações: o que funciona de fato, o que precisa de docs e o que remover
- Confiabilidade e suporte do Cookbook em outras máquinas (GPUs, drivers, shells, ambientes Python), incluindo SGLang
- Presets de Deep Research por hardware e ranking melhor de modelos no Cookbook
- Mensagens de erro e logs úteis no Cookbook (comando, saída e próximos passos)
- Reduzir o "inchaço" de prompt do modo agente para modelos locais menores (4k/8k/16k de contexto)
- Speculative decoding para modelos locais, com draft model de mesmo tokenizer
- Auditoria de prompt injection em skills, notas, documentos e memórias
- Melhorar sinalização de estado degradado (ChromaDB, SearXNG, email, ntfy, probes de provedores)
- Performance de email (IMAP/SMTP, cache e prefetch)
- Auditoria de setup dos provedores Anthropic, Gemini, Groq, xAI, OpenRouter, OpenAI e DeepSeek
- Refatorações: limpeza de CSS (`static/style.css`), helper compartilhado para tours (`tour-core.js`) e posicionamento de modais

## Convenções para trabalhar aqui

- Antes de começar, procure issues e PRs existentes sobre o assunto.
- Faça mudanças pequenas, focadas e fáceis de revisar.
- Adicione ou atualize testes na pasta `tests/` correspondente à área alterada.
- Ao mexer em CSS, atenção aos overrides de `@media` mobile: muitos bugs de "CSS não mudou" vêm daí.
