---
product: material-ui
title: React Button component
components: Button, IconButton, ButtonBase, LoadingButton
materialDesign: https://m2.material.io/components/buttons
githubLabel: 'component: button'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/button/
unstyled: /base/react-button/
---

# Кнопка <meta data-oversett="" data-original-text="Button">

<p class="description">Кнопки позволяют пользователям выполнять действия и делать выбор одним нажатием.</p>

Кнопки сообщают о действиях, которые могут предпринять пользователи. Они обычно размещаются в пользовательском интерфейсе в таких местах, как:

-   модальные окна
-   Формы
-   Карточки
-   Панели инструментов

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основная кнопка <meta data-oversett="" data-original-text="Basic button">

Кнопка `Button` имеет три варианта: текстовый (по умолчанию), содержащийся и очерченный.

{{"demo": "BasicButtons.js"}}

### Текстовая кнопка <meta data-oversett="" data-original-text="Text button">

[Текстовые кнопки](https://m2.material.io/components/buttons#text-button)обычно используются для менее выраженных действий, в том числе расположенных: в диалогах, в карточках. В карточках текстовые кнопки помогают сделать акцент на содержимом карточки.

{{"demo": "TextButtons.js"}}

### Содержательная кнопка <meta data-oversett="" data-original-text="Contained button">

[Содержательные кнопки](https://m2.material.io/components/buttons#contained-button)\- это кнопки с высоким акцентом, отличающиеся использованием возвышения и заливки. Они содержат действия, которые являются основными для вашего приложения.

{{"demo": "ContainedButtons.js"}}

Вы можете убрать возвышение с помощью реквизита `disableElevation`.

{{"demo": "DisableElevation.js"}}

### Выделенная кнопка <meta data-oversett="" data-original-text="Outlined button">

[Подчеркнутые кнопки](https://m2.material.io/components/buttons#outlined-button) - это кнопки со средним выделением. Они содержат действия, которые важны, но не являются основными в приложении.

Выделенные кнопки также являются альтернативой кнопкам с меньшим акцентом для содержащихся кнопок или альтернативой текстовым кнопкам с большим акцентом.

{{"demo": "OutlinedButtons.js"}}

## Обработка нажатий <meta data-oversett="" data-original-text="Handling clicks">

Все компоненты принимают обработчик `onClick`, который применяется к корневому элементу DOM.

```jsx
<Button
  onClick={() => {
    alert('clicked');
  }}
>
  Click me
</Button>
```

Обратите внимание, что документация [избегает](/material-ui/guides/api/#native-properties) упоминания нативных реквизитов (их очень много) в разделе API компонентов.

## Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "ColorButtons.js"}}

В дополнение к использованию цветов кнопок по умолчанию, вы можете добавить пользовательские цвета или отключить те, которые вам не нужны. Более подробную информацию смотрите в примере [добавления новых цветов](/material-ui/customization/palette/#adding-new-colors).

## Размеры <meta data-oversett="" data-original-text="Sizes">

Для создания кнопок большего или меньшего размера используйте реквизит `size`.

{{"demo": "ButtonSizes.js"}}

## Кнопка загрузки <meta data-oversett="" data-original-text="Upload button">

{{"demo": "UploadButtons.js"}}

## Кнопки с иконками и метками <meta data-oversett="" data-original-text="Buttons with icons and label">

Иногда для улучшения пользовательского интерфейса приложения вам могут понадобиться значки для определенных кнопок, поскольку мы легче распознаем логотипы, чем простой текст. Например, если у вас есть кнопка удаления, вы можете пометить ее значком мусорного ведра.

{{"demo": "IconLabelButtons.js"}}

## Кнопка с иконкой <meta data-oversett="" data-original-text="Icon button">

Кнопки-иконки обычно встречаются на панелях приложений и панелях инструментов.

Иконки также подходят для кнопок-переключателей, которые позволяют выбрать или отменить выбор одного варианта, например, добавить или убрать звезду у элемента.

{{"demo": "IconButtons.js"}}

### Размеры <meta data-oversett="" data-original-text="Sizes">

Для увеличения или уменьшения размера кнопок-значков используйте реквизит `size`.

{{"demo": "IconButtonSizes.js"}}

### Цвета <meta data-oversett="" data-original-text="Colors">

Используйте реквизит `color`, чтобы применить цветовую палитру темы к компоненту.

{{"demo": "IconButtonColors.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведены некоторые примеры настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedButtons.js", "defaultCodeOpen": false}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/button/).

## Кнопка загрузки <meta data-oversett="" data-original-text="Loading button">

Кнопки загрузки могут показывать состояние загрузки и отключать взаимодействие.

{{"demo": "LoadingButtons.js"}}

Переключите кнопку загрузки, чтобы увидеть переход между различными состояниями.

{{"demo": "LoadingButtonsTransition.js"}}

## Сложная кнопка <meta data-oversett="" data-original-text="Complex button">

Текстовые кнопки, содержащиеся кнопки, плавающие кнопки действий и кнопки с иконками построены на основе одного и того же компонента: `ButtonBase`. Вы можете использовать преимущества этого компонента нижнего уровня для создания пользовательских взаимодействий.

{{"demo": "ButtonBase.js"}}

## Сторонняя библиотека маршрутизации <meta data-oversett="" data-original-text="Third-party routing library">

Одним из частых случаев использования является выполнение навигации только на клиенте, без HTTP-трипа на сервер. Компонент `ButtonBase` предоставляет реквизит `component` для обработки этого случая использования. Здесь представлено [более подробное руководство](/material-ui/guides/routing/#button).

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### Курсор не разрешен <meta data-oversett="" data-original-text="Cursor not-allowed">

Компонент ButtonBase устанавливает `pointer-events: none;` на отключенные кнопки, что предотвращает появление отключенного курсора.

Если вы хотите использовать `not-allowed`, у вас есть два варианта:

1.  **Только CSS**. Вы можете удалить стиль pointer-events на отключенном состоянии элемента `<button>`:

```css
.MuiButtonBase-root:disabled {
  cursor: not-allowed;
  pointer-events: auto;
}
```

Однако:

-   Вы должны добавить `pointer-events: none;` обратно, когда вам нужно отображать [всплывающие подсказки на отключенных элементах](/material-ui/react-tooltip/#disabled-elements).
-   Курсор не изменится, если вы отобразите не элемент кнопки, а что-то другое, например, элемент ссылки `<a>`.

2.  **Изменение DOM**. Вы можете обернуть кнопку:

```jsx
<span style={{ cursor: 'not-allowed' }}>
  <Button component={Link} disabled>
    disabled
  </Button>
</span>
```

Преимуществом этого способа является поддержка любого элемента, например, элемента link `<a>`.

## Версия Material You <meta data-oversett="" data-original-text="Material You version">

Компонент Button по умолчанию соответствует спецификации Material Design 2. Для версии MD3[(Material You](https://m3.material.io/)) установите и импортируйте из экспериментального пакета `@mui/material-next`:

```js
import Button from '@mui/material-next/Button';
```

{{"demo": "ButtonMaterialYouPlayground.js", "hideToolbar": true}}
