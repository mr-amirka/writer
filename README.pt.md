# Espaço de Trabalho para Escrita de Livros com IA

Um espaço de trabalho estruturado para a escrita colaborativa de livros entre um autor humano e agentes de IA. Suporta múltiplos idiomas através de domínios de língua independentes (`books/{iso}/`).

Outros idiomas: [English](README.md) · [Русский](README.ru.md)

---

## O Que É Isto

Esta estrutura dá a ti e a um agente de IA um espaço organizado e partilhado para escrever um livro — com regras claras sobre quem possui o quê, como os rascunhos progridem até ao cânone e como o agente mantém o contexto entre capítulos sem reler o manuscrito completo de cada vez.

**Ideia central:** três espaços com prioridade estrita.

```
USER_DRAFT  →  AGENT_DRAFT  →  APPROVED
(o teu input bruto)  (o agente interpreta)  (cânone aprovado)
```

O agente nunca altera os teus rascunhos. Tu nunca escreves manualmente as interpretações do agente. Apenas tu moves o conteúdo para APPROVED.

---

## Estrutura do Repositório

```
books/
├── ru/                        # Domínio de língua russa
│   ├── CONTEXT/
│   │   ├── CONVENTIONS/       # Regras de comportamento do agente para esta língua
│   │   ├── MEMORY/            # Preferências universais do autor (todos os livros)
│   │   └── RESEARCH/          # Investigação de craft (estrutura, tamanho de capítulos, géneros...)
│   ├── _template/             # Copiar para criar um novo livro
│   └── {bookName}/            # Um livro específico
│
├── en/                        # Domínio de língua inglesa
│   ├── CONTEXT/
│   ├── _template/
│   └── {bookName}/
│
└── pt/                        # Domínio de língua portuguesa
    ├── CONTEXT/
    ├── _template/
    └── {bookName}/
```

Cada domínio de língua é independente. A pasta `_template/` é o teu ponto de partida em branco para um novo livro.

---

## Início Rápido

### 1. Criar um novo livro

Copia o template para o teu idioma:
```
books/pt/_template/  →  books/pt/o-meu-livro/
```

### 2. Preenche os ficheiros de conceito

Começa com estes ficheiros na pasta do novo livro — escreve livremente, sem formato obrigatório:

| Ficheiro | O que colocar |
|----------|--------------|
| `USER_DRAFT/idea.md` | O teu conceito bruto — fluxo de consciência, imagens, questões |
| `BRIEF.md` | Género, público, premissa, tema (máximo uma página) |
| `PLAN.md` | Plano capítulo a capítulo e arcos das personagens |
| `USER_DRAFT/universe/world.md` | Que tipo de mundo é este |
| `USER_DRAFT/universe/characters/{nome}.md` | Cada personagem — quem é, o que quer |

### 3. Pede ao agente interpretações

Aponta o agente para o `CLAUDE.md` do teu livro e pede-lhe para interpretar um elemento de cada vez. Por exemplo:
- «Interpreta `USER_DRAFT/idea.md` em três variantes»
- «Escreve três versões do capítulo 001 com base no meu rascunho»

O agente cria sempre **mínimo 3 variantes** (v1, v2, v3). Cada variante é uma abordagem significativamente diferente, não uma variação cosmética.

### 4. Revê e aprova

Lê as variantes. Quando estiveres pronto:
- Diz ao agente qual variante preferes (ou o que combinar)
- Move o conteúdo escolhido para `APPROVED/` tu mesmo — o agente nunca o faz unilateralmente

### 5. Continua a escrever

Para cada novo capítulo, o agente lê:
1. O resumo do capítulo aprovado anterior (`APPROVED/chapters/N.short.md`)
2. O snapshot de estado do último capítulo (`state-snapshot.md`)
3. Os factos aprovados do universo (`APPROVED/universe/`)
4. O plano narrativo (`PLAN.md`)

É assim que o agente mantém contexto sem reler o manuscrito inteiro.

---

## Os Três Espaços

### USER_DRAFT — o teu input bruto
Tudo o que escreves vai aqui primeiro. O agente lê isto mas **nunca o edita**. Escreve como quiseres: fragmentos, contradições, perguntas a ti mesmo. O agente vai interpretar, não corrigir.

### AGENT_DRAFT — interpretações do agente
O agente cria mínimo 3 variantes para cada capítulo ou elemento do universo. Cada pasta de variante contém:
- `content.md` — texto completo
- `short.md` — resumo de ~500 palavras para reutilização como contexto
- `state-snapshot.md` — estado do mundo após este capítulo (localizações das personagens, emoções, fios narrativos activos)

