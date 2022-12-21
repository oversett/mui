

# Переходы <meta data-oversett="" data-original-text="Transitions">

<p class="description">Ключ темы позволяет настраивать длительность и смягчение различных переходов, используемых в компонентах MUI, а также предлагает утилиту для создания пользовательских переходов.</p>

## API <meta data-oversett="" data-original-text="API">

### `theme.transitions.create(props, options) => transition` <meta data-oversett="" data-original-text="theme.transitions.create(props, options) => transition">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `props` _(string_ | _string\[\]_): По умолчанию `['all']`. Предоставляет CSS-свойство или список CSS-свойств, для которых должен быть выполнен переход.
2.  `options` _(объект_ \[необязательно\]):

-   `options.duration` _(строка_ | _число_ \[необязательно\]): По умолчанию `theme.transitions.duration.standard`. Предоставляет длительность перехода.
-   `options.easing` _(строка_ \[необязательно\]): По умолчанию `theme.transitions.easing.easeInOut`. Предоставляет смягчение для перехода.
-   `options.delay` _(строка_ | _число_ \[необязательно\]): По умолчанию `0`. Предоставляет задержку для перехода.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`transition`: Значение CSS-перехода, в котором собраны все CSS-свойства, которые должны быть переведены, вместе с заданной длительностью, смягчением и задержкой.

Используйте помощник `theme.transitions.create()` для создания последовательных переходов для элементов вашего пользовательского интерфейса.

```js
theme.transitions.create(['background-color', 'transform']);
```

#### Пример <meta data-oversett="" data-original-text="Example">

{{"demo": "TransitionHover.js", "defaultCodeOpen": false}}

### `theme.transitions.getAutoHeightDuration(height) => duration` <meta data-oversett="" data-original-text="theme.transitions.getAutoHeightDuration(height) => duration">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `height` _(число_): Высота компонента.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`duration`: Вычисленная продолжительность на основе высоты.

## Длительности <meta data-oversett="" data-original-text="Durations">

Вы можете изменить некоторые или все значения длительности, или предоставить свои собственные (для использования в помощнике `create()` ). В этом примере показаны все значения по умолчанию (в миллисекундах), но вам нужно указать только те ключи, которые вы хотите изменить или добавить.

```js
const theme = createTheme({
  transitions: {
    duration: {
      shortest: 150,
      shorter: 200,
      short: 250,
      // most basic recommended timing
      standard: 300,
      // this is to be used in complex animations
      complex: 375,
      // recommended when something is entering screen
      enteringScreen: 225,
      // recommended when something is leaving screen
      leavingScreen: 195,
    },
  },
});
```

## Easings <meta data-oversett="" data-original-text="Easings">

Вы можете изменить некоторые или все значения смягчения или предоставить свои собственные, указав пользовательское значение CSS `transition-timing-function`.

```js
const theme = createTheme({
  transitions: {
    easing: {
      // This is the most common easing curve.
      easeInOut: 'cubic-bezier(0.4, 0, 0.2, 1)',
      // Objects enter the screen at full velocity from off-screen and
      // slowly decelerate to a resting point.
      easeOut: 'cubic-bezier(0.0, 0, 0.2, 1)',
      // Objects leave the screen at full velocity. They do not decelerate when off-screen.
      easeIn: 'cubic-bezier(0.4, 0, 1, 1)',
      // The sharp curve is used by objects that may return to the screen at any time.
      sharp: 'cubic-bezier(0.4, 0, 0.6, 1)',
    },
  },
});
```

## Ссылки <meta data-oversett="" data-original-text="References">

Посетите страницу [Переходы](/material-ui/transitions/), чтобы изучить компоненты переходов, включенные в MUI.
