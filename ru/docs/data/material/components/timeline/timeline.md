---
product: material-ui
title: React Timeline component
components: Timeline, TimelineItem, TimelineSeparator, TimelineDot, TimelineConnector, TimelineContent, TimelineOppositeContent
githubLabel: 'component: timeline'
packageName: '@mui/lab'
---

# Временная шкала <meta data-oversett="" data-original-text="Timeline">

<p class="description">Временная шкала отображает список событий в хронологическом порядке.</p>

**Примечание:** Этот компонент не документирован в [руководстве по Material Design](https://m2.material.io/), но MUI поддерживает его.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовая временная шкала <meta data-oversett="" data-original-text="Basic timeline">

Базовая временная шкала, отображающая список событий.

{{"demo": "BasicTimeline.js"}}

## Временная шкала с левым расположением <meta data-oversett="" data-original-text="Left-positioned timeline">

Основное содержимое временной шкалы может быть расположено слева относительно оси времени.

{{"demo": "LeftPositionedTimeline.js"}}

## Чередующаяся временная шкала <meta data-oversett="" data-original-text="Alternating timeline">

Временная шкала может отображать события поочередно.

{{"demo": "AlternateTimeline.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

Сайт `TimelineDot` может отображаться в различных цветах из палитры тем.

{{"demo": "ColorsTimeline.js"}}

## Очерченный <meta data-oversett="" data-original-text="Outlined">

{{"demo": "OutlinedTimeline.js"}}

## Противоположное содержание <meta data-oversett="" data-original-text="Opposite content">

Временная шкала может отображать содержимое на противоположных сторонах.

{{"demo": "OppositeContentTimeline.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTimeline.js"}}

## Выравнивание <meta data-oversett="" data-original-text="Alignment">

Существуют различные способы размещения временной шкалы в контейнере.

Это можно сделать, переопределив стили.

По умолчанию временная шкала центрируется в контейнере.

Демонстрации ниже показывают, как настроить относительную ширину левой и правой сторон временной шкалы:

### Выровненная по левому краю <meta data-oversett="" data-original-text="Left-aligned">

{{"demo": "LeftAlignedTimeline.js"}}

### Выровненная по правому краю <meta data-oversett="" data-original-text="Right-aligned">

{{"demo": "RightAlignedTimeline.js"}}

### Выровненная по левому краю без противоположного содержимого <meta data-oversett="" data-original-text="Left-aligned with no opposite content">

{{"demo": "NoOppositeContent.js"}}
