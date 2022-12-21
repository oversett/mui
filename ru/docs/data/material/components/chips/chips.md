---
product: material-ui
title: React Chip component
components: Chip
githubLabel: 'component: chip'
materialDesign: https://m2.material.io/components/chips
---

# Фишка <meta data-oversett="" data-original-text="Chip">

<p class="description">Фишки - это компактные элементы, которые представляют ввод, атрибут или действие.</p>

Фишки позволяют пользователям вводить информацию, делать выбор, фильтровать содержимое или запускать действия.

Несмотря на то, что фишки представлены здесь как самостоятельный компонент, наиболее часто они используются в той или иной форме ввода, поэтому некоторые из демонстрируемых здесь действий не показаны в контексте.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовая фишка <meta data-oversett="" data-original-text="Basic chip">

Компонент `Chip` поддерживает стилизацию с обводкой и заливкой.

{{"demo": "BasicChips.js"}}

## Действия фишки <meta data-oversett="" data-original-text="Chip actions">

Вы можете использовать следующие действия.

-   Фишки с определенным реквизитом `onClick` изменяют внешний вид при фокусе, наведении и нажатии.
-   Фишки с определенным реквизитом `onDelete` отображают иконку удаления, которая меняет вид при наведении.

### Кликабельный <meta data-oversett="" data-original-text="Clickable">

{{"demo": "ClickableChips.js"}}

### Удаляемый <meta data-oversett="" data-original-text="Deletable">

{{"demo": "DeletableChips.js"}}

### Кликабельный и удаляемый <meta data-oversett="" data-original-text="Clickable and deletable">

{{"demo": "ClickableAndDeletableChips.js"}}

### Щелкаемая ссылка <meta data-oversett="" data-original-text="Clickable link">

{{"demo": "ClickableLinkChips.js"}}

### Пользовательский значок удаления <meta data-oversett="" data-original-text="Custom delete icon">

{{"demo": "CustomDeleteIconChips.js"}}

## Украшения для фишек <meta data-oversett="" data-original-text="Chip adornments">

Вы можете добавить украшения в начало компонента.

Используйте реквизит `avatar` для добавления аватара или используйте реквизит `icon` для добавления иконки.

### Фишка аватара <meta data-oversett="" data-original-text="Avatar chip">

{{"demo": "AvatarChips.js"}}

### Фишка иконки <meta data-oversett="" data-original-text="Icon chip">

{{"demo": "IconChips.js"}}

## Фишка цвета <meta data-oversett="" data-original-text="Color chip">

Вы можете использовать реквизит `color` для определения цвета из палитры тем.

{{"demo": "ColorChips.js"}}

## Фишка размеров <meta data-oversett="" data-original-text="Sizes chip">

Вы можете использовать реквизит `size` для определения маленькой фишки.

{{"demo": "SizesChips.js"}}

## Массив фишек <meta data-oversett="" data-original-text="Chip array">

Пример рендеринга нескольких фишек из массива значений. Удаление фишки удаляет ее из массива. Обратите внимание, что поскольку реквизит`onClick` не определен, `Chip` может быть сфокусирован, но не набирает глубину при нажатии или касании.

{{"demo": "ChipsArray.js", "bg": true}}

## Игровая площадка фишек <meta data-oversett="" data-original-text="Chip playground">

{{"demo": "ChipsPlayground.js", "hideToolbar": true}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Если фишка удаляема или кликабельна, то она является кнопкой в порядке вкладок. Когда фишка сфокусирована (например, при переходе по вкладкам), отпускание (событие`keyup` ) `Backspace` или `Delete` вызовет обработчик `onDelete`, а отпускание `Escape` приведет к размытию фишки.
