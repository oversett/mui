---
product: material-ui
title: React Masonry component
components: Masonry
githubLabel: 'component: masonry'
---

# Masonry <meta data-oversett="" data-original-text="Masonry">

<p class="description">Masonry выстраивает содержимое разных размеров в виде блоков одинаковой ширины и разной высоты с настраиваемыми промежутками.</p>

Masonry поддерживает список блоков содержимого с одинаковой шириной и разной высотой. Содержимое упорядочивается по рядам. Если ряд уже заполнен указанным количеством столбцов, то следующий элемент начинает другой ряд, и он добавляется в самый короткий столбец, чтобы оптимизировать использование пространства.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Базовая кладка <meta data-oversett="" data-original-text="Basic masonry">

Простой пример `Masonry`. `Masonry` - это контейнер для одного или нескольких элементов. Он может принимать любой элемент, включая `<div />` и `<img />`.

{{"demo": "BasicMasonry.js", "bg": true}}

## Кладка изображений <meta data-oversett="" data-original-text="Image masonry">

Этот пример демонстрирует использование `Masonry` для изображений. `Masonry` упорядочивает свои дочерние элементы по строкам. Если вы хотите упорядочить изображения по столбцам, ознакомьтесь с [ImageList](/material-ui/react-image-list/#masonry-image-list).

{{"demo": "ImageMasonry.js", "bg": true}}

## Элементы с переменной высотой <meta data-oversett="" data-original-text="Items with variable height">

Этот пример демонстрирует использование `Masonry` для элементов с переменной высотой. Элементы могут перемещаться в другие колонки, чтобы соблюсти правило, согласно которому элементы всегда добавляются в самую короткую колонку, и, следовательно, оптимизировать использование пространства.

{{"demo": "MasonryWithVariableHeightItems.js", "bg": true}}

## Колонки <meta data-oversett="" data-original-text="Columns">

Этот пример демонстрирует использование `columns` для настройки количества колонок `Masonry`.

{{"demo": "FixedColumns.js", "bg": true}}

`columns` принимает значения, соответствующие требованиям:

{{"demo": "ResponsiveColumns.js", "bg": true}}

## Spacing <meta data-oversett="" data-original-text="Spacing">

Этот пример демонстрирует использование `spacing` для настройки расстояния между элементами. Важно отметить, что значение, передаваемое реквизиту `spacing`, умножается на поле spacing темы.

{{"demo": "FixedSpacing.js", "bg": true}}

`spacing` принимает значения responsive:

{{"demo": "ResponsiveSpacing.js", "bg": true}}

## Рендеринг на стороне сервера <meta data-oversett="" data-original-text="Server-side rendering">

Этот пример демонстрирует использование `defaultHeight`, `defaultColumns` и `defaultSpacing`, которые используются для поддержки рендеринга на стороне сервера.

:::info
`defaultHeight` должно быть достаточно большим, чтобы отобразить все строки. Также стоит отметить, что при серверном рендеринге элементы не добавляются в самый короткий столбец.
:::

{{"demo": "SSRMasonry.js", "bg": true}}
