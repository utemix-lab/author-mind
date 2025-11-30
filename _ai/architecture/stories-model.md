---
id: stories-model
type: architecture
scope: stories
status: active
---

# Stories Model — архитектура двухголосных эпизодов

Этот документ описывает формальный механизм работы со Stories  
в репозитории `author-mind` и связанных технических репозиториях (например, `vovaipetrova-core`).

Stories — это двухголосный дневник проекта:

- **Author-line** — авторская, эмоциональная, образная часть эпизода.
- **Machine-line** — сухой, структурированный отчёт по истории проекта (обычно по GitHub).

---

## 1. Назначение Stories

Stories нужны для:

- фиксации истории проекта в человекочитаемой форме  
- соединения художественной и технической линий  
- создания материала для будущих текстов, визуала и видео  
- демонстрации совместной работы человека и машины  

Каждый эпизод Stories — это единица времени / состояния / смысла.

---

## 2. Файловая структура

**В репозитории `author-mind`:**

stories/
story-001-something.md
story-002-...md
_ai/index-stories.md

arduino
Копировать код

**В техническом репо (например, `vovaipetrova-core`):**

```text
story/
  episodes/          ← machine-line
    machine-episode-001.md
    machine-episode-002.md
  combined/          ← author-line + machine-line
    combined-001.md
    combined-002.md
3. Формат файла story-XXX в author-mind
Расположение:

bash
Копировать код
stories/story-XYZ-title.md
Рекомендуемый фронтматтер:

markdown
Копировать код
---
id: story-XYZ
type: story
title: "Название эпизода"
related_lines: []        # например: [line-000-metathoughts, line-001-origin]
related_themes: []       # например: [duality, evolution]
project: vovaipetrova    # или другой проект
story_number: XYZ
status: draft
---
Структура содержимого:

markdown
Копировать код
# story-XYZ — Название эпизода

## Author-line
(Художественный, эмоциональный, образный текст.  
Может быть абстрактным, философским, с ассоциациями.)

## Machine-line (link / placeholder)
(Ссылка или описание того, какой machine-episode соответствует этому эпизоду.  
Сам текст machine-line хранится в техническом репозитории.)

## Notes for LLM
- Смысловые связи
- Контекст для последующих эпизодов
- Указания, как использовать этот эпизод при генерации
4. Формат machine-line в техническом репо
Расположение:

bash
Копировать код
story/episodes/machine-episode-XYZ.md
Содержание:

дата / диапазон времени

список коммитов / PR / задач

краткое текстовое саммари изменений

структурированное описание прогресса

Формат может быть адаптирован под CI/бота, но концепция:

строгий

фактологичный

опирается на Git, задачи, метрики

5. Формат combined-эпизода
Расположение:

bash
Копировать код
story/combined/combined-XYZ.md
Структура:

markdown
Копировать код
# Episode XYZ — Название

## Author-line
(подтягивается из author-mind/stories/story-XYZ.md)

## Machine-line
(подтягивается из story/episodes/machine-episode-XYZ.md)

## Meta
(опционально: тема, линии, ссылки)
6. Жизненный цикл эпизода
Возникает событие/состояние в проекте.

Техрепо фиксирует изменения → создаётся или обновляется machine-episode-XYZ.

В author-mind создаётся stories/story-XYZ.md — пишется Author-line.

В техрепо формируется combined-XYZ.md, в котором два голоса сведены вместе.

Для будущих аналитик и творчества используются:

author-line → как художественный материал

machine-line → как фактологический источник

7. Связи Stories
Stories должны быть связаны:

с линиями (lines/) через поле related_lines

с темами (themes/) через related_themes

с проектами (projects/) через project

иногда — с worlds/, aesthetics/, emotions/ (через ссылки в Notes)

8. Требования к качеству Stories
каждый story-эпизод должен быть самодостаточным

Author-line не обязан объяснять всё — может быть фрагментарным

Machine-line должен быть однозначным и точным

номер эпизода (XYZ) должен совпадать между всеми тремя версиями:

story-XYZ

machine-episode-XYZ

combined-XYZ

9. Назначение этого документа
Этот документ служит:

спецификацией двухголосной структуры Stories

инструкцией для LLM и агентов

основой для автоматизации сборки combined-эпизодов

каркасом для “журнала проекта” как продукта

Конец stories-model.md
