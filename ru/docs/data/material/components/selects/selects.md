---
product: material-ui
title: React Select component
components: Select, NativeSelect
githubLabel: 'component: select'
materialDesign: https://m2.material.io/components/menus#exposed-dropdown-menu
waiAria: https://www.w3.org/WAI/ARIA/apg/example-index/combobox/combobox-select-only.html
unstyled: /base/react-select/
---

# Select <meta data-oversett="" data-original-text="Select">

<p class="description">Компоненты Select используются для сбора информации, предоставленной пользователем, из списка вариантов.</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовый выбор <meta data-oversett="" data-original-text="Basic select">

Меню располагаются под своими излучающими элементами, если они не находятся близко к нижней части области просмотра.

{{"demo": "BasicSelect.js"}}

## Расширенные возможности <meta data-oversett="" data-original-text="Advanced features">

Компонент Select предназначен для взаимозаменяемости с собственным элементом `<select>`.

Если вам нужны более продвинутые функции, такие как combobox, multiselect, autocomplete, async или creatable, перейдите к [компоненту`Autocomplete`](/material-ui/react-autocomplete/) . Он представляет собой улучшенную версию пакетов "react-select" и "downshift".

## Реквизиты <meta data-oversett="" data-original-text="Props">

Компонент Select реализован как пользовательский `<input>` элемент [InputBase](/material-ui/api/input-base/). Он расширяет подкомпоненты [компонентов текстового поля](/material-ui/react-text-field/), либо [OutlinedInput](/material-ui/api/outlined-input/), [Input](/material-ui/api/input/), либо [FilledInput](/material-ui/api/filled-input/), в зависимости от выбранного варианта. Он использует те же стили и многие из тех же реквизитов. Подробности см. на странице API соответствующего компонента.

### Заполненный и стандартный варианты <meta data-oversett="" data-original-text="Filled and standard variants">

{{"demo": "SelectVariants.js"}}

### Ярлыки и вспомогательный текст <meta data-oversett="" data-original-text="Labels and helper text">

{{"demo": "SelectLabels.js"}}

:::warning
Обратите внимание, что при использовании FormControl с очерченным вариантом Select необходимо указать метку в двух местах: в компоненте InputLabel и в реквизите `label` компонента Select (см. демонстрацию выше).
:::

### Автоматическая ширина <meta data-oversett="" data-original-text="Auto width">

{{"demo": "SelectAutoWidth.js"}}

### Малый размер <meta data-oversett="" data-original-text="Small Size">

{{"demo": "SelectSmall.js"}}

### Другие реквизиты <meta data-oversett="" data-original-text="Other props">

{{"demo": "SelectOtherProps.js"}}

## Родной select <meta data-oversett="" data-original-text="Native select">

Поскольку пользовательский опыт может быть улучшен на мобильных устройствах с помощью нативного селекта платформы, мы разрешаем такой шаблон.

{{"demo": "NativeSelect.js"}}

## TextField <meta data-oversett="" data-original-text="TextField">

Компонент-обертка `TextField` представляет собой полноценный элемент управления формой, включающий метку, ввод и текст подсказки. Пример с режимом select вы можете найти [в этом разделе](/material-ui/react-text-field/#select).

## Персонализация <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Более подробно об этом можно узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

Первым шагом является стилизация компонента `InputBase`. После стилизации вы можете либо использовать его непосредственно как текстовое поле, либо предоставить его реквизиту select `input`, чтобы получить поле `select`. Обратите внимание, что вариант `"standard"` легче настраивается, поскольку он не оборачивает содержимое в разметку `fieldset`/`legend`.

{{"demo": "CustomizedSelects.js"}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/select/).

## Множественный выбор <meta data-oversett="" data-original-text="Multiple select">

Компонент `Select` может работать с множественным выбором. Это включается с помощью реквизита `multiple`.

Как и при одиночном выборе, вы можете извлечь новое значение, обратившись к `event.target.value` в обратном вызове `onChange`. Это всегда массив.

### По умолчанию <meta data-oversett="" data-original-text="Default">

{{"demo": "MultipleSelect.js"}}

### Галочки <meta data-oversett="" data-original-text="Checkmarks">

{{"demo": "MultipleSelectCheckmarks.js"}}

### Фишка <meta data-oversett="" data-original-text="Chip">

{{"demo": "MultipleSelectChip.js"}}

### Местодержатель <meta data-oversett="" data-original-text="Placeholder">

{{"demo": "MultipleSelectPlaceholder.js"}}

### Родной <meta data-oversett="" data-original-text="Native">

{{"demo": "MultipleSelectNative.js"}}

## Управление открытым состоянием <meta data-oversett="" data-original-text="Controlling the open state">

Вы можете управлять открытым состоянием селекта с помощью реквизита `open`. Также можно установить начальное (неконтролируемое) открытое состояние компонента с помощью реквизита `defaultOpen`.

{{"demo": "ControlledOpenSelect.js"}}

## С помощью диалога <meta data-oversett="" data-original-text="With a dialog">

Несмотря на то, что руководство по Material Design не рекомендует это делать, вы можете использовать селект внутри диалога.

{{"demo": "DialogSelect.js"}}

## Группировка <meta data-oversett="" data-original-text="Grouping">

Отображайте категории с помощью компонента `ListSubheader` или собственного элемента `<optgroup>`.

{{"demo": "GroupedSelect.js"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Для правильной маркировки ввода `Select` необходим дополнительный элемент с `id`, содержащим метку. Этот `id` должен соответствовать `labelId` элемента `Select`, например.

```jsx
<InputLabel id="label">Age</InputLabel>
<Select labelId="label" id="select" value="20">
  <MenuItem value="10">Ten</MenuItem>
  <MenuItem value="20">Twenty</MenuItem>
</Select>
```

Альтернативный вариант - `TextField` с `id` и `label`, создающий правильную разметку и идентификаторы:

```jsx
<TextField id="select" label="Age" value="20" select>
  <MenuItem value="10">Ten</MenuItem>
  <MenuItem value="20">Twenty</MenuItem>
</TextField>
```

Для [собственного select](#native-select) вы должны упомянуть метку, передав значение атрибута `id` элемента select атрибуту `InputLabel`'s `htmlFor`:

```jsx
<InputLabel htmlFor="select">Age</InputLabel>
<NativeSelect id="select">
  <option value="10">Ten</option>
  <option value="20">Twenty</option>
</NativeSelect>
```
