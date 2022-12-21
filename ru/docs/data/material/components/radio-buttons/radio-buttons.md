---
product: material-ui
title: React Radio Group component
components: Radio, RadioGroup, FormControl, FormLabel, FormControlLabel
githubLabel: 'component: radio'
materialDesign: https://m2.material.io/components/selection-controls#radio-buttons
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/radiobutton/
---

# Радиогруппа <meta data-oversett="" data-original-text="Radio Group">

<p class="description">Радиогруппа позволяет пользователю выбрать один вариант из множества.</p>

Используйте радиокнопки, когда пользователю необходимо видеть все доступные варианты. Если доступные варианты можно свернуть, используйте [компонент Select](/material-ui/react-select/), поскольку он занимает меньше места.

В радиокнопках по умолчанию должен быть выбран наиболее часто используемый вариант.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Группа радио <meta data-oversett="" data-original-text="Radio group">

`RadioGroup` это полезная обертка, используемая для группировки компонентов `Radio`, которая обеспечивает более простой API и надлежащую доступность группы с клавиатуры.

{{"demo": "RadioButtonsGroup.js"}}

### Направление <meta data-oversett="" data-original-text="Direction">

Чтобы расположить кнопки горизонтально, установите параметр `row`:

{{"demo": "RowRadioButtonsGroup.js"}}

### Controlled . <meta data-oversett="" data-original-text="Controlled">

Вы можете управлять радио с помощью реквизитов `value` и `onChange`:

{{"demo": "ControlledRadioButtonsGroup.js"}}

## Автономные радиокнопки <meta data-oversett="" data-original-text="Standalone radio buttons">

`Radio` также могут быть использованы отдельно, без обертки RadioGroup.

{{"demo": "RadioButtons.js"}}

## Размер <meta data-oversett="" data-original-text="Size">

Используйте реквизит `size` или настройте размер шрифта иконок svg, чтобы изменить размер радиокнопок.

{{"demo": "SizeRadioButtons.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "ColorRadioButtons.js"}}

## Размещение ярлыка <meta data-oversett="" data-original-text="Label placement">

Вы можете изменить размещение метки с помощью свойства `labelPlacement` компонента `FormControlLabel`:

{{"demo": "FormControlLabelPlacement.js"}}

## Show error <meta data-oversett="" data-original-text="Show error">

Как правило, радиокнопки должны иметь значение, выбранное по умолчанию. Если это не так, вы можете отобразить ошибку, если при отправке формы значение не выбрано:

{{"demo": "ErrorRadios.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedRadios.js"}}

## `useRadioGroup` <meta data-oversett="" data-original-text="useRadioGroup">

Для расширенной настройки используется хук `useRadioGroup()`. Он возвращает контекстное значение родительской группы радио. Компонент Radio использует этот хук внутри компонента.

### API <meta data-oversett="" data-original-text="API">

```jsx
import { useRadioGroup } from '@mui/material/RadioGroup';
```

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`value` _(объект_):

-   `value.name` _(строка_ \[необязательно\]): Имя, используемое для ссылки на значение элемента управления.
-   `value.onChange` _(func_ \[необязательно\]): Обратный вызов, выполняемый при выборе радиокнопки.
-   `value.value` _(any_ \[необязательно\]): Значение выбранной радиокнопки.

#### Пример <meta data-oversett="" data-original-text="Example">

{{"demo": "UseRadioGroup.js"}}

## Когда использовать <meta data-oversett="" data-original-text="When to use">

-   [Флажки против радиокнопок](https://www.nngroup.com/articles/checkboxes-vs-radio-buttons/)

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/radiobutton/)](https://www.w3.org/WAI/ARIA/apg/patterns/radiobutton/)

-   Все элементы управления формы должны иметь метки, и это относится к радиокнопкам, флажкам и переключателям. В большинстве случаев для этого используется элемент `<label>` [(FormControlLabel](/material-ui/api/form-control-label/)).
-   Когда метка не может быть использована, необходимо добавить атрибут непосредственно к компоненту ввода. В этом случае вы можете применить дополнительный атрибут (например, `aria-label`, `aria-labelledby`, `title`) через свойство `inputProps`.

```jsx
<Radio
  value="radioA"
  inputProps={{
    'aria-label': 'Radio A',
  }}
/>
```
