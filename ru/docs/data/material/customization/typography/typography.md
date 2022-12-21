

# Типографика <meta data-oversett="" data-original-text="Typography">

<p class="description">Тема предоставляет набор шрифтов, которые хорошо сочетаются друг с другом, а также с сеткой макета.</p>

## Семейство шрифтов <meta data-oversett="" data-original-text="Font family">

Вы можете изменить семейство шрифтов с помощью свойства `theme.typography.fontFamily`.

Например, в этом примере используется системный шрифт вместо шрифта Roboto по умолчанию:

```js
const theme = createTheme({
  typography: {
    fontFamily: [
      '-apple-system',
      'BlinkMacSystemFont',
      '"Segoe UI"',
      'Roboto',
      '"Helvetica Neue"',
      'Arial',
      'sans-serif',
      '"Apple Color Emoji"',
      '"Segoe UI Emoji"',
      '"Segoe UI Symbol"',
    ].join(','),
  },
});
```

### Самостоятельно размещаемые шрифты <meta data-oversett="" data-original-text="Self-hosted fonts">

Чтобы самостоятельно разместить шрифты, загрузите файлы шрифтов в форматах `ttf`, `woff`, и/или `woff2` и импортируйте их в свой код.

⚠️ Это требует наличия в процессе сборки плагина или загрузчика, который может обрабатывать загрузку файлов `ttf`, `woff` и`woff2`. Шрифты _не_ будут встроены в ваш пакет. Они будут загружены с вашего веб-сервера, а не из CDN.

```js
import RalewayWoff2 from './fonts/Raleway-Regular.woff2';
```

Далее необходимо изменить тему для использования нового шрифта. Для того чтобы глобально определить Raleway как шрифт, можно использовать компонент [`CssBaseline`](/material-ui/react-css-baseline/) (или любое другое CSS-решение на ваш выбор).

```jsx
import RalewayWoff2 from './fonts/Raleway-Regular.woff2';

const theme = createTheme({
  typography: {
    fontFamily: 'Raleway, Arial',
  },
  components: {
    MuiCssBaseline: {
      styleOverrides: `
        @font-face {
          font-family: 'Raleway';
          font-style: normal;
          font-display: swap;
          font-weight: 400;
          src: local('Raleway'), local('Raleway-Regular'), url(${RalewayWoff2}) format('woff2');
          unicodeRange: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF;
        }
      `,
    },
  },
});

// ...
return (
  <ThemeProvider theme={theme}>
    <CssBaseline />
    <Box
      sx={{
        fontFamily: 'Raleway',
      }}
    >
      Raleway
    </Box>
  </ThemeProvider>
);
```

Обратите внимание, что если вы хотите добавить дополнительные объявления `@font-face`, вам нужно использовать синтаксис шаблона строкового CSS для добавления переопределений стиля, чтобы не заменять ранее определенные объявления `@font-face`.

## Размер шрифта <meta data-oversett="" data-original-text="Font size">

MUI использует единицы `rem` для размера шрифта. Размер шрифта по умолчанию в браузере `<html>` элемента `16px`, но браузеры имеют возможность изменить это значение, поэтому единицы `rem` позволяют нам учитывать настройки пользователя, что приводит к лучшей поддержке доступности. Пользователи изменяют настройки размера шрифта по разным причинам, от плохого зрения до выбора оптимальных настроек для устройств, которые могут сильно отличаться по размеру и расстоянию просмотра.

Для изменения размера шрифта в MUI можно указать свойство `fontSize`. Значение по умолчанию - `14px`.

```js
const theme = createTheme({
  typography: {
    // In Chinese and Japanese the characters are usually larger,
    // so a smaller fontsize may be appropriate.
    fontSize: 12,
  },
});
```

Размер шрифта, вычисляемый браузером, соответствует этому математическому уравнению:

<div class="only-light-mode"><img alt="font size calculation" style="width: 458px;" src="/static/images/font-size.svg"></div><div class="only-dark-mode"><img alt="font size calculation" style="width: 458px;" src="/static/images/font-size-dark.svg"></div>

### Отзывчивые размеры шрифтов <meta data-oversett="" data-original-text="Responsive font sizes">

