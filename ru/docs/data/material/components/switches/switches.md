---
product: material-ui
title: React Switch component
components: Switch, FormControl, FormGroup, FormLabel, FormControlLabel
githubLabel: 'component: switch'
materialDesign: https://m2.material.io/components/selection-controls#switches
unstyled: /base/react-switch/
---

# Переключатель <meta data-oversett="" data-original-text="Switch">

<p class="description">Переключатели включают или выключают состояние одного параметра.</p>

Переключатели являются предпочтительным способом настройки параметров на мобильных устройствах. Параметр, которым управляет переключатель, а также состояние, в котором он находится, должны быть понятны из соответствующей встроенной метки.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основные переключатели <meta data-oversett="" data-original-text="Basic switches">

{{"demo": "BasicSwitches.js"}}

## Метка <meta data-oversett="" data-original-text="Label">

Благодаря компоненту `FormControlLabel` вы можете предоставить метку для `Switch`.

{{"demo": "SwitchLabels.js"}}

## Размер <meta data-oversett="" data-original-text="Size">

Используйте компонент `size` для изменения размера переключателя.

{{"demo": "SwitchesSize.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "ColorSwitches.js"}}

## Управляемый <meta data-oversett="" data-original-text="Controlled">

Вы можете управлять переключателем с помощью реквизитов `checked` и `onChange`:

{{"demo": "ControlledSwitches.js"}}

## Переключатели с FormGroup <meta data-oversett="" data-original-text="Switches with FormGroup">

`FormGroup` это полезная обертка, используемая для группировки компонентов элементов управления выбором, которая обеспечивает более простой API. Однако, если требуется несколько связанных элементов управления, рекомендуется использовать вместо них [флажки](/material-ui/react-checkbox/). (См.: [Когда использовать](#when-to-use)).

{{"demo": "SwitchesGroup.js"}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Подробнее об этом вы можете узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSwitches.js"}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/switch/).

## Размещение ярлыка <meta data-oversett="" data-original-text="Label placement">

Вы можете изменить размещение ярлыка:

{{"demo": "FormControlLabelPosition.js"}}

## Когда использовать <meta data-oversett="" data-original-text="When to use">

-   [Флажки против переключателей](https://uxplanet.org/checkbox-vs-toggle-switch-7fc6e83f10b8)

## Доступность <meta data-oversett="" data-original-text="Accessibility">

-   Элемент будет отображаться с ролью `checkbox`, а не `switch`, поскольку эта роль еще не получила широкой поддержки. Пожалуйста, сначала проверьте, поддерживают ли вспомогательные технологии вашей целевой аудитории эту роль должным образом. Затем вы можете изменить роль с помощью`<Switch inputProps={{ role: 'switch' }}>`
-   Все элементы управления формы должны иметь метки, включая радиокнопки, флажки и переключатели. В большинстве случаев для этого используется элемент `<label>` [(FormControlLabel](/material-ui/api/form-control-label/)).
-   Когда метка не может быть использована, необходимо добавить атрибут непосредственно к компоненту ввода. В этом случае вы можете применить дополнительный атрибут (например, `aria-label`, `aria-labelledby`, `title`) через реквизит `inputProps`.

```jsx
<Switch value="checkedA" inputProps={{ 'aria-label': 'Switch A' }} />
```
