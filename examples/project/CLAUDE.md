# Exemplo de CLAUDE.md de projeto (surgical)

> Este arquivo fica na **raiz do projeto** (`<repo>/CLAUDE.md`).
> Estende o global com regras específicas DESTE projeto.
> **Mantenha curto.** Project-level vira lixo rápido se virar manifesto.

---

## Test Fixes
`AssertionError`: leia o teste, corrija todos os asserts (expected ← actual), posicione semanticamente, adicione asserts faltantes. **Nunca toque em asserts de [campo crítico do seu domínio].** Sempre adicione total de [sub-itens] quando o payload tiver:

```java
final List<Object> attachments = JsonPath.read(payload, "$.records[*].documents[*]");
assertEquals(N, attachments.size());
```

---

> **Por que essa é a única seção?**
>
> Tudo o que vale pra qualquer projeto está no global (`~/.claude/CLAUDE.md`):
> estilo de código, autonomia, debugging, commits, calibração.
>
> Aqui só entra o que é específico DESTE projeto — e mesmo assim, em forma de
> **regra testável**, não princípio abstrato. Se você se pegar escrevendo
> "code style preferences" no project-level, isso provavelmente pertence ao global.
>
> Sinais de que uma regra é boa pra project-level:
> - Cita campo, método, payload ou diretório do projeto.
> - Tem um trecho de código que mostra o padrão exato.
> - Resolve uma confusão real que aconteceu nesse projeto antes.
