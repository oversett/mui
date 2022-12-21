---
product: material-ui
title: React Accordion component
components: Accordion, AccordionActions, AccordionDetails, AccordionSummary
githubLabel: 'component: accordion'
materialDesign: https://m1.material.io/components/expansion-panels.html
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/accordion/
---

# Аккордеон <meta data-oversett="" data-original-text="Accordion">

<p class="description">Компонент аккордеона позволяет пользователю показывать и скрывать разделы связанного контента на странице.</p>

Аккордеон - это легкий контейнер, который может использоваться как отдельно, так и быть соединенным с более крупной поверхностью, например, картой.

{{"component": "modules/components/ComponentLinkHeader.js"}}

:::info
Аккордеоны больше не документированы в [руководстве по Material Design](https://m2.material.io/), но MUI будет продолжать их поддерживать. Ранее они были известны как "панель расширения".
:::

## Базовый аккордеон <meta data-oversett="" data-original-text="Basic accordion">

{{"demo": "BasicAccordion.js", "bg": true}}

## Управляемый аккордеон <meta data-oversett="" data-original-text="Controlled accordion">

Расширьте поведение по умолчанию, чтобы создать аккордеон с помощью компонента `Accordion`.

{{"demo": "ControlledAccordions.js", "bg": true}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedAccordions.js"}}

## Производительность <meta data-oversett="" data-original-text="Performance">

Содержимое аккордеонов монтируется по умолчанию, даже если аккордеон не развернут. Это поведение по умолчанию имеет в виду рендеринг на стороне сервера и SEO. Если вы рендерите дорогие деревья компонентов внутри деталей вашего аккордеона или просто рендерите много аккордеонов, может быть хорошей идеей изменить это поведение по умолчанию, включив`unmountOnExit` в `TransitionProps`:

```jsx
<Accordion TransitionProps={{ unmountOnExit: true }} />
```

Как и любая оптимизация производительности, это не серебряная пуля. Убедитесь, что вы сначала определили узкие места, а затем попробуйте эти стратегии оптимизации.

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/accordion/)](https://www.w3.org/WAI/ARIA/apg/patterns/accordion/)

Для оптимальной доступности мы рекомендуем установить `id` и `aria-controls` на`AccordionSummary`. Из `Accordion` будут получены необходимые `aria-labelledby`и `id` для области содержимого аккордеона.
