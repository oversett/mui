---
product: material-ui
title: React Divider component
components: Divider
githubLabel: 'component: divider'
materialDesign: https://m2.material.io/components/dividers
---

# Разделитель <meta data-oversett="" data-original-text="Divider">

<p class="description">Разделитель - это тонкая линия, которая группирует содержимое в списках и макетах.</p>

Разделители разделяют содержимое на четкие группы.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Разделители списков <meta data-oversett="" data-original-text="List dividers">

По умолчанию разделитель отображается как `<hr>`. Вы можете сохранить отображение этого DOM-элемента, используя параметр `divider` для компонента `ListItem`.

{{"demo": "ListDividers.js", "bg": true}}

## Спецификация HTML5 <meta data-oversett="" data-original-text="HTML5 specification">

В списке необходимо обеспечить отображение `Divider` в виде `<li>` в соответствии со спецификацией HTML5. В примерах ниже показаны два способа достижения этой цели.

## Вставные разделители <meta data-oversett="" data-original-text="Inset dividers">

{{"demo": "InsetDividers.js", "bg": true}}

## Подзаголовочные разделители <meta data-oversett="" data-original-text="Subheader dividers">

{{"demo": "SubheaderDividers.js", "bg": true}}

## Средний разделитель <meta data-oversett="" data-original-text="Middle divider">

{{"demo": "MiddleDividers.js", "bg": true}}

## Разделители с текстом <meta data-oversett="" data-original-text="Dividers with text">

Вы также можете отобразить разделитель с содержимым.

{{"demo": "DividerText.js"}}

:::warning
При использовании компонента `Divider` для визуального оформления, например, в заголовке, явно укажите `role="presentation"` для разделителя, чтобы гарантировать, что программы чтения с экрана смогут объявить его содержимое:

```js
<Divider component="div" role="presentation">
  {/* any elements nested inside the role="presentation" preserve their semantics. */}
  <Typography variant="h2">My Heading</Typography>
</Divider>
```
:::

## Вертикальный разделитель <meta data-oversett="" data-original-text="Vertical divider">

Вы также можете отобразить разделитель вертикально, используя компонент `orientation`.

{{"demo": "VerticalDividers.js", "bg": true}}

:::info
Обратите внимание на использование реквизита `flexItem` для учета гибкого контейнера.
:::

### Вертикальный с вариантом середины <meta data-oversett="" data-original-text="Vertical with variant middle">

Вы также можете отобразить вертикальный разделитель с помощью `variant="middle"`.

{{"demo": "VerticalDividerMiddle.js", "bg": true}}

### Вертикальный с текстом <meta data-oversett="" data-original-text="Vertical with text">

Вы также можете отобразить вертикальный разделитель с помощью содержимого.

{{"demo": "VerticalDividerText.js"}}
