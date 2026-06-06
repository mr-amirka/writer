# RELEASES — Compilações Finais

Versões montadas do livro para publicação ou distribuição. Cada pasta é um estilo narrativo separado.

**O agente monta um RELEASE a pedido do autor, pegando em `APPROVED/chapters/` e aplicando o estilo de `APPROVED/universe/styles/`.**

---

## Estrutura

```
RELEASES/
├── main/                  # Estilo principal (styles/main.md) — texto completo
│   └── index.md
├── romantic/              # Estilo: styles/romantic.md
│   ├── index.md           # Texto completo do livro neste estilo
│   └── metadata.md        # O que mudou em relação ao main
├── gothic/                # Estilo: styles/gothic.md
│   ├── index.md
│   └── metadata.md
└── {nomeDoEstilo}/        # Qualquer outro estilo
    ├── index.md
    └── metadata.md
```

**Princípio de nomenclatura:** a pasta tem o mesmo nome do ficheiro de estilo em `APPROVED/universe/styles/`. Sem `raw`, `default` ou outros pseudónimos.

**Conteúdo de index.md:** texto completo do livro, não ligações. O leitor deve ver o resultado final sem precisar de abrir outros ficheiros.

---

## Processo de Montagem do RELEASE

1. Verificar que todos os capítulos necessários estão em `APPROVED/`.
2. Carregar o estilo de `APPROVED/universe/styles/{nomeDoEstilo}.md`.
3. Para cada capítulo aprovado: reescrever na voz do estilo, preservando factos e enredo.
4. Montar: prólogo + capítulos por ordem + epílogo → `RELEASES/{nomeDoEstilo}/index.md`.
5. Preencher `metadata.md`.

**O estilo não muda o enredo, as personagens ou os factos — apenas a forma de apresentação.**