Свойства [варианта](#variants) `theme.typography.*` отображаются непосредственно в сгенерированном CSS. Вы можете использовать [медиа-запросы](/material-ui/customization/breakpoints/#api) внутри них:

```js
const theme = createTheme();

theme.typography.h3 = {
  fontSize: '1.2rem',
  '@media (min-width:600px)': {
    fontSize: '1.5rem',
  },
  [theme.breakpoints.up('md')]: {
    fontSize: '2.4rem',
  },
};
```

{{"demo": "CustomResponsiveFontSizes.js"}}

Чтобы автоматизировать эту настройку, вы можете использовать [`responsiveFontSizes()`](/material-ui/customization/theming/#responsivefontsizes-theme-options-theme) чтобы сделать размеры шрифтов Typography в теме отзывчивыми.

{{"demo": "ResponsiveFontSizesChart.js", "hideToolbar": true}}

Вы можете увидеть это в действии в примере ниже. Настройте размер окна вашего браузера и обратите внимание, как изменяется размер шрифта при переходе ширины через различные [точки разрыва](/material-ui/customization/breakpoints/):

```js
import { createTheme, responsiveFontSizes } from '@mui/material/styles';

let theme = createTheme();
theme = responsiveFontSizes(theme);
```

{{"demo": "ResponsiveFontSizes.js"}}

### Изменение размера шрифта <meta data-oversett="" data-original-text="Fluid font sizes">

Будет сделано: [#15251](https://github.com/mui/material-ui/issues/15251).

### Размер шрифта HTML <meta data-oversett="" data-original-text="HTML font size">

Вы можете захотеть изменить размер шрифта по умолчанию элемента `<html>`. Например, при использовании [упрощения 10px](https://www.sitepoint.com/understanding-and-using-rem-units-in-css/).

:::warning
Изменение размера шрифта может повредить доступности ♿️. Большинство браузеров согласны с размером шрифта по умолчанию 16px, но пользователь может изменить его. Например, человек с ослабленным зрением может установить в своем браузере размер шрифта по умолчанию на более крупный.
:::

Для этого случая предусмотрено свойство `theme.typography.htmlFontSize`, которое сообщает MUI размер шрифта в элементе `<html>`. Оно используется для корректировки значения `rem`, чтобы вычисленный размер шрифта всегда соответствовал спецификации.

```js
const theme = createTheme({
  typography: {
    // Tell MUI what's the font-size on the html element is.
    htmlFontSize: 10,
  },
});
```

```css
html {
  font-size: 62.5%; /* 62.5% of 16px = 10px */
}
```

_Вам нужно применить вышеупомянутый CSS к html-элементу этой страницы, чтобы увидеть корректное отображение приведенной ниже демонстрации._

{{"demo": "FontSizeTheme.js"}}

## Варианты <meta data-oversett="" data-original-text="Variants">

По умолчанию объект типографики поставляется с [13 вариантами](/material-ui/react-typography/#component):

-   h1
-   h2
-   h3
-   h4
-   h5
-   h6
-   субтитр1
-   субтитр2
-   тело1
-   тело2
-   кнопка
-   надпись
-   надпись

Каждый из этих вариантов может быть настроен индивидуально:

```js
const theme = createTheme({
  typography: {
    subtitle1: {
      fontSize: 12,
    },
    body1: {
      fontWeight: 500,
    },
    button: {
      fontStyle: 'italic',
    },
  },
});
```

{{"demo": "TypographyVariants.js"}}

## Добавление и отключение вариантов <meta data-oversett="" data-original-text="Adding &amp; disabling variants">

Помимо использования вариантов типографики по умолчанию, вы можете добавлять собственные варианты или отключать те, которые вам не нужны. Вот что для этого нужно сделать:

**Шаг 1. Обновите объект типографики темы**

```js
const theme = createTheme({
  typography: {
    poster: {
      color: 'red',
    },
    // Disable h3 variant
    h3: undefined,
  },
});
```

**Шаг 2. Обновите необходимые варианты типографики (если вы используете TypeScript)**

:::info
Если вы не используете TypeScript, вам следует пропустить этот шаг.
:::

Вам необходимо убедиться, что типизация вариантов темы `typography` и объекта `Typography`'s `variant` отражает новый набор вариантов.

```ts
declare module '@mui/material/styles' {
  interface TypographyVariants {
    poster: React.CSSProperties;
  }

  // allow configuration using `createTheme`
  interface TypographyVariantsOptions {
    poster?: React.CSSProperties;
  }
}

// Update the Typography's variant prop options
declare module '@mui/material/Typography' {
  interface TypographyPropsVariantOverrides {
    poster: true;
    h3: false;
  }
}
```

**Шаг 3. Теперь вы можете использовать новый вариант**

{{"demo": "TypographyCustomVariant.js", "hideToolbar": true}}

```jsx
<Typography variant="poster">poster</Typography>;

/* This variant is no longer supported */
<Typography variant="h3">h3</Typography>;
```

## Значения по умолчанию <meta data-oversett="" data-original-text="Default values">

Вы можете изучить значения типографики по умолчанию с помощью [проводника тем](/material-ui/customization/default-theme/?expand-path=$.typography) или открыв консоль dev tools на этой странице (`window.theme.typography`).
