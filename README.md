# Figma Composer

`Figma Composer` превращает UI-референсы в Figma в структурированные и редактируемые экраны.

## Как подготовить файл

1. Поместите каждый UI-референс отдельным изображением внутрь собственного Figma Frame.

2. Настройте размер, скругления, Corner smoothing и clipping внешнего Frame — эти свойства будут сохранены в итоговом экране. Названия Frame и слоя изображения могут быть любыми.

3. Для нескольких экранов используйте отдельный Frame для каждого референса. Для максимальной точности рекомендуется обрабатывать один сложный референс за запуск.

4. При необходимости добавьте любые фотографии в `figma-compozer/assets/`. Навык распределит разные изображения по медиаконтейнерам без подбора по смыслу.

5. Передайте Codex ссылку на Figma-файл, нужный node или выделенную область. Не добавляйте в область обработки посторонние изображения, которые не являются UI-референсами.

Запустите навык:

```text
Используй $figma-compozer для этой Figma-ссылки: <ссылка>
```

## Что будет на выходе

Для каждого референса навык создаст рядом отдельный редактируемый экран `Screen 01`, `Screen 02` и далее. Исходные референсы и посторонние слои останутся без изменений.

Итоговый экран повторит размеры и геометрию исходного Frame. Интерфейс будет собран из нативных слоёв Figma и Auto Layout с редактируемыми текстами, подобранными шрифтами, векторными иконками, изображениями из `assets/`, градиентами, прозрачностью, обводками, тенями и blur-эффектами.

Референсы обрабатываются последовательно: навык полностью собирает и проверяет один экран, исправляет визуальные расхождения и только затем переходит к следующему.


## Material analysis and reference handoff

Complex surfaces are reconstructed as layered materials: backgrounds, fills, gradients, translucency, blur, borders, highlights and shadows. Ambiguous constructions are compared in context and assumptions are recorded.

Each reference produces a local `reference-packs/<reference-id>/` package:

- `reference.md`: a readable handoff for another agent.
- `reference.json`: structure, tokens, material recipes, components, composition, behavior, tags and quality.
- `art-direction.md`: defining visual principles and acceptance criteria.
- `art-review.md`: evidence, findings, correction history and verdict.

## Art director review

The art director inspects actual screenshots against the original reference and provides concrete corrections. A separate reviewer agent is used when available; otherwise the report explicitly identifies self-review. Up to three correction cycles are performed per reference. Any remaining issues are recorded before proceeding; unavailable visual evidence results in an `unverified` verdict rather than approval. This bounded review qualifies the sequential completion workflow above.

## Optional code twin

Ask for a code twin to generate a version from the same reference model using the current project stack, or standalone HTML/CSS in an empty workspace. The browser render is checked independently against the original reference.

```text
Use $figma-compozer for this Figma link: <link>.
Save the reference description and also create a code twin.
```
