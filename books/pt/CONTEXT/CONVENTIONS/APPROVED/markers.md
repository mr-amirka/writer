# Convenção: Sistema de Marcadores

---

## CONV-006 · Formato do Marcador
`#CONV-006` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Cada ponto em cada ficheiro (excepto RELEASES e ficheiros de saída limpa equivalentes) carrega um marcador:

```
`#CONV-NNN` · {agent-id} · YYYY-MM-DD HH:MM · `{status}`
```

- **ID** — globalmente único, sequencial. Prefixo: `CONV-` universal, `CONV-PT-` / `CONV-EN-` / `CONV-RU-` específico de domínio.
- **Agent** — ID do modelo que propôs o ponto, ex. `claude-sonnet-4-6`.
- **Timestamp** — ao minuto, ISO-8601.
- **Status** — um de: `draft` · `accepted` · `rejected`.

Quando um ponto é aceite ou rejeitado, o campo de estado é actualizado no lugar. O texto original **nunca é eliminado** — apenas o campo de estado muda.

---

## CONV-006-A · Formato de Questão
`#CONV-006-A` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Quando uma decisão requer a participação da autora, o agente levanta uma questão marcada:

```
`?CONV-NNN-Q1` · {agent-id} · YYYY-MM-DD HH:MM

**Texto da questão?**

→ **A:** opção A
→ **B:** opção B
→ **C:** opção C

↳ *Aguarda a autora*
```

Quando a autora responde, a resposta é **acrescentada abaixo** das opções — as opções não são removidas:

```
↳ *Aguarda a autora*

↳ **Autora · YYYY-MM-DD HH:MM:** B — porque...
```

---

## CONV-006-B · Âmbito dos Marcadores
`#CONV-006-B` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

**Ficheiros que requerem marcadores:** todos os ficheiros `.md` no repositório, excepto:
- `RELEASES/*/index.md` e ficheiros de saída limpa similares (texto do livro para leitores)
- `RELEASES/*/metadata.md`
- `README.md`, `README.ru.md`, `README.pt.md` (documentos públicos)

**Ficheiros que requerem marcadores obrigatoriamente:** CONVENTIONS/, CONTEXT/, STATUS.md, BRIEF.md, PLAN.md, MEMORY.md, FEEDBACK.md, APPROVED/universe/*, state-snapshot.md.

---

## Questões em Aberto

`?CONV-006-Q1` · claude-sonnet-4-6 · 2026-06-06 15:30

**Os marcadores devem ser aplicados retroactivamente a todos os ficheiros existentes, ou apenas a ficheiros criados ou significativamente editados daqui para a frente?**

→ **A:** Retroactivo — todos os ficheiros existentes recebem marcadores numa única passagem agora (~100+ ficheiros).
→ **B:** Apenas para a frente — os marcadores aplicam-se a novos ficheiros e ficheiros activamente editados; os existentes não são tocados sem outra razão.
→ **C:** Híbrido — ficheiros de CONVENTIONS e meta (STATUS, BRIEF, PLAN, MEMORY, FEEDBACK, state-snapshot, universe) são marcados agora; os ficheiros de texto dos capítulos apenas quando novos capítulos são adicionados.

↳ *Aguarda a autora*

↳ **Autora · 2026-06-06:** C — marcar ficheiros de CONVENTIONS e meta agora; ficheiros de capítulos apenas quando novos capítulos são adicionados.

---

`?CONV-006-Q2` · claude-sonnet-4-6 · 2026-06-06 15:30

**Espaço de nomes dos IDs: devem ser globalmente únicos em todos os domínios, ou limitados por domínio?**

→ **A:** Global — `CONV-001` significa a mesma regra em `books/ru/`, `books/en/`, `books/pt/`. Regras específicas de domínio recebem prefixo: `CONV-PT-001`.
→ **B:** Por domínio — cada domínio tem o seu próprio contador a partir de 001; referências entre domínios usam notação de caminho completo.

↳ *Aguarda a autora*

↳ **Autora · 2026-06-06:** A — IDs globais, um único espaço de nomes para todos os domínios.
