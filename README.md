# full-power

**A skill cannot make the model smarter. It can make sure none of its capacity is wasted.**

`full-power` is an agent skill for Claude Code (and any agent that reads `SKILL.md` skills) for work where a mistake is expensive: client deliverables, production changes, decisions others act on, hard bugs. Bad results from strong models rarely come from missing intelligence. They come from the same few places: the hard step got the same quick pass as the easy ones, the first draft shipped as the answer, the author graded its own work, a fact was guessed instead of looked up, and the same miss came back next week.

The skill fixes each one and spends tokens only where it matters:

1. **Sort the task by risk.** Each step is marked routine, hard or irreversible, and the task gets an acceptance list a stranger could check.
2. **The right model per step.** Routine steps stay cheap and bulk reading goes to a small model. Only the hard step goes to the strongest model at high effort, with a short brief.
3. **Independent attempts plus a judge** when one answer is not enough: 2-3 subagents that never see each other, and a fresh judge that scores them against the acceptance list.
4. **A fresh-eyes verifier** that assumes the result is wrong and hunts for the failure before "done". It also runs as a pre-mortem before irreversible actions.
5. **A ceiling check.** Dates, prices, arithmetic, file contents and "does it work" come from tools, never from memory.
6. **A shared error log** that the next run reads first.

## See the difference

> **Owner:** "Write 3 headline options for a client's paid ad for a dental clinic. Best possible, no errors."

**Without the skill:** it loads the copy skills, writes 8-10 hooks itself and keeps the 3 it likes best. A reviewer checks policy. One author picks its own winners.

**With the skill:** it writes the acceptance list first (price matches the price list, no health promises, readable in one second). Then 3 independent strong-model attempts from different angles (price, convenience, trust), a fresh judge that scores them, and a verifier that attacks the winners for policy risk and unbacked claims. The report quotes the price line and says where the strong model was used.

**Skip it if** the task is a quick question or a one-line edit. It costs more on hard and irreversible steps, by design.

**Status:** new. Built from 3 weeks of a real setup (20+ Claude Code sessions for a small agency) where the owner wrote "no errors" in about 150 messages. The market check found strong process skills (superpowers) and code-only verification loops, but none that sets the model and effort per step, runs best-of-N with a judge, or checks the model's ceiling. Tested with and without the skill on 3 cases (ad copy, a production bot fix, a date question): 6/6 with it, 2.5/6 without. MIT. Issues welcome.

## Install

```bash
npx skills@1.8.1 add https://github.com/RabbitDesigns22/full-power/tree/3d3916102b6e6503424761f47d314ab03807e8b5
```

Or copy `skills/full-power/` into `~/.claude/skills/`.

## Works well with

- [`model-per-chat`](https://github.com/RabbitDesigns22/model-per-chat): the same idea across many chats: cheap base, strong model only for the hard step.
- [`never-twice`](https://github.com/RabbitDesigns22/never-twice): the shared error log that step 6 reads and writes.
- [`one-pass`](https://github.com/RabbitDesigns22/one-pass): the acceptance list and no blind retries.

## Español

**Máxima potencia.** Una skill no hace más inteligente al modelo, pero sí evita que desperdicie lo que tiene. Divide la tarea por riesgo: lo fácil queda barato, el paso difícil va al modelo más fuerte con esfuerzo alto, y lo que no tiene vuelta atrás espera una revisión. Cuando una sola respuesta no basta, hace 2 o 3 intentos independientes y un juez escoge. Antes de decir "listo", un revisor que no vio el trabajo busca el error. Las fechas, los precios y las cuentas salen de herramientas, nunca de memoria. Cada error queda anotado para la próxima vez.

Instalar: `npx skills@1.8.1 add https://github.com/RabbitDesigns22/full-power/tree/3d3916102b6e6503424761f47d314ab03807e8b5`

If it saved you a redo, a star helps other people find it.

## License

MIT. Made by [Rabbit Designs](https://github.com/RabbitDesigns22).
