---
product: material-ui
title: React Checkbox component
components: Checkbox, FormControl, FormGroup, FormLabel, FormControlLabel
materialDesign: https://m2.material.io/components/selection-controls#checkboxes
githubLabel: 'component: checkbox'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/
---

# Флажок <meta data-oversett="" data-original-text="Checkbox">

<p class="description">Флажки позволяют пользователю выбрать один или несколько элементов из набора.</p>

Флажки можно использовать для включения или выключения опции.

Если в списке отображается несколько опций, вы можете сэкономить место, используя флажки вместо переключателей вкл/выкл. Если у вас одна опция, избегайте флажков и используйте вместо них переключатели вкл/выкл.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основные флажки <meta data-oversett="" data-original-text="Basic checkboxes">

{{"demo": "Checkboxes.js"}}

## Ярлык <meta data-oversett="" data-original-text="Label">

Благодаря компоненту `FormControlLabel` вы можете предоставить метку для `Checkbox`.

{{"demo": "CheckboxLabels.js"}}

## Размер <meta data-oversett="" data-original-text="Size">

Используйте компонент `size` или настройте размер шрифта иконок svg, чтобы изменить размер флажков.

{{"demo": "SizeCheckboxes.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "ColorCheckboxes.js"}}

## Иконка <meta data-oversett="" data-original-text="Icon">

{{"demo": "IconCheckboxes.js"}}

## Управляемый <meta data-oversett="" data-original-text="Controlled">

Вы можете управлять флажком с помощью реквизитов `checked` и `onChange`:

{{"demo": "ControlledCheckbox.js"}}

## Неопределенный <meta data-oversett="" data-original-text="Indeterminate">

Ввод флажка может иметь только два состояния в форме: отмечен или не отмечен. Он либо отправляет свое значение, либо нет. Визуально флажок может находиться в **трех** состояниях: отмечен, не отмечен или неопределенный.

{{"demo": "IndeterminateCheckbox.js"}}

:::warning
Когда установлено значение indeterminate, значение реквизита `checked` влияет только на отправленные значения формы. Это не влияет на доступность или UX.
:::

## FormGroup <meta data-oversett="" data-original-text="FormGroup">

`FormGroup` это полезная обертка, используемая для группировки компонентов элемента управления выбором.

{{"demo": "CheckboxesGroup.js"}}

## Размещение ярлыка <meta data-oversett="" data-original-text="Label placement">

Вы можете изменить расположение метки:

{{"demo": "FormControlLabelPosition.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedCheckbox.js"}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/checkbox/).

## Когда использовать <meta data-oversett="" data-original-text="When to use">

-   [Флажки против радиокнопок](https://www.nngroup.com/articles/checkboxes-vs-radio-buttons/)
-   [Флажки против переключателей](https://uxplanet.org/checkbox-vs-toggle-switch-7fc6e83f10b8)

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/)](https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/)

-   Все элементы управления формы должны иметь метки, это касается и радиокнопок, и флажков, и переключателей. В большинстве случаев для этого используется элемент `<label>` [(FormControlLabel](/material-ui/api/form-control-label/)).
-   Когда метка не может быть использована, необходимо добавить атрибут непосредственно к компоненту ввода. В этом случае вы можете применить дополнительный атрибут (например, `aria-label`, `aria-labelledby`, `title`) через реквизит `inputProps`.

```jsx
<Checkbox
  value="checkedA"
  inputProps={{
    'aria-label': 'Checkbox A',
  }}
/>
```
