# Convenção: Completude de Tarefas — Domínio Português

Aprovado pela autora em conversa · 2026-06-06
Equivalente canónico: `books/en/CONTEXT/CONVENTIONS/APPROVED/completeness.md`

---

## CONV-001 · Lista de Verificação de Completude
`#CONV-001` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Antes de declarar qualquer tarefa concluída, o agente deve verificar:

1. **Todos os ficheiros planeados criados.** Se a tarefa envolve N ficheiros, confirmar que N ficheiros existem.
2. **Referências cruzadas actualizadas.** Qualquer ficheiro que mencione a estrutura criada — actualizado.
3. **Resto declarado explicitamente.** Se algo foi intencionalmente omitido, indicar pelo nome. Nunca parar silenciosamente a meio.

Proibido: terminar uma resposta com "concluído" quando a lista de ficheiros está incompleta.

---

## CONV-002 · Declaração de Âmbito
`#CONV-002` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Para qualquer tarefa que crie ou modifique mais de 5 ficheiros: antes de começar, declarar o âmbito explicitamente:

> «Vou criar X ficheiros em Y pastas: [lista]. A começar.»

---

## CONV-003 · Verificação de Paridade Estrutural
`#CONV-003` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Ao duplicar uma estrutura para outro domínio:

1. Contar ficheiros na referência.
2. Contar ficheiros na nova estrutura.
3. Declarar a comparação explicitamente.
4. Se houver diferença — indicar quais ficheiros faltam e se é intencional.

---

## CONV-004 · Definição de Livro Demo Completo
`#CONV-004` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Um livro demo considera-se **minimamente completo** quando contém os ficheiros listados em `books/en/CONTEXT/CONVENTIONS/APPROVED/completeness.md` (tabela CONV-004).

Considera-se **completamente ilustrado** (mostrando o sistema de continuidade) apenas quando também tem o capítulo 002 com variantes.

---

## CONV-005 · Actualização do STATUS em Caso de Interrupção
`#CONV-005` · claude-sonnet-4-6 · 2026-06-06 15:30 · `accepted`

Se uma tarefa multi-passo for interrompida:

1. Actualizar `STATUS.md` dos livros afectados — indicar o que foi feito e o que não foi.
2. Na resposta à autora, indicar explicitamente: «Tarefa parcialmente concluída. Feito: [lista]. Falta: [lista].»
3. Nunca deixar STATUS.md num estado que implique conclusão quando a tarefa não está concluída.
