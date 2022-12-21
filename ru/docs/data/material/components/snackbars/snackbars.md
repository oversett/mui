---
product: material-ui
title: React Snackbar component
components: Snackbar, SnackbarContent
githubLabel: 'component: snackbar'
materialDesign: https://m2.material.io/components/snackbars
waiAria: https://www.w3.org/TR/wai-aria-1.1/#alert
---

# Закусочная <meta data-oversett="" data-original-text="Snackbar">

<p class="description">Закусочные панели предоставляют краткие уведомления. Этот компонент также известен как тост.</p>

Закусочные панели информируют пользователей о процессе, который приложение выполнило или будет выполнять. Они появляются временно, в нижней части экрана. Они не должны прерывать работу пользователя и не требуют его ввода, чтобы исчезнуть.

Закусочные панели содержат одну строку текста, непосредственно связанную с выполняемой операцией. Они могут содержать текстовое действие, но без пиктограмм. Их можно использовать для отображения уведомлений.

{{"component": "modules/components/ComponentLinkHeader.js"}}

**Частота**: Одновременно может отображаться только одна закусочная панель.

## Простые закуски <meta data-oversett="" data-original-text="Simple snackbars">

Базовая закусочная панель, цель которой - воспроизвести поведение закусочной панели Google Keep.

{{"demo": "SimpleSnackbar.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Подробнее об этом вы можете узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedSnackbars.js"}}

## Расположенные закуски <meta data-oversett="" data-original-text="Positioned snackbars">

В широких макетах закуски могут быть выровнены по левому краю или по центру, если они последовательно размещаются на одном и том же месте в нижней части экрана, однако могут возникнуть обстоятельства, когда размещение закуски должно быть более гибким. Вы можете управлять положением закуски, указав параметр `anchorOrigin`.

{{"demo": "PositionedSnackbar.js"}}

## Длина сообщения <meta data-oversett="" data-original-text="Message Length">

Некоторые закуски имеют различную длину сообщения.

{{"demo": "LongTextSnackbar.js"}}

## Переходы <meta data-oversett="" data-original-text="Transitions">

### Последовательные закуски <meta data-oversett="" data-original-text="Consecutive Snackbars">

Когда необходимо несколько обновлений закусочной, они должны появляться по одному.

{{"demo": "ConsecutiveSnackbars.js"}}

### Закусочные панели и плавающие кнопки действий (FAB) <meta data-oversett="" data-original-text="Snackbars and floating action buttons (FABs)">

Закусочные панели должны появляться над FAB (на мобильных устройствах).

{{"demo": "FabIntegrationSnackbar.js", "iframe": true, "maxWidth": 400}}

### Изменение перехода <meta data-oversett="" data-original-text="Change transition">

По умолчанию используется переход[Grow](/material-ui/transitions/#grow), но вы можете использовать другой переход.

{{"demo": "TransitionsSnackbar.js"}}

### Управление направлением слайда <meta data-oversett="" data-original-text="Control Slide direction">

Вы можете изменить направление перехода [слайда](/material-ui/transitions/#slide).

Пример: сделать переход слайда влево:

```jsx
import Slide from '@mui/material/Slide';

function TransitionLeft(props) {
  return <Slide {...props} direction="left" />;
}

export default function MyComponent() {
  return <Snackbar TransitionComponent={TransitionLeft} />;
}
```

Другие примеры:

{{"demo": "DirectionSnackbar.js"}}

## Взаимодополняющие проекты <meta data-oversett="" data-original-text="Complementary projects">

Для более сложных случаев использования вы можете воспользоваться:

### notistack <meta data-oversett="" data-original-text="notistack">

![stars](https://img.shields.io/github/stars/iamhosseindhv/notistack.svg?style=social&label=Stars) ![npm downloads](https://img.shields.io/npm/dm/notistack.svg)

Этот пример демонстрирует, как использовать [notistack](https://github.com/iamhosseindhv/notistack). notistack имеет **императивный API**, который позволяет легко отображать закусочные панели без необходимости обрабатывать их состояние открытия/закрытия. Он также позволяет **складывать** их друг на друга (хотя это и не рекомендуется руководством Material Design).

{{"demo": "IntegrationNotistack.js", "defaultCodeOpen": false}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/TR/wai-aria-1.1/#alert)](https://www.w3.org/TR/wai-aria-1.1/#alert)

По умолчанию панель закусок не будет автоматически скрываться. Однако если вы решите использовать реквизит `autoHideDuration`, рекомендуется дать пользователю [достаточно времени](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) для ответа.

При открытии **каждая** `Snackbar` будет уволена, если нажата <kbd class="key">Escape</kbd>. Если только вы не обрабатываете `onClose` с помощью причины `"escapeKeyDown"`. Если вы хотите ограничить это поведение, чтобы уволить только самую старую из открытых в данный момент закусочных, вызовите `event.preventDefault` в `onClose`.

```jsx
export default function MyComponent() {
  const [open, setOpen] = React.useState(true);

  return (
    <React.Fragment>
      <Snackbar
        open={open}
        onClose={(event, reason) => {
          // `reason === 'escapeKeyDown'` if `Escape` was pressed
          setOpen(false);
          // call `event.preventDefault` to only close one Snackbar at a time.
        }}
      />
      <Snackbar open={open} onClose={() => setOpen(false)} />
    </React.Fragment>
  );
}
```
