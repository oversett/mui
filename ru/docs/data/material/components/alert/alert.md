---
product: material-ui
title: React Alert component
components: Alert, AlertTitle
githubLabel: 'component: alert'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/alert/
---

# Оповещение <meta data-oversett="" data-original-text="Alert">

<p class="description">Оповещение отображает короткое, важное сообщение таким образом, чтобы привлечь внимание пользователя, не прерывая его задачу.</p>

**Примечание:** Этот компонент не документирован в [руководстве по Material Design](https://m2.material.io/), но MUI поддерживает его.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основные оповещения <meta data-oversett="" data-original-text="Basic alerts">

Оповещение предлагает четыре уровня серьезности, для которых устанавливается отличительный значок и цвет.

{{"demo": "BasicAlerts.js"}}

## Описание <meta data-oversett="" data-original-text="Description">

Вы можете использовать компонент `AlertTitle` для отображения форматированного заголовка над содержимым.

{{"demo": "DescriptionAlerts.js"}}

## Действия <meta data-oversett="" data-original-text="Actions">

Оповещение может иметь действие, например, кнопку закрытия или отмены. Оно отображается после сообщения, в конце оповещения.

Если указан обратный вызов `onClose` и не задано свойство `action`, отображается значок закрытия. Реквизит `action` можно использовать для предоставления альтернативного действия, например, с помощью кнопки Button или IconButton.

{{"demo": "ActionAlerts.js"}}

### Переход <meta data-oversett="" data-original-text="Transition">

Вы можете использовать [компонент перехода](/material-ui/transitions/), такой как `Collapse`, для изменения внешнего вида оповещения.

{{"demo": "TransitionAlerts.js"}}

## Иконки <meta data-oversett="" data-original-text="Icons">

Свойство `icon` позволяет добавить иконку в начало компонента оповещения. Это отменяет иконку по умолчанию для указанной степени тяжести.

С помощью свойства `iconMapping` можно изменить стандартное соответствие между степенью тяжести и иконкой. Его можно задать глобально с помощью [настройки темы](/material-ui/customization/theme-components/#default-props).

Установка свойства icon в `false` приведет к полному удалению иконки.

{{"demo": "IconAlerts.js"}}

## Варианты <meta data-oversett="" data-original-text="Variants">

Доступны два дополнительных варианта - очерченный и заполненный:

### Outlined <meta data-oversett="" data-original-text="Outlined">

{{"demo": "OutlinedAlerts.js"}}

При использовании очерченного оповещения с [компонентом`Snackbar`](/material-ui/react-snackbar/#customization) фоновое содержимое будет видно и по умолчанию будет просвечивать сквозь оповещение. Вы можете предотвратить это, добавив `bgcolor: 'background.paper'` к[параметру`sx`](/material-ui/customization/how-to-customize/#the-sx-prop) компонента `Alert`.

### Заполненный <meta data-oversett="" data-original-text="Filled">

{{"demo": "FilledAlerts.js"}}

## Тост <meta data-oversett="" data-original-text="Toast">

Вы можете использовать закусочную панель для [отображения тоста](/material-ui/react-snackbar/#customization) с оповещением.

## Цвет <meta data-oversett="" data-original-text="Color">

Свойство `color` переопределяет цвет по умолчанию для указанной степени тяжести.

{{"demo": "ColorAlerts.js"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/alert/)](https://www.w3.org/WAI/ARIA/apg/patterns/alert/)

Когда компонент динамически отображается, его содержимое автоматически объявляется большинством программ для чтения с экрана. В настоящее время программы чтения с экрана не информируют пользователей о предупреждениях, возникающих при загрузке страницы.

Использование цвета для придания смысла обеспечивает только визуальную индикацию, которая не будет передана пользователям вспомогательных технологий, таких как считыватели экрана. Убедитесь, что информация, обозначенная цветом, либо очевидна из самого содержимого (например, видимый текст), либо включена альтернативными средствами, например, дополнительным скрытым текстом.

Действия должны иметь индекс табуляции 0, чтобы к ним могли обращаться пользователи, использующие только клавиатуру.
