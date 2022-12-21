---
product: material-ui
title: React Badge component
components: Badge
githubLabel: 'component: badge'
unstyled: /base/react-badge/
---

# Значок <meta data-oversett="" data-original-text="Badge">

<p class="description">Значок генерирует небольшой значок в правом верхнем углу своего ребенка (детей).</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основной бейдж <meta data-oversett="" data-original-text="Basic badge">

Примеры бейджей, содержащих текст, с использованием основных и дополнительных цветов. Значок применяется к своим дочерним элементам.

{{"demo": "SimpleBadge.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

Используйте свойство `color`, чтобы применить палитру тем к компоненту.

{{"demo": "ColorBadge.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedBadges.js"}}

## Видимость бейджей <meta data-oversett="" data-original-text="Badge visibility">

Видимость бейджей можно контролировать с помощью свойства `invisible`.

{{"demo": "BadgeVisibility.js"}}

Бейдж автоматически скрывается, когда `badgeContent` равен нулю. Вы можете переопределить этот параметр с помощью свойства `showZero`.

{{"demo": "ShowZeroBadge.js"}}

## Максимальное значение <meta data-oversett="" data-original-text="Maximum value">

С помощью реквизита `max` можно ограничить значение содержимого бейджа.

{{"demo": "BadgeMax.js"}}

## Точечный значок <meta data-oversett="" data-original-text="Dot badge">

Реквизит `dot` меняет значок на маленькую точку. Это можно использовать в качестве уведомления о том, что что-то изменилось, без указания количества.

{{"demo": "DotBadge.js"}}

## Наложение значков <meta data-oversett="" data-original-text="Badge overlap">

Реквизит `overlap` можно использовать для размещения бейджа относительно угла обернутого элемента.

{{"demo": "BadgeOverlap.js"}}

## Выравнивание значка <meta data-oversett="" data-original-text="Badge alignment">

С помощью свойства `anchorOrigin` можно переместить значок в любой угол обернутого элемента.

{{"demo": "BadgeAlignment.js", "hideToolbar": true}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Вы не можете полагаться на то, что содержимое бейджа будет объявлено правильно. Вы должны предоставить полное описание, например, с помощью `aria-label`:

{{"demo": "AccessibleBadges.js"}}
