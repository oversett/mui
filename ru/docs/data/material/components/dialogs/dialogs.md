---
product: material-ui
title: React Dialog component
components: Dialog, DialogTitle, DialogContent, DialogContentText, DialogActions, Slide
githubLabel: 'component: dialog'
materialDesign: https://m2.material.io/components/dialogs
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/dialogmodal/
---

# Диалог <meta data-oversett="" data-original-text="Dialog">

<p class="description">Диалоги информируют пользователей о задаче и могут содержать важную информацию, требовать принятия решения или включать несколько задач.</p>

Диалог - это тип [модального](/material-ui/react-modal/) окна, которое появляется перед содержимым приложения для предоставления важной информации или запроса решения. Диалоги отключают все функции приложения, когда они появляются, и остаются на экране до тех пор, пока не будут подтверждены, отклонены или не будет выполнено необходимое действие.

Диалоговые окна намеренно прерывают работу приложения, поэтому их следует использовать редко.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовый диалог <meta data-oversett="" data-original-text="Basic dialog">

Простые диалоги могут предоставлять дополнительные сведения или действия относительно элемента списка. Например, они могут отображать аватары, иконки, уточняющий подтекст или ортогональные действия (такие как добавление аккаунта).

Механика касания:

-   Выбор опции немедленно фиксирует опцию и закрывает меню.
-   Касание за пределами диалога или нажатие кнопки Назад отменяет действие и закрывает диалог.

{{"demo": "SimpleDialog.js"}}

## Оповещения <meta data-oversett="" data-original-text="Alerts">

Оповещения - это срочные прерывания, требующие подтверждения, которые информируют пользователя о ситуации.

Большинство предупреждений не нуждаются в заголовках. Они кратко излагают решение в одном-двух предложениях, либо:

-   Задавая вопрос (например, "Удалить этот разговор?").
-   Делают заявление, связанное с кнопками действий.

Используйте предупреждения с заголовком только для ситуаций высокого риска, таких как потенциальная потеря связи. Пользователи должны быть в состоянии понять выбор, основываясь только на заголовке и тексте кнопки.

Если заголовок необходим:

-   Используйте четкий вопрос или утверждение с пояснением в области содержимого, например, "Стереть USB-накопитель?".
-   Избегайте извинений, двусмысленности или вопросов, таких как "Внимание!" или "Вы уверены?".

{{"demo": "AlertDialog.js"}}

## Переходы <meta data-oversett="" data-original-text="Transitions">

Вы также можете поменять местами переходы, в следующем примере используется `Slide`.

{{"demo": "AlertDialogSlide.js"}}

## Диалоговые окна формы <meta data-oversett="" data-original-text="Form dialogs">

Диалоговые формы позволяют пользователям заполнять поля формы внутри диалога. Например, если ваш сайт предлагает потенциальным подписчикам заполнить адрес электронной почты, они могут заполнить поле email и нажать кнопку "Отправить".

{{"demo": "FormDialog.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

В диалоговое окно добавлена кнопка закрытия для удобства использования.

{{"demo": "CustomizedDialogs.js"}}

## Полноэкранные диалоги <meta data-oversett="" data-original-text="Full-screen dialogs">

{{"demo": "FullScreenDialog.js"}}

## Дополнительные размеры <meta data-oversett="" data-original-text="Optional sizes">

Вы можете задать максимальную ширину диалога с помощью перечислимого параметра `maxWidth` в сочетании с булевым параметром `fullWidth`. Когда параметр `fullWidth` равен true, диалог будет адаптироваться на основе значения `maxWidth`.

{{"demo": "MaxWidthDialog.js"}}

## Отзывчивый полноэкранный <meta data-oversett="" data-original-text="Responsive full-screen">

Вы можете сделать диалог отзывчивым на весь экран, используя [`useMediaQuery`](/material-ui/react-use-media-query/).

```jsx
import useMediaQuery from '@mui/material/useMediaQuery';

function MyComponent() {
  const theme = useTheme();
  const fullScreen = useMediaQuery(theme.breakpoints.down('md'));

  return <Dialog fullScreen={fullScreen} />;
}
```

{{"demo": "ResponsiveDialog.js"}}

## Подтверждающие диалоги <meta data-oversett="" data-original-text="Confirmation dialogs">

Диалоговые окна подтверждения требуют от пользователя явного подтверждения своего выбора до того, как опция будет выполнена. Например, пользователь может прослушать несколько мелодий звонка, но сделать окончательный выбор только после нажатия кнопки "OK".

Нажатие кнопки "Отмена" в диалоге подтверждения или нажатие кнопки Назад отменяет действие, отменяет любые изменения и закрывает диалог.

{{"demo": "ConfirmationDialog.js"}}

## Перетаскиваемый диалог <meta data-oversett="" data-original-text="Draggable dialog">

С помощью [react-draggable](https://github.com/react-grid-layout/react-draggable) можно создать перетаскиваемый диалог. Для этого вы можете передать импортированный компонент `Draggable` в качестве `PaperComponent` компонента `Dialog`. Это сделает весь диалог перетаскиваемым.

{{"demo": "DraggableDialog.js"}}

## Прокрутка длинного содержимого <meta data-oversett="" data-original-text="Scrolling long content">

Когда диалоговые окна становятся слишком длинными для области просмотра или устройства пользователя, они прокручиваются.

-   `scroll=paper` содержимое диалога прокручивается в пределах элемента бумаги.
-   `scroll=body` содержимое диалога прокручивается в элементе body.

Попробуйте демонстрацию ниже, чтобы понять, что мы имеем в виду:

{{"demo": "ScrollDialog.js"}}

## Производительность <meta data-oversett="" data-original-text="Performance">

Следуйте [разделу "Производительность модала](/material-ui/react-modal/#performance)".

## Ограничения <meta data-oversett="" data-original-text="Limitations">

Следуйте [разделу "Ограничения Modal](/material-ui/react-modal/#limitations)".

## Дополнительные проекты <meta data-oversett="" data-original-text="Complementary projects">

### Material UI Confirm <meta data-oversett="" data-original-text="Material UI Confirm">

![stars](https://img.shields.io/github/stars/jonatanklosko/material-ui-confirm) ![npm downloads](https://img.shields.io/npm/dm/material-ui-confirm.svg)

Этот пакет предоставляет диалоговые окна для подтверждения действий пользователя без написания шаблонного кода.

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Следуйте [разделу "Доступность Modal](/material-ui/react-modal/#accessibility)".