As variantes devem oferecer **escolhas reais** — ritmo diferente, ponto de vista, tom — não diferenças menores de formulação.

### APPROVED — o teu cânone
A prioridade mais alta. Apenas tu moves conteúdo para aqui. Quando algo é aprovado, o agente trata-o como facto imutável. Ao escrever qualquer novo capítulo, o agente lê APPROVED e ignora AGENT_DRAFT.

**Regra de prioridade:** `APPROVED > USER_DRAFT > AGENT_DRAFT`

Se o agente encontrar uma contradição entre espaços — regista-a em `STATUS.md` e aguarda a tua decisão. Nunca resolve contradições unilateralmente.

---

## Gestão de Estado

Um romance é longo demais para caber no contexto. A estrutura resolve isto com duas camadas:

**Camada estática — `APPROVED/universe/`**
Factos permanentes que raramente mudam: biografias das personagens, regras do mundo, história antes do início do livro.

**Camada dinâmica — `state-snapshot.md`**
O estado do mundo *após* cada capítulo: onde está cada personagem, o que sente, o que mudou, que fios narrativos estão em aberto. O agente preenche isto após cada variante.

Antes de escrever o capítulo N, o agente lê:
- `APPROVED/chapters/{N-1}.short.md` — o que aconteceu
- `state-snapshot.md` do capítulo N-1 — estado actual
- `APPROVED/universe/` — os factos permanentes

Isso é suficiente para escrever de forma consistente sem reler tudo.

---

## Acompanhamento do Trabalho

**`STATUS.md`** — o diário de trabalho do agente. Actualizado após cada acção. Contém:
- Tarefa actual
- Fase de cada capítulo e elemento do universo (USER_DRAFT / AGENT_DRAFT / APPROVED)
- Questões à espera da tua decisão

**`FEEDBACK.md`** — registo de variantes rejeitadas. Quando rejeitas uma variante, o agente regista o que não funcionou e porquê. Evita repetir os mesmos erros.

**`MEMORY.md`** — as tuas preferências para este livro específico (referências de tom, o que evitar, o que aprovaste).

---

## Estilos e Múltiplas Versões

Um livro pode ser lançado em múltiplos estilos narrativos — mesmo enredo e factos, voz e tom diferentes.

Os estilos vivem em `APPROVED/universe/styles/`. Cada estilo aprovado gera uma pasta `RELEASES/{nomeDoEstilo}/` separada com o texto completo do livro reescrito nessa voz.

Exemplos de estilos: `main` (principal), `romantic` (romântico), `gothic` (gótico).

**O estilo muda a apresentação, não o conteúdo.** O agente nunca muda o enredo, as personagens ou os factos ao aplicar um estilo.

---

## Domínios de Língua

Cada `books/{iso}/` é independente. Adicionar um novo idioma significa criar um novo domínio com o seu `CONTEXT/` (convenções e investigação nessa língua) e o seu `_template/`.

Domínios disponíveis:
- `books/ru/` — Russo (activo, inclui livro demo `mur/`)
- `books/en/` — Inglês (template pronto)
- `books/pt/` — Português (template pronto)

---

## Pontos de Entrada do Agente

O agente lê dois ficheiros CLAUDE.md no início de qualquer sessão:

1. **`/CLAUDE.md`** (raiz) — arquitectura global, regras de prioridade, protocolo de gestão de estado
2. **`books/{iso}/{book}/CLAUDE.md`** — contexto do livro específico, regras especiais, ligações rápidas

Antes de escrever um capítulo, o agente também lê BRIEF.md, PLAN.md, MEMORY.md e FEEDBACK.md do livro.

---

## Referência de Ficheiros

| Preciso de... | Ver aqui |
|--------------|---------|
| Criar um novo livro | `books/{iso}/_template/` |
| Verificar as regras de comportamento do agente | `books/{iso}/CONTEXT/CONVENTIONS/index.md` |
| Acompanhar o progresso do trabalho | `{book}/STATUS.md` |
| Ler o plano narrativo | `{book}/PLAN.md` |
| Ler o conceito + tema | `{book}/BRIEF.md` |
| Encontrar factos aprovados das personagens | `{book}/APPROVED/universe/characters/` |
| Encontrar regras do mundo aprovadas | `{book}/APPROVED/universe/lore.md` |
| Ver o estado actual após o último capítulo | `state-snapshot.md` do último capítulo aprovado |
| Registar o motivo de rejeição de uma variante | `{book}/FEEDBACK.md` |
| Ler investigação de craft | `books/{iso}/CONTEXT/RESEARCH/` |
