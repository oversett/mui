---
product: material-ui
title: React Stack component
components: Stack
githubLabel: 'component: Stack'
---

# Stack <meta data-oversett="" data-original-text="Stack">

<p class="description">Компонент Stack управляет расположением ближайших дочерних элементов вдоль вертикальной или горизонтальной оси с дополнительными интервалами и/или разделителями между каждым дочерним элементом.</p>

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Использование <meta data-oversett="" data-original-text="Usage">

`Stack` используется для одномерной компоновки, в то время как [Grid](/material-ui/react-grid/) работает с двухмерной компоновкой. По умолчанию используется направление `column`, при котором дочерние элементы укладываются вертикально.

{{"demo": "BasicStack.js", "bg": true}}

Чтобы управлять пространством между дочерними элементами, используйте реквизит `spacing`. Значение интервала может быть любым числом, включая десятичные дроби и любую строку. Реквизит преобразуется в свойство CSS с помощью параметра [`theme.spacing()`](/material-ui/customization/spacing/) помощника.

## Направление <meta data-oversett="" data-original-text="Direction">

По умолчанию `Stack` располагает элементы вертикально в `column`. Однако реквизит `direction` можно использовать и для горизонтального расположения элементов в `row`.

{{"demo": "DirectionStack.js", "bg": true}}

## Разделители <meta data-oversett="" data-original-text="Dividers">

Используйте свойство `divider` для вставки элемента между каждым дочерним элементом. Это особенно хорошо работает с компонентом [Divider](/material-ui/react-divider/).

{{"demo": "DividerStack.js", "bg": true}}

## Отзывчивые значения <meta data-oversett="" data-original-text="Responsive values">

Вы можете переключать значения `direction` или `spacing` в зависимости от активной точки останова.

{{"demo": "ResponsiveStack.js", "bg": true}}

## Интерактивный <meta data-oversett="" data-original-text="Interactive">

Ниже представлен интерактивный демонстрационный пример, позволяющий изучить визуальные результаты различных настроек:

{{"demo": "InteractiveStack.js", "hideToolbar": true, "bg": true}}

## Системные реквизиты <meta data-oversett="" data-original-text="System props">

Как компонент CSS утилиты, `Stack` поддерживает все [`system`](/system/properties/) свойства. Вы можете использовать их в качестве реквизитов непосредственно в компоненте. Например, margin-top:

```jsx
<Stack mt={2}>
```
