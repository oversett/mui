---
product: material-ui
title: Toggle Button React component
components: ToggleButton, ToggleButtonGroup
githubLabel: 'component: toggle button'
materialDesign: https://m2.material.io/components/buttons#toggle-button
---

# Кнопка переключения <meta data-oversett="" data-original-text="Toggle Button">

<p class="description">Кнопка переключения может использоваться для группировки связанных опций.</p>

Чтобы выделить группы связанных кнопок Toggle, группа должна иметь общий контейнер. `ToggleButtonGroup` управляет выбранным состоянием своих дочерних кнопок, если ему присвоен собственный реквизит `value`.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Эксклюзивный выбор <meta data-oversett="" data-original-text="Exclusive selection">

При эксклюзивном выборе один параметр отменяет выбор любого другого.

В этом примере кнопки переключения обоснования текста представляют варианты для левого, центрального, правого и полностью обоснованного текста (отключено), причем для выбора одновременно доступен только один элемент.

**Примечание**: Исключительный выбор не требует, чтобы кнопка была активной. Об этом см. раздел " [Усилить набор значений](#enforce-value-set)".

{{"demo": "ToggleButtons.js"}}

## Множественный выбор <meta data-oversett="" data-original-text="Multiple selection">

Множественный выбор позволяет выбирать несколько вариантов логически сгруппированных опций, таких как полужирный, курсив и подчеркивание.

{{"demo": "ToggleButtonsMultiple.js"}}

## Размер <meta data-oversett="" data-original-text="Size">

Для создания кнопок большего или меньшего размера используйте параметр `size`.

{{"demo": "ToggleButtonSizes.js"}}

## Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "ColorToggleButton.js"}}

## Вертикальные кнопки <meta data-oversett="" data-original-text="Vertical buttons">

Кнопки можно укладывать вертикально, если для параметра `orientation` установить значение "вертикально".

{{"demo": "VerticalToggleButtons.js"}}

## Принудительный набор значений <meta data-oversett="" data-original-text="Enforce value set">

Если вы хотите, чтобы хотя бы одна кнопка была активна, вы можете адаптировать функцию handleChange.

```jsx
const handleAlignment = (event, newAlignment) => {
  if (newAlignment !== null) {
    setAlignment(newAlignment);
  }
};

const handleDevices = (event, newDevices) => {
  if (newDevices.length) {
    setDevices(newDevices);
  }
};
```

{{"demo": "ToggleButtonNotEmpty.js"}}

## Отдельная кнопка переключения <meta data-oversett="" data-original-text="Standalone toggle button">

{{"demo": "StandaloneToggleButton.js"}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedDividers.js", "bg": true}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

### ARIA <meta data-oversett="" data-original-text="ARIA">

-   ToggleButtonGroup имеет `role="group"`. Вы должны предоставить доступную метку с `aria-label="label"`, `aria-labelledby="id"` или `<label>`.
-   ToggleButton устанавливает `aria-pressed="<bool>"` в соответствии с состоянием кнопки. Для каждой кнопки следует использовать метку `aria-label`.

### Клавиатура <meta data-oversett="" data-original-text="Keyboard">

В настоящее время кнопки переключения расположены в порядке DOM. Переход между ними осуществляется с помощью клавиши табуляции. Поведение кнопки соответствует стандартной клавиатурной семантике.
