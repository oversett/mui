---
product: material-ui
components: CssBaseline, ScopedCssBaseline
githubLabel: 'component: CssBaseline'
---

# Базовая линия CSS <meta data-oversett="" data-original-text="CSS Baseline">

<p class="description">Компонент CssBaseline помогает создать элегантный, последовательный и простой базовый уровень, на который можно опираться.</p>

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Глобальный сброс <meta data-oversett="" data-original-text="Global reset">

Вы можете быть знакомы с [normalize.css](https://github.com/necolas/normalize.css), коллекцией нормализаций стилей элементов и атрибутов HTML.

```jsx
import * as React from 'react';
import CssBaseline from '@mui/material/CssBaseline';

export default function MyApp() {
  return (
    <React.Fragment>
      <CssBaseline />
      {/* The rest of your application */}
    </React.Fragment>
  );
}
```

## Скопинг на дочерние элементы <meta data-oversett="" data-original-text="Scoping on children">

Однако, если вы постепенно переводите сайт на MUI, использование глобального сброса может оказаться неприемлемым. Можно применить базовую линию только к дочерним элементам с помощью компонента `ScopedCssBaseline`.

```jsx
import * as React from 'react';
import ScopedCssBaseline from '@mui/material/ScopedCssBaseline';
import MyApp from './MyApp';

export default function MyApp() {
  return (
    <ScopedCssBaseline>
      {/* The rest of your application */}
      <MyApp />
    </ScopedCssBaseline>
  );
}
```

⚠️ Убедитесь, что вы сначала импортировали компонент `ScopedCssBaseline`, чтобы избежать конфликтов размеров ящиков, как в приведенном выше примере.

## Подход <meta data-oversett="" data-original-text="Approach">

### Страница <meta data-oversett="" data-original-text="Page">

Элементы `<html>` и `<body>` обновлены для обеспечения лучших значений по умолчанию для всей страницы. Более конкретно:

-   Убрана маржа во всех браузерах.
-   По умолчанию применяется цвет фона Material Design. Он использует [`theme.palette.background.default`](/material-ui/customization/default-theme/?expand-path=$.palette.background) для стандартных устройств и белый фон для устройств печати.
-   Если `enableColorScheme` указан на `CssBaseline`, родной цвет компонентов будет установлен с помощью применения [`color-scheme`](https://web.dev/color-scheme/) на `<html>`. Используемое значение задается свойством темы `theme.palette.mode`.

### Макет <meta data-oversett="" data-original-text="Layout">

-   `box-sizing` устанавливается глобально на элементе `<html>` в `border-box`. Каждый элемент, включая `*::before` и `*::after`, объявляется наследующим это свойство, что гарантирует, что объявленная ширина элемента никогда не будет превышена из-за набивки или границы.

### Полосы прокрутки <meta data-oversett="" data-original-text="Scrollbars">

:::error
Этот API устарел. Вместо него можно использовать [color-scheme](#color-scheme).
:::

Цвета полос прокрутки могут быть настроены для улучшения контраста (особенно в Windows). Добавьте этот код в вашу тему (для темного режима).

```jsx
import darkScrollbar from '@mui/material/darkScrollbar';

const theme = createTheme({
  components: {
    MuiCssBaseline: {
      styleOverrides: (themeParam) => ({
        body: themeParam.palette.mode === 'dark' ? darkScrollbar() : null,
      }),
    },
  },
});
```

Однако имейте в виду, что использование этой утилиты (и настройка `-webkit-scrollbar`) заставляет macOS всегда показывать полосу прокрутки.

### Цветовая схема <meta data-oversett="" data-original-text="Color scheme">

Этот API появился в @mui/material (v5.1.0) для переключения между режимами `"light"` и `"dark"` нативных компонентов, таких как скроллбар, с помощью свойства `color-scheme` CSS. Чтобы включить его, вы можете установить `enableColorScheme=true` следующим образом:

```jsx
<CssBaseline enableColorScheme />

// or

<ScopedCssBaseline enableColorScheme >
  {/* The rest of your application using color-scheme*/}
</ScopedCssBaseline>
```

### Типографика <meta data-oversett="" data-original-text="Typography">

-   Базовый размер шрифта на `<html>` не объявлен, но предполагается 16px (браузер по умолчанию). Вы можете узнать больше о последствиях изменения размера шрифта по умолчанию `<html>` на странице [документации темы](/material-ui/customization/typography/#html-font-size).
-   Установите стиль `theme.typography.body1` для элемента `<body>`.
-   Установите font-weight на `theme.typography.fontWeightBold` для элементов `<b>` и `<strong>`.
-   Для лучшего отображения шрифта Roboto включено пользовательское сглаживание шрифта.

## Настройка <meta data-oversett="" data-original-text="Customization">

Чтобы изменить вывод этих компонентов, перейдите в раздел документации, посвященный [глобальной настройке](/material-ui/customization/how-to-customize/#4-global-css-override).
