# SkeletonCrew

## Portfolio overview

SkeletonCrew is a documentation-first design for coordinating
AI-assisted development tasks across different executors.

**Implemented as a specification:**
- Task lifecycle and routing rules.
- Separation of roles, executors, and models.
- Markdown task schema with review and approval gates.
- Context, access, and execution-budget guidelines.

**Not implemented yet:** automatic dispatch, agent adapters,
task queues, execution runtime, and automated retries.

The goal is to make AI-assisted development traceable,
reviewable, and controlled by a human operator.

## Working documentation


Ручная диспетчерская Skeleton Crew Games: выбрать проект, описать задачу, назначить роль и исполнителя, получить и проверить результат.

**Role** — функция, например `Writer`. **Executor** — механизм выполнения, например `Codex`. Модель выбирается отдельно: `Ollama` — исполнитель, `llama3.2:3b` — модель.

## Начать работу

1. Настрой `config/local.yaml` по [примеру](config/local.example.yaml): укажи локальные корни проектов. Этот файл исключён из Git.
2. Открой [индекс задач](TASKS.md) или создай карточку в `tasks/` по [шаблону](DISPATCH.md#шаблон-карточки).
3. Выбери [роль](ROLES.md) и подходящего [исполнителя](EXECUTORS.md). Проверь его доступ, инструменты и бюджет, затем вручную переведи карточку в `routed`.
4. Передай поручение исполнителю; веди статус, проверки и решение человека в самой карточке.

Основной путь: `inbox → routed → running → verifying → needs_human → done`. Правила повторов и остановки описаны в [DISPATCH.md](DISPATCH.md).

## Где что хранится

| Источник | Содержимое |
| --- | --- |
| [PROJECTS.md](PROJECTS.md) | Project key, назначение и границы проектов |
| [ROLES.md](ROLES.md), [EXECUTORS.md](EXECUTORS.md) | Функции и механизмы выполнения |
| `tasks/*.md` | Текущее состояние, поручение, результат и история каждой задачи |
| [TASKS.md](TASKS.md) | Только ссылки на карточки |
| `config/local.yaml` | Локальные пути и настройки подключения; не публикуется |
| [CONTEXT_PACKETS.md](CONTEXT_PACKETS.md), [TOKEN_BUDGET.md](TOKEN_BUDGET.md) | Контекст и выбор уровня модели |
| [AGENTS.md](AGENTS.md) | Правила для работающего с репозиторием агента |

Это подготовка формата для **crew-dispatcher v0.1**. Движка, адаптеров, очереди, автоматического запуска и повторов пока нет. Все переходы выполняет человек или исполнитель в рамках явного поручения.
