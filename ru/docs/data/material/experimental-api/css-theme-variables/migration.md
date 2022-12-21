

# Переход на переменные темы CSS <meta data-oversett="" data-original-text="Migrating to CSS theme variables">

<p class="description">Пошаговое руководство по миграции для начала использования переменных тем CSS в вашем проекте.</p>

Это руководство показывает, как перевести существующий проект Material UI на переменные темы CSS. Этот переход предлагает решение давней проблемы, когда пользователь, предпочитающий темный режим, видит вспышку светлого режима при первой загрузке страницы.

## 1\. Добавьте новый поставщик <meta data-oversett="" data-original-text="1. Add the new provider">

### Без пользовательской темы <meta data-oversett="" data-original-text="Without a custom theme">

Если вы не используете [`ThemeProvider`](/material-ui/customization/theming/#theme-provider), то все, что вам нужно сделать, это обернуть ваше приложение скриптом `CssVarsProvider`:

```js
import { Experimental_CssVarsProvider as CssVarsProvider } from '@mui/material/styles';

function App() {
  return <CssVarsProvider>...your existing application</CssVarsProvider>;
}
```

Вы должны увидеть сгенерированные переменные темы CSS в таблице стилей. Компоненты Material UI, которые рендерятся внутри нового провайдера, будут автоматически использовать эти переменные.

### Пользовательская тема <meta data-oversett="" data-original-text="Custom theme">

Если у вас есть пользовательская тема, вы должны заменить `createTheme()` на `extendTheme()` API.

Это позволит перенести настройку палитры в узел `colorSchemes`. Другие свойства можно скопировать и вставить.

```diff
-import { createTheme } from '@mui/material/styles';
+import { experimental_extendTheme as extendTheme} from '@mui/material/styles';

-const lightTheme = createTheme({
-  palette: {
-   primary: {
-     main: '#ff5252',
-   },
-   ...
- },
- // ...other properties, e.g. breakpoints, spacing, shape, typography, components
-});

-const darkTheme = createTheme({
-  palette: {
-   mode: 'dark',
-   primary: {
-     main: '#000',
-   },
-   ...
- },
-});

+const theme = extendTheme({
+  colorSchemes: {
+    light: {
+      palette: {
+        primary: {
+          main: '#ff5252',
+        },
+        ...
+      },
+    },
+    dark: {
+      palette: {
+        primary: {
+          main: '#000',
+        },
+        ...
+      },
+    },
+  },
+  // ...other properties
+});
```

Затем замените `ThemeProvider` на `CssVarsProvider`:

```diff
-import { ThemeProvider } from '@mui/material/styles';
+import { Experimental_CssVarsProvider as CssVarsProvider } from '@mui/material/styles';

 const theme = extendTheme(...);

 function App() {
-  return <ThemeProvider theme={theme}>...</ThemeProvider>
+  return <CssVarsProvider theme={theme}>...</CssVarsProvider>
 }
```

Сохраните файл и запустите сервер разработки. Ваше приложение должно работать без сбоев.

:::info
Если вы столкнулись с какими-либо ошибками, пожалуйста, [откройте проблему](https://github.com/mui/material-ui/issues/new?assignees=&labels=status%3A+needs+triage&template=1.bug.yml), чтобы поделиться ею с нами. Мы будем рады помочь.
:::

Если вы осмотрите страницу, то увидите сгенерированные CSS-переменные в таблице стилей. Компоненты Material UI, которые рендерятся внутри нового провайдера, будут автоматически использовать переменные темы CSS.

## 2\. Удалите логику режима переключения <meta data-oversett="" data-original-text="2. Remove the toggle mode logic">

Вы можете удалить существующую логику, которая обрабатывает выбранный пользователем режим, и заменить ее хуком `useColorScheme`.

**До**:

```jsx
// This is only a minimal example to demonstrate the migration.
function App() {
  const [mode, setMode] = React.useState(() => {
    if (typeof window !== 'undefined') {
      return localStorage.getItem('mode') ?? 'light';
    }
    return 'light';
  });

  // a new theme is created every time the mode changes
  const theme = createTheme({
    palette: {
      mode,
    },
    // ...your custom theme
  });
  return (
    <ThemeProvider theme={theme}>
      <Button
        onClick={() => {
          const newMode = mode === 'light' ? 'dark' : 'light';
          setMode(newMode);
          localStorage.setItem('mode', newMode);
        }}
      >
        {mode === 'light' ? 'Turn dark' : 'Turn light'}
      </Button>
      ...
    </ThemeProvider>
  );
}
```

**После**:

```js
import {
  Experimental_CssVarsProvider as CssVarsProvider,
  experimental_extendTheme as extendTheme,
  useColorScheme,
} from '@mui/material/styles';

function ModeToggle() {
  const { mode, setMode } = useColorScheme();
  return (
    <Button
      onClick={() => {
        setMode(mode === 'light' ? 'dark' : 'light');
      }}
    >
      {mode === 'light' ? 'Turn dark' : 'Turn light'}
    </Button>
  );
}

const theme = extendTheme({
  // ...your custom theme
});

function App() {
  return (
    <CssVarsProvider theme={theme}>
      <ModeToggle />
      ...
    </CssVarsProvider>
  );
}
```

Хук `useColorScheme` предоставляет выбранный пользователем `mode` и функцию `setMode` для обновления значения.

Значение `mode` хранится внутри `CssVarsProvider`, который обрабатывает для вас синхронизацию локального хранилища.

## 3\. Предотвращение мерцания в темном режиме в приложениях на стороне сервера <meta data-oversett="" data-original-text="3. Prevent dark-mode flickering in server-side applications">

API `getInitColorSchemeScript()` предотвращает мерцание в темном режиме, возвращая скрипт, который должен быть запущен перед началом работы React.

### Next.js <meta data-oversett="" data-original-text="Next.js">

Разместите скрипт перед `<Main />` в вашем каталоге. [`pages/_document.js`](https://nextjs.org/docs/advanced-features/custom-document):

```jsx
import Document, { Html, Head, Main, NextScript } from 'next/document';
import { getInitColorSchemeScript } from '@mui/material/styles';

export default class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>...</Head>
        <body>
          {getInitColorSchemeScript()}
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}
```

### Gatsby <meta data-oversett="" data-original-text="Gatsby">

Поместите скрипт в ваш [`gatsby-ssr.js`](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-ssr/) файл:

```jsx
import React from 'react';
import { getInitColorSchemeScript } from '@mui/material/styles';

export function onRenderBody({ setPreBodyComponents }) {
  setPreBodyComponents([getInitColorSchemeScript()]);
}
```

## 4\. Рефакторинг пользовательских стилей для использования селектора атрибутов <meta data-oversett="" data-original-text="4. Refactor custom styles to use the attribute selector">

Пользователи будут продолжать сталкиваться с мерцанием в темном режиме, если ваши пользовательские стили включают условные выражения, как показано ниже:

```js
// theming example
extendTheme({
  components: {
    MuiChip: {
      styleOverrides: {
        root: ({ theme }) => ({
          backgroundColor:
            theme.palette.mode === 'dark'
              ? 'rgba(255 255 255 / 0.2)'
              : 'rgba(0 0 0 / 0.2)',
        }),
      },
    },
  },
});

// or a custom component example
const Button = styled('button')(({ theme }) => ({
  backgroundColor:
    theme.palette.mode === 'dark' ? 'rgba(255 255 255 / 0.2)' : 'rgba(0 0 0 / 0.2)',
}));
```

Это происходит потому, что `theme.palette.mode` всегда `light` на сервере.

Чтобы решить эту проблему, замените условные выражения селектором атрибутов:

```js
// theming example
extendTheme({
  components: {
    MuiChip: {
      styleOverrides: {
        root: ({ theme }) => ({
          backgroundColor: 'rgba(0 0 0 / 0.2)',
          [theme.getColorSchemeSelector('dark')]: {
            backgroundColor: 'rgba(255 255 255 / 0.2)',
          },
        }),
      },
    },
  },
});

// or a custom component example
const Button = styled('button')(({ theme }) => ({
  backgroundColor: 'rgba(0 0 0 / 0.2)',
  [theme.getColorSchemeSelector('dark')]: {
    backgroundColor: 'rgba(255 255 255 / 0.2)',
  },
}));
```

:::warning
`theme.getColorSchemeSelector()` - это служебная функция, которая возвращает селектор атрибутов `'[data-mui-color-scheme="dark"] &'`.

Обратите внимание, что селектор атрибутов создает более высокую специфичность CSS, что может быть обременительным для тематического оформления.
:::

## 5\. Проверка мерцания в темном режиме <meta data-oversett="" data-original-text="5. Test dark-mode flickering">

1.  Включите темный режим в вашем приложении
2.  Откройте DevTools и установите [дросселирование процессора](https://developer.chrome.com/docs/devtools/evaluate-performance/#simulate_a_mobile_cpu) на минимальное значение (не закрывайте DevTools).
3.  Обновите страницу. На первый взгляд вы должны увидеть все компоненты в темном режиме.
