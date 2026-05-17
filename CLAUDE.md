# CLAUDE.md

> Contexto persistente DESTE projeto. Estende o global (`~/.claude/CLAUDE.md`).
>
> **Curto por princípio.** Code style, autonomia, debugging, commits, calibração
> → ficam no global. Aqui SÓ entram regras específicas testáveis deste projeto.

---

## Commits (override do global)

Projeto pessoal, sem Jira. Override do padrão global de commits:

- Formato: `type: descrição curta em português` (sem colchetes, sem TICKET).
- Idioma: PT-BR.
- Types permitidos: os mesmos do global (`feat`, `fix`, `chore`, `refactor`, `docs`, `test`, `style`, `perf`, `ci`, `build`).
- Mantido do global: sem body, sem footer, sem `Co-Authored-By`.

```
feat: estrutura inicial do template
fix: corrige path do hook no Windows
docs: adiciona exemplo de settings global
```

---

> **Antes de adicionar nova seção, pergunte:**
>
> 1. Vale só pra este projeto, ou pra qualquer projeto?
>    → "Qualquer" = vai pro global.
> 2. Tem campo/método/path específico?
>    → Se não, é princípio abstrato — não pertence aqui.
> 3. Resolve uma confusão real que já aconteceu?
>    → Se "pode acontecer", não documente ainda. Espera acontecer.
>
> Project-level que vira manifesto = lixo.
> **Quando em dúvida, não adicione.**
