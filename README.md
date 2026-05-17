# Claude Code para Devs de Automação

Setup opinionado de Claude Code pra quem escreve bots, scrapers e automações em Java ou Python — extraído de um setup real em produção, anonimizado pra publicar.

**Não é tutorial introdutório.** Pressupõe que você já configurou `CLAUDE.md`, criou pelo menos um subagent, e mexeu em `settings.json`. Se ainda não, pegue antes a [documentação oficial](https://docs.claude.com/en/docs/claude-code/overview) e volte aqui.

---

## A divisão que muda tudo: global vs project

Tem dois níveis de configuração no Claude Code:

- **Global** (`~/.claude/`): vale pra todas as sessões da sua máquina. Princípios, estilo, preferências pessoais.
- **Project** (`<repo>/CLAUDE.md` e `<repo>/.claude/`): vale só pra um projeto. Vai pro git.

A maioria dos exemplos públicos coloca tudo no project-level. Vira manifesto de 200 linhas no `CLAUDE.md` da raiz, com regras genéricas que aplicariam a qualquer projeto. Isso é **ruído por construção**: cada novo projeto começa com o mesmo lixo.

O caminho que funciona pra mim:

- Princípios universais (estilo de código, autonomia, debugging, commits, calibração) → **global**
- Regras com nome de campo, método ou path → **project**, curto e cirúrgico

Esse repo materializa essa divisão.

---

## O que tem aqui

```
claude-code-automation/
├── CLAUDE.md                              ← template project-level mínimo
├── .claude/
│   ├── agents/review-java.md              ← agente production-grade pra revisão Java
│   └── settings.json                      ← permissions + hook bloqueando push pra main
└── examples/
    ├── global/
    │   ├── CLAUDE.md                      ← exemplo de global real (princípios opinionados)
    │   └── settings.json                  ← settings.json global anonimizado
    └── project/
        └── CLAUDE.md                      ← exemplo de project-level cirúrgico
```

**Os arquivos que valem ler com calma:**

- [`examples/global/CLAUDE.md`](examples/global/CLAUDE.md) — onde mora o conhecimento real. Seções sobre autonomia, calibração, surgical changes, pipeline coverage, evidence-based debugging. Adapte como template do seu `~/.claude/CLAUDE.md`.
- [`.claude/agents/review-java.md`](.claude/agents/review-java.md) — agente de revisão Java com 9 categorias de checklist, protocolo de sub-agentes paralelos, verification gate. Suporta modo full project ou git diff.
- [`examples/project/CLAUDE.md`](examples/project/CLAUDE.md) — exemplo do que um `CLAUDE.md` de projeto bem feito parece. Curto por princípio.

---

## Três decisões opinionadas

### 1. Sem `.mcp.json` na raiz

MCP servers (Context7, Playwright, Memory) quase sempre são pessoais. Você usa em todo projeto, então moram no global (ver `examples/global/settings.json > mcpServers`). Criar `.mcp.json` no projeto só faz sentido pra MCPs **inerentemente do projeto** — um postgres-mcp apontando pro DB específico, por exemplo. Se você não tem isso, não cria o arquivo.

### 2. `CLAUDE.md` raiz tem 20 linhas

Project-level vira lixo quando vira manifesto. Toda regra que aplica a "qualquer projeto" pertence ao global. No project só entra o que cita campo, método, path ou comportamento específico DESTE projeto — em forma de **regra testável**, não princípio abstrato.

O arquivo na raiz é template com 3 perguntas anti-bloat. O exemplo real preenchido está em `examples/project/CLAUDE.md`: uma seção, com snippet de código, e uma nota explicando por que é tão curto.

### 3. `bypassPermissions` no global

O `examples/global/settings.json` usa `defaultMode: bypassPermissions` + `skipDangerousModePermissionPrompt: true`. Isso é **YOLO mode**: Claude executa qualquer comando sem perguntar. Não é seguro por default — é escolha consciente baseada em:

- Velocidade de iteração > prompt de permissão a cada ação
- A confiança no agente vem da seção `Autonomy` do CLAUDE.md global, com guarda explícita em `Stop & Ask`
- Repos importantes têm o hook do `.claude/settings.json` (project-level) que bloqueia push direto pra main

**Use por sua conta e risco.** Em projeto crítico, prefira `defaultMode: ask` no global e mantenha o hook.

---

## Como usar

1. Adapta o `examples/global/CLAUDE.md` ao seu estilo, salva em `~/.claude/CLAUDE.md`
2. Adapta o `examples/global/settings.json` (cautela nos paths e na escolha de `defaultMode`), salva em `~/.claude/settings.json`
3. Em cada projeto novo, copia `CLAUDE.md` (raiz) e `.claude/settings.json` do template, adapta
4. Quando aparecer uma regra recorrente específica do projeto, adiciona ao `CLAUDE.md` no formato do exemplo cirúrgico

**Isso não é boilerplate pra clonar e usar.** É template pra pensar.

---

## O que NÃO está aqui

- Subagents alternativos além do `review-java` — tenho outros, ficaram fora pra manter o repo enxuto
- Hooks elaborados (quality gates, lint automático, telemetria) — área de exploração contínua
- Comandos customizados (`/commands`) — próximo passo de iteração
- Skills — outra camada que merece repo próprio

Brevidade é feature. Se sentir falta de algo, provavelmente cabe num post separado.

---

## Sobre

Construído com base no setup que uso em produção pra bots de automação — Java/Spring Boot, Python/Scrapy, Playwright, integração com IA local via Ollama.

Compartilho mais sobre Claude Code, automação e scraping no LinkedIn: [linkedin.com/in/laercio-sfilho](https://linkedin.com/in/laercio-sfilho).

Sugestões, críticas e issues são bem-vindas.

---

📝 Por **Laércio de Sant' Anna Filho** · [LinkedIn](https://linkedin.com/in/laercio-sfilho) · [GitHub](https://github.com/dev-laerciosf)