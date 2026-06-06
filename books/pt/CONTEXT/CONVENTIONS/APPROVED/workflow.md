# Convenção: Fluxo de Trabalho — Domínio Português

Migrado de `CONTEXT/CONVENTIONS/index.md` · 2026-06-06 15:30
Estado de todos os pontos abaixo: `accepted` (em uso desde 2026-06-05)

---

## CONV-007 · Trabalho com Variantes
`#CONV-007` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Ao criar v1 / v2 / v3 para cada capítulo ou elemento do universo:

| Variante | Foco |
|----------|------|
| v1 | A mais próxima do USER_DRAFT — preserva a entoação da autora, desvio mínimo |
| v2 | Reescrita estrutural — ritmo diferente, outro ponto de vista ou ordem de eventos |
| v3 | Experiência ousada — tom diferente, abertura não-convencional, mudança de registo |

Não tornar as variantes superficialmente diferentes — cada uma deve oferecer uma escolha real e significativa.

**Cada variante inclui três ficheiros:** `content.md` + `short.md` + `state-snapshot.md`.

---

## CONV-008 · Protocolo de Transição entre Capítulos
`#CONV-008` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Obrigatório antes de escrever o capítulo N:
1. `APPROVED/chapters/{N-1}.short.md` — o que aconteceu
2. `state-snapshot.md` da variante aprovada do capítulo N-1 — onde estão todos
3. `PLAN.md` — o que deve acontecer em N
4. `BRIEF.md` — tema, moral e âncoras físicas (secção «Tema e Moral»)
5. `APPROVED/universe/characters/` — fichas actuais (estáticas)
6. `APPROVED/universe/world.md` + `lore.md` — regras do mundo
7. `MEMORY.md` — preferências da autora para este livro
8. `FEEDBACK.md` — o que foi rejeitado e porquê

Não começar um capítulo sem este contexto.

**Estático vs. dinâmico:**
- `APPROVED/universe/` — factos permanentes. Muda raramente, apenas por instrução da autora.
- `state-snapshot.md` — estado actual após o último capítulo. Preenchido pelo agente após cada variante.

---

## CONV-009 · Estilos e RELEASES
`#CONV-009` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

- Um estilo vive em `APPROVED/universe/styles/{nome}.md`.
- Ao compilar um RELEASE: pegar em `APPROVED/chapters/` e reescrever na voz do estilo.
- Factos e enredo não mudam — apenas a apresentação.
- Cada RELEASE é independente e auto-suficiente.

---

## CONV-010 · Prioridade dos Espaços
`#CONV-010` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

```
APPROVED  >  USER_DRAFT  >  AGENT_DRAFT
```

Em conflito entre espaços — vence o de prioridade mais alta.
O agente nunca coloca no AGENT_DRAFT nada que contradiga USER_DRAFT ou APPROVED.
Contradição encontrada — registada em `STATUS.md → Decisões pendentes`, não corrigida unilateralmente.

---

## CONV-011 · O Que o Agente NÃO Faz Sem Instrução Explícita
`#CONV-011` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

- Não edita `USER_DRAFT/`.
- Não move conteúdo para `APPROVED/` — apenas a autora o faz.
- Não elimina variantes antigas de `AGENT_DRAFT/`.
- Não inventa novas personagens ou factos fora de `APPROVED/universe/`.
- Não altera factos já aprovados de `APPROVED/universe/`.
- Não actualiza `APPROVED/universe/` unilateralmente.
- Não regista o estado actual das personagens em `APPROVED/universe/` — apenas em `state-snapshot.md`.

---

## CONV-012 · Numeração de Capítulos
`#CONV-012` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Sempre três dígitos com zeros à esquerda: `001`, `002`, `099`, `100`.
Garante ordenação alfabética correcta até ao capítulo 999.

---

## CONV-013 · Ficheiros de Estado e Conceito
`#CONV-013` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

**`STATUS.md`** — registo de trabalho. Actualizado a cada mudança. Não confundir com PLAN.md.

**`BRIEF.md`** — documento de uma página. Inclui **tema, moral, anti-moral e âncoras físicas**. Lido antes de cada tarefa.

**`FEEDBACK.md`** — motivos de rejeição. Evita repetir erros.

**Lore para o cânone** — secção `## Lore para o Cânone` de cada `state-snapshot.md`. A autora decide o que mover para `APPROVED/universe/`.

---

## CONV-014 · Metodologia de Investigação
`#CONV-014` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

Para qualquer análise — seguir `CONTEXT/RESEARCH/craft/03_how_to_research.md`.

**Regra-chave:** análise começa com recolha de dados actuais, não com conhecimento de treino. Mínimo de 4 perspectivas para novo projecto: mercado, leitor, concorrência, prosa.

---

## CONV-015 · Nomenclatura e Consistência
`#CONV-015` · claude-sonnet-4-6 · 2026-06-05 12:00 · `accepted`

O nome da pasta em `RELEASES/` corresponde exactamente ao ficheiro de estilo em `APPROVED/universe/styles/`.
O conteúdo de `RELEASES/{style}/index.md` — texto completo do livro, não ligações.

---

## CONV-016 · Commits Git
`#CONV-016` · claude-sonnet-4-6 · 2026-06-06 · `accepted`

Todos os commits devem ser feitos exclusivamente em nome do proprietário. Sem atribuição de agentes — sem `Co-Authored-By:`, sem IDs de modelos, sem assinaturas de ferramentas de IA em mensagens de commit ou metadados.

O histórico de commits é o registo da autora, não do agente.

## CONV-016-A · Proposta de Mensagem de Commit
`#CONV-016-A` · claude-sonnet-4-6 · 2026-06-06 · `accepted`

Antes de qualquer commit, o agente deve propor a mensagem de commit e aguardar a aprovação do proprietário. Nunca fazer commit silenciosamente ou imediatamente.

Formato da proposta:
```
Mensagem de commit proposta:
> {mensagem}

Fazer commit?
```

Só fazer commit após confirmação explícita. Se o proprietário editar a mensagem — usar a versão editada literalmente.
