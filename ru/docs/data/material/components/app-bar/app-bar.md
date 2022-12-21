---
product: material-ui
title: App Bar React component
components: AppBar, Toolbar, Menu
githubLabel: 'component: app bar'
materialDesign: https://m2.material.io/components/app-bars-top
---

# Панель приложений <meta data-oversett="" data-original-text="App Bar">

<p class="description">Панель приложений отображает информацию и действия, относящиеся к текущему экрану.</p>

Верхняя панель App Bar предоставляет содержимое и действия, относящиеся к текущему экрану. Она используется для брендинга, заголовков экранов, навигации и действий.

Она может превращаться в контекстную панель действий или использоваться в качестве навигационной панели.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основная панель приложений <meta data-oversett="" data-original-text="Basic App bar">

{{"demo": "ButtonAppBar.js", "bg": true}}

## Панель приложений с меню <meta data-oversett="" data-original-text="App bar with menu">

{{"demo": "MenuAppBar.js", "bg": true}}

## Панель приложений с отзывчивым меню <meta data-oversett="" data-original-text="App bar with responsive menu">

{{"demo": "ResponsiveAppBar.js", "bg": true}}

## Панель приложений с полем поиска <meta data-oversett="" data-original-text="App bar with search field">

Боковая панель поиска.

{{"demo": "SearchAppBar.js", "bg": true}}

## Отзывчивая панель приложений с ящиком <meta data-oversett="" data-original-text="Responsive App bar with Drawer">

{{"demo": "DrawerAppBar.js", "bg": true,"iframe": true}}

## Панель приложений с основным полем поиска <meta data-oversett="" data-original-text="App bar with a primary search field">

Основная панель поиска.

{{"demo": "PrimarySearchAppBar.js", "bg": true}}

## Плотная (только для настольных компьютеров) <meta data-oversett="" data-original-text="Dense (desktop only)">

{{"demo": "DenseAppBar.js", "bg": true}}

## Выдающийся <meta data-oversett="" data-original-text="Prominent">

Выделяющаяся панель приложений.

{{"demo": "ProminentAppBar.js", "bg": true}}

## Нижняя панель приложений <meta data-oversett="" data-original-text="Bottom App bar">

{{"demo": "BottomAppBar.js", "iframe": true, "maxWidth": 400}}

## Фиксированное размещение <meta data-oversett="" data-original-text="Fixed placement">

При фиксированном размещении панели приложений размер элемента не влияет на остальную часть страницы. Это может привести к тому, что часть контента окажется невидимой за панелью приложений. Вот 3 возможных решения:

1.  Вы можете использовать `position="sticky"` вместо фиксированного. ⚠️ sticky не поддерживается IE11.
2.  Вы можете отобразить второй компонент `<Toolbar />`:

```jsx
function App() {
  return (
    <React.Fragment>
      <AppBar position="fixed">
        <Toolbar>{/* content */}</Toolbar>
      </AppBar>
      <Toolbar />
    </React.Fragment>
  );
}
```

3.  Вы можете использовать `theme.mixins.toolbar` CSS:

```jsx
const Offset = styled('div')(({ theme }) => theme.mixins.toolbar);

function App() {
  return (
    <React.Fragment>
      <AppBar position="fixed">
        <Toolbar>{/* content */}</Toolbar>
      </AppBar>
      <Offset />
    </React.Fragment>
  );
}
```

## Прокрутка <meta data-oversett="" data-original-text="Scrolling">

Вы можете использовать хук `useScrollTrigger()` для реагирования на действия пользователя по прокрутке.

### Скрыть панель приложений <meta data-oversett="" data-original-text="Hide App bar">

Полоса приложений скрывается при прокрутке вниз, чтобы оставить больше места для чтения.

{{"demo": "HideAppBar.js", "iframe": true, "disableLiveEdit": true}}

### Поднять панель приложений <meta data-oversett="" data-original-text="Elevate App bar">

Полоса приложения поднимается при прокрутке, чтобы сообщить пользователю, что он находится не в верхней части страницы.

{{"demo": "ElevateAppBar.js", "iframe": true, "disableLiveEdit": true}}

### Вернуться к началу <meta data-oversett="" data-original-text="Back to top">

Плавающая кнопка действия появляется при прокрутке, чтобы легко вернуться к началу страницы.

{{"demo": "BackToTop.js", "iframe": true, "disableLiveEdit": true}}

### `useScrollTrigger([options]) => trigger` <meta data-oversett="" data-original-text="useScrollTrigger([options]) => trigger">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `options` _(object_ \[optional\]):
    
    -   `options.disableHysteresis` _(bool_ \[необязательно\]): По умолчанию `false`. Отключить гистерезис. Игнорировать направление прокрутки при определении значения `trigger`.
    -   `options.target` _(Узел_ \[необязательно\]): По умолчанию `window`.
    -   `options.threshold` _(Число_ \[необязательно\]): По умолчанию `100`. Изменить значение `trigger`, когда вертикальная прокрутка строго пересекает этот порог (исключение).

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`trigger`: Соответствует ли положение прокрутки заданным критериям?

#### Примеры <meta data-oversett="" data-original-text="Examples">

```jsx
import useScrollTrigger from '@mui/material/useScrollTrigger';

function HideOnScroll(props) {
  const trigger = useScrollTrigger();
  return (
    <Slide in={!trigger}>
      <div>Hello</div>
    </Slide>
  );
}
```

## Включить цвет на темном фоне <meta data-oversett="" data-original-text="Enable color on dark">

В соответствии с [рекомендациями Material Design](https://m2.material.io/design/color/dark-theme.html), параметр `color` не влияет на внешний вид панели приложения в темном режиме. Вы можете отменить это поведение, установив параметр `enableColorOnDark` в значение `true`.

{{"demo": "EnableColorOnDarkAppBar.js", "bg": true}}
