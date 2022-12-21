---
product: material-ui
title: React Paper component
components: Paper
githubLabel: 'component: Paper'
materialDesign: https://m2.material.io/design/environment/elevation.html
---

# Бумага <meta data-oversett="" data-original-text="Paper">

<p class="description">В Material Design физические свойства бумаги перенесены на экран.</p>

Фон приложения напоминает плоскую, непрозрачную текстуру листа бумаги, а поведение приложения имитирует способность бумаги изменять размер, перемешивать и скреплять несколько листов.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основная бумага <meta data-oversett="" data-original-text="Basic paper">

{{"demo": "SimplePaper.js", "bg": true}}

## Варианты <meta data-oversett="" data-original-text="Variants">

Если вам нужна очерченная поверхность, используйте реквизит `variant`.

{{"demo": "Variants.js", "bg": "inline"}}

## Возвышение <meta data-oversett="" data-original-text="Elevation">

Возвышение можно использовать для установления иерархии между другим содержимым. С практической точки зрения, возвышение управляет размером тени, накладываемой на поверхность. В темном режиме повышение высоты также делает поверхность светлее.

{{"demo": "Elevation.js", "bg": "inline"}}

Изменение тени в темном режиме происходит путем применения полупрозрачного градиента к свойству `background-image`. Это может привести к путанице при переопределении стилей `Paper`, поскольку установка только свойства `background-color` не повлияет на затенение, связанное с возвышением. Чтобы игнорировать затенение и установить цвет фона, на который не влияет возвышение в темном режиме, переопределите свойство `background` (или оба `background-color` и `background-image`).
