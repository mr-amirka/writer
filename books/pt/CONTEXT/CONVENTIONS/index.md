# Convenções do Agente — domínio português

Regras de comportamento do agente de IA ao trabalhar com livros em português.
Ler em conjunto com `/CLAUDE.md`.
Livros e contexto do domínio: `books/pt/`

---

## Língua e Comunicação

- Todas as respostas e textos — **em português**, salvo indicação explícita do autor.
- Ao discutir estrutura ou variantes — conciso, sem enchimento.
- Não explicar o que é óbvio a partir do código ou da estrutura de ficheiros.

---

## Formatação de Texto

### Diálogos
Padrão português: travessão (—), não aspas.
```
— Tens a certeza? — perguntou ele.
— Não — respondeu ela. — Mas não há outro caminho.
```
Aspas «guillemets» — apenas para citações, títulos, pensamentos no fluxo de consciência.

### Parágrafos
- Diálogo — sempre novo parágrafo.
- Acção do falante — no mesmo parágrafo que a fala, separada por travessão.
- Mudança de cena ou de tempo — linha em branco + `* * *`.

### Números no texto
Até dez — por extenso. A partir de 10 — numerais em cenas de acção, por extenso em cenas meditativas.

---

## Trabalho com Variantes

Ao criar v1 / v2 / v3 para cada capítulo:

| Variante | Foco |
|----------|------|
| v1 | A mais próxima do USER_DRAFT: preserva a entoação do autor, desvio mínimo |
| v2 | Reescrita estrutural: ritmo diferente, outro ponto de vista ou ordem de eventos |
| v3 | Experiência ousada: tom diferente, abertura não-convencional, mudança de registo |

Não tornar as variantes superficialmente diferentes — cada uma deve oferecer uma escolha real.

**Cada variante inclui três ficheiros:** `content.md` + `short.md` + `state-snapshot.md`.
Isto permite ao autor comparar não só o texto, mas também o estado do mundo após cada variante.

---

## Protocolo de Transição entre Capítulos

Obrigatório antes de escrever o capítulo N:
1. `APPROVED/chapters/{N-1}.short.md` — o que aconteceu
2. `state-snapshot.md` da variante aprovada do capítulo N-1 — onde estão todos
3. `PLAN.md` — o que deve acontecer em N
4. `BRIEF.md` — tema, moral e âncoras físicas (secção «Tema e Moral»)
5. `APPROVED/universe/characters/` — fichas actuais das personagens (estáticas)
6. `APPROVED/universe/world.md` + `lore.md` — regras do mundo
7. `MEMORY.md` — preferências do autor para este livro
8. `FEEDBACK.md` — o que foi rejeitado anteriormente e porquê

Não começar um capítulo sem este contexto.

**Estático vs. dinâmico:**
- `APPROVED/universe/` — factos permanentes (biografias, regras do mundo, história anterior ao livro). Muda raramente, apenas por instrução do autor.
- `state-snapshot.md` — estado actual após o último capítulo (localização, emoções, estado dos artefactos). Preenchido pelo agente após cada variante.

---

## Estilos e RELEASES

- Um estilo vive em `APPROVED/universe/styles/{nome}.md`.
- Ao compilar um RELEASE, o agente pega em `APPROVED/chapters/` e reescreve na voz do estilo.
- Os factos e o enredo não mudam — apenas a forma de apresentação.
- Cada RELEASE é independente e auto-suficiente.

---

## Prioridade dos Espaços

```
APPROVED  >  USER_DRAFT  >  AGENT_DRAFT
```

Em caso de conflito de factos entre espaços — vence o de prioridade mais alta.
O agente nunca coloca no AGENT_DRAFT nada que contradiga o USER_DRAFT ou o APPROVED.
Contradição encontrada — registada em `STATUS.md → Decisões pendentes`, não corrigida unilateralmente.

## O Que o Agente NÃO Faz Sem Instrução Explícita

- Não edita `USER_DRAFT/`.
- Não move conteúdo para `APPROVED/` — apenas o autor o faz.
- Não elimina variantes antigas de `AGENT_DRAFT/`.
- Não inventa novas personagens ou factos do mundo fora de `APPROVED/universe/`.
- Não altera factos já aprovados de `APPROVED/universe/`.
- Não actualiza `APPROVED/universe/` unilateralmente — apenas por instrução explícita do autor.
- Não regista o estado actual das personagens em `APPROVED/universe/` — apenas em `state-snapshot.md`.

---

## Tamanho dos Capítulos

**Mínimo:** 10 000 caracteres (~1 700 palavras) — menos é um fragmento, não um capítulo.
**Intervalo alvo:** 20 000–30 000 caracteres (~3 500–5 000 palavras) — padrão para prosa literária.
**Máximo sem justificação:** 50 000 caracteres. Mais longo apenas se o conteúdo o exigir.

Se um capítulo ficar abaixo do mínimo — registar o motivo em `state-snapshot.md` (secção «Avisos»).
A consistência é mais importante do que qualquer número específico: o desvio em relação à média do livro não deve ultrapassar 40%.

Análise detalhada: `CONTEXT/RESEARCH/craft/02_chapter_size.md`

---

## Numeração de Capítulos

Sempre três dígitos com zeros à esquerda: `001`, `002`, `099`, `100`.
Isto garante ordenação alfabética correcta até ao capítulo 999.

---

## Ficheiros de Estado e Conceito

**`STATUS.md`** — registo de trabalho do agente. O agente actualiza-o a cada mudança de estado de uma variante ou elemento do universo. Estrutura: tabelas com colunas de fase (USER_DRAFT → AGENT_DRAFT → APPROVED). Não confundir com PLAN.md (plano narrativo, não registo de trabalho).

**`BRIEF.md`** — documento de uma página do livro. Inclui género, público, personagens, estrutura, **e também tema, moral, anti-moral e âncoras físicas**. O agente lê-o antes de cada tarefa do livro.

**`FEEDBACK.md`** — motivos de rejeição de variantes. O agente preenche quando o autor rejeita uma variante: o que especificamente não funcionou e porquê. Evita repetir os mesmos erros.

**Lore para o cânone** — acompanhado na secção `## Lore para o Cânone` de cada `state-snapshot.md`. O agente regista novos factos sobre o mundo e as personagens estabelecidos pela primeira vez no capítulo. O autor decide o que mover para `APPROVED/universe/`.

---

## Metodologia de Investigação

Para qualquer análise — de mercado, de género, estrutural — o agente segue a metodologia em `CONTEXT/RESEARCH/craft/03_how_to_research.md`.

**Regra-chave:** a análise começa com a recolha de dados actuais, não com o conhecimento de treino do modelo. O conhecimento de treino são dados secundários com data de corte. O mercado actual, os padrões dos leitores e as tendências de género requerem pesquisa fresca.

Mínimo de 4 perspectivas para um novo projecto de livro: mercado, leitor, concorrência, prosa.

---

## Nomenclatura e Consistência

O nome da pasta em `RELEASES/` deve corresponder exactamente ao nome do ficheiro de estilo em `APPROVED/universe/styles/`.
- Estilo `main.md` → pasta `RELEASES/main/`
- Estilo `gothic.md` → pasta `RELEASES/gothic/`
- Sem pseudónimos (`raw`, `default`, `base`).

O conteúdo de `RELEASES/{style}/index.md` — texto completo do livro, não ligações para outros ficheiros.
