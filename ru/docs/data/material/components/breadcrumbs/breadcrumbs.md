---
product: material-ui
title: React Breadcrumbs component
components: Breadcrumbs, Link, Typography
githubLabel: 'component: breadcrumbs'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/
---

# Хлебные крошки <meta data-oversett="" data-original-text="Breadcrumbs">

<p class="description">Хлебные крошки состоят из списка ссылок, которые помогают пользователю представить расположение страницы в иерархической структуре сайта и позволяют перейти к любому из ее "предков".</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основные хлебные крошки <meta data-oversett="" data-original-text="Basic breadcrumbs">

{{"demo": "BasicBreadcrumbs.js"}}

## Активная последняя хлебная крошка <meta data-oversett="" data-original-text="Active last breadcrumb">

Поддерживать последнюю хлебную крошку в интерактивном режиме.

{{"demo": "ActiveLastBreadcrumb.js"}}

## Пользовательский разделитель <meta data-oversett="" data-original-text="Custom separator">

В следующих примерах мы используем два строковых разделителя и SVG-иконку.

{{"demo": "CustomSeparator.js"}}

## Хлебные крошки с иконками <meta data-oversett="" data-original-text="Breadcrumbs with icons">

{{"demo": "IconBreadcrumbs.js"}}

## Свернутые хлебные крошки <meta data-oversett="" data-original-text="Collapsed breadcrumbs">

{{"demo": "CollapsedBreadcrumbs.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedBreadcrumbs.js"}}

## Интеграция с react-router <meta data-oversett="" data-original-text="Integration with react-router">

{{"demo": "RouterBreadcrumbs.js", "bg": true}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)

Обязательно добавьте описание `aria-label` на компонент `Breadcrumbs`.

Доступность этого компонента зависит от:

-   Набор ссылок структурирован с помощью упорядоченного списка (элемент`<ol>` ).
-   Чтобы экранное устройство чтения не объявляло визуальные разделители между ссылками, они скрыты с помощью `aria-hidden`.
-   Элемент nav, помеченный `aria-label`, идентифицирует структуру как хлебные крошки и делает ее навигационным ориентиром, чтобы ее было легко найти.
