

# Темный режим <meta data-oversett="" data-original-text="Dark mode">

<p class="description">Material UI поставляется с двумя режимами палитры: светлым (по умолчанию) и темным.</p>

## Темный режим по умолчанию <meta data-oversett="" data-original-text="Dark mode by default">

Вы можете заставить свое приложение использовать темную тему по умолчанию - независимо от предпочтений пользователя - добавив `mode: 'dark'` к помощнику `createTheme`:

```js
import { ThemeProvider, createTheme } from '@mui/material/styles';
import CssBaseline from '@mui/material/CssBaseline';

const darkTheme = createTheme({
  palette: {
    mode: 'dark',
  },
});

function App() {
  return (
    <ThemeProvider theme={darkTheme}>
      <CssBaseline />
      <main>This app is using the dark mode</main>
    </ThemeProvider>
  );
}

export default App;
```

Добавление `mode: 'dark'` к помощнику `createTheme` изменяет несколько значений палитры, как показано в следующем примере:

{{"demo": "DarkTheme.js", "bg": "inline", "hideToolbar": true}}

Добавление `<CssBaseline />` внутрь компонента `<ThemeProvider>` также включит темный режим для фона приложения.

:::warning
Установка темного режима таким образом работает только в том случае, если вы используете [палитру по умолчанию](/material-ui/customization/default-theme/). Если у вас пользовательская палитра, убедитесь, что у вас правильные значения, основанные на `mode`. Следующий раздел объясняет, как это сделать.
:::

## Темный режим с пользовательской палитрой <meta data-oversett="" data-original-text="Dark mode with a custom palette">

Чтобы использовать пользовательские палитры для светлого и темного режимов, можно создать функцию, которая будет возвращать правильную палитру в зависимости от выбранного режима, как показано здесь:

```ts
const getDesignTokens = (mode: PaletteMode) => ({
  palette: {
    mode,
    ...(mode === 'light'
      ? {
          // palette values for light mode
          primary: amber,
          divider: amber[200],
          text: {
            primary: grey[900],
            secondary: grey[800],
          },
        }
      : {
          // palette values for dark mode
          primary: deepOrange,
          divider: deepOrange[700],
          background: {
            default: deepOrange[900],
            paper: deepOrange[900],
          },
          text: {
            primary: '#fff',
            secondary: grey[500],
          },
        }),
  },
});
```

На примере видно, что используются разные цвета в зависимости от того, какой режим выбран - светлый или темный. Следующим шагом будет использование этой функции при создании темы.

```tsx
export default function App() {
  const [mode, setMode] = React.useState<PaletteMode>('light');
  const colorMode = React.useMemo(
    () => ({
      // The dark mode switch would invoke this method
      toggleColorMode: () => {
        setMode((prevMode: PaletteMode) =>
          prevMode === 'light' ? 'dark' : 'light',
        );
      },
    }),
    [],
  );

  // Update the theme only if the mode changes
  const theme = React.useMemo(() => createTheme(getDesignTokens(mode)), [mode]);

  return (
    <ColorModeContext.Provider value={colorMode}>
      <ThemeProvider theme={theme}>
        <Page />
      </ThemeProvider>
    </ColorModeContext.Provider>
  );
}
```

Вот полностью рабочий пример:

{{"demo": "DarkThemeWithCustomPalette.js", "defaultCodeOpen": false}}

## Переключение цветового режима <meta data-oversett="" data-original-text="Toggling color mode">

Чтобы дать пользователям возможность переключать режимы, вы можете добавить контекст React в событие кнопки `onClick`, как показано в следующем примере:

{{"demo": "ToggleColorMode.js", "defaultCodeOpen": false}}

## Системные предпочтения <meta data-oversett="" data-original-text="System preference">

Пользователи могут иметь предпочтение светлого или темного режима, которое они установили в своей операционной системе - либо в масштабах всей системы, либо для отдельного пользовательского агента.

Вы можете использовать эти предпочтения с помощью хука [useMediaQuery](/material-ui/react-use-media-query/) и медиазапроса [prefers-color-scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme).

Следующая демонстрация показывает, как автоматически включить темный режим, проверяя предпочтения пользователя в настройках его ОС или браузера:

```jsx
import * as React from 'react';
import useMediaQuery from '@mui/material/useMediaQuery';
import { createTheme, ThemeProvider } from '@mui/material/styles';
import CssBaseline from '@mui/material/CssBaseline';

function App() {
  const prefersDarkMode = useMediaQuery('(prefers-color-scheme: dark)');

  const theme = React.useMemo(
    () =>
      createTheme({
        palette: {
          mode: prefersDarkMode ? 'dark' : 'light',
        },
      }),
    [prefersDarkMode],
  );

  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <Routes />
    </ThemeProvider>
  );
}
```
