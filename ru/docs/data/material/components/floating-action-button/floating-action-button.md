---
product: material-ui
title: React Floating Action Button (FAB) component
components: Fab
githubLabel: 'component: Fab'
materialDesign: https://m2.material.io/components/buttons-floating-action-button
---

# Плавающая кнопка действия <meta data-oversett="" data-original-text="Floating Action Button">

<p class="description">Плавающая кнопка действия (FAB) выполняет основное, или наиболее распространенное, действие на экране.</p>

Плавающая кнопка действия появляется перед всем содержимым экрана, обычно в виде круга с пиктограммой в центре. FAB бывают двух типов: обычные и расширенные.

Используйте FAB только в том случае, если это наиболее подходящий способ представления основного действия на экране. Для представления наиболее распространенного действия на экране рекомендуется использовать только один компонент.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовая ФАБ <meta data-oversett="" data-original-text="Basic FAB">

{{"demo": "FloatingActionButtons.js"}}

## Размер <meta data-oversett="" data-original-text="Size">

По умолчанию размер равен `large`. Для плавающих кнопок действий меньшего размера используйте реквизит `size`.

{{"demo": "FloatingActionButtonSize.js"}}

{{"demo": "FloatingActionButtonExtendedSize.js"}}

## Анимация <meta data-oversett="" data-original-text="Animation">

По умолчанию плавающая кнопка действия анимируется на экране в виде расширяющегося куска материала.

Плавающая кнопка действия, охватывающая несколько боковых экранов (например, экраны с вкладками), должна ненадолго исчезать, а затем появляться снова, если ее действие меняется.

Для этого можно использовать переход Zoom. Обратите внимание, что поскольку анимации выхода и входа запускаются одновременно, мы используем `enterDelay`, чтобы анимация выходящей плавающей кнопки действия успела завершиться до того, как появится новая.

{{"demo": "FloatingActionButtonZoom.js", "bg": true}}
