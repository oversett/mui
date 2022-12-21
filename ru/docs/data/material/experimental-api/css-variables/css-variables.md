

# TODO объединить с другими страницами <meta data-oversett="" data-original-text="TODO merge with other pages">

<p class="description">Узнайте об экспериментальном API для использования переменных CSS с компонентами Material UI.</p>

CSS-переменные обеспечивают значительные улучшения в работе разработчиков, связанные с темой и настройкой. С помощью этих переменных вы можете внедрить тему в таблицу стилей вашего приложения во _время сборки_, чтобы применить выбранные пользователем настройки до того, как все приложение будет отображено.

Это решает проблему мерцания SSR в темном режиме, позволяет предоставить пользователям несколько тем, помимо светлой и темной, а также улучшает отладку, среди прочих преимуществ.

Ранее эти переменные CSS были доступны только в качестве экспериментального API в пакете MUI System. Теперь они готовы для экспериментального использования в компонентах Material UI.

:::info
Если вы хотите увидеть более широкую поддержку этого API во всей библиотеке компонентов Material UI, пожалуйста, не стесняйтесь вносить свой вклад в текущую разработку. Не забудьте проверить [вопрос на GitHub](https://github.com/mui/material-ui/issues/32049), который отслеживает наш прогресс, чтобы узнать, работает ли кто-нибудь еще над интересующим вас компонентом.\
\
Мы будем благодарны за любые отзывы об этом API, поскольку он все еще находится в стадии разработки.
:::

## Введение <meta data-oversett="" data-original-text="Introduction">

API переменных CSS полагается на новый экспериментальный поставщик темы под названием `Experimental_CssVarsProvider` для внедрения стилей в компоненты Material UI. Помимо предоставления темы во внутреннем контексте React, этот новый поставщик также генерирует переменные CSS из всех токенов темы, которые не являются функциями, и делает их также доступными в контексте.

Все эти переменные доступны в объекте темы под названием `vars`. Структура этого объекта практически идентична структуре темы, единственное отличие заключается в том, что значения представляют собой CSS-переменные.

## Использование <meta data-oversett="" data-original-text="Usage">

`Experimental_CssVarsProvider` это новый экспериментальный провайдер, который присоединяет все сгенерированные CSS переменные к теме и помещает их в контекст React. Детские элементы под этим провайдером также смогут считывать CSS-переменные с сайта `theme.vars`.

```js
import { Experimental_CssVarsProvider as CssVarsProvider } from '@mui/material/styles';

function App() {
  return <CssVarsProvider>...</CssVarsProvider>;
}
```

Если вы используете TypeScript, ознакомьтесь с [настройкой типов тем](#typescript).

### Настройка компонентов <meta data-oversett="" data-original-text="Customizing components">

Поскольку API переменных CSS является экспериментальной функцией, в настоящее время она поддерживается только компонентом `Button`. Чтобы настроить его с помощью переменных CSS, вам нужно обернуть ваше приложение компонентом `Experimental_CssVarsProvider`.

Поиграйте с демонстрацией ниже!

{{"demo": "CssVariablesCustomization.js" }}

Если вы используете TypeScript, то для обновления структуры `Theme` следует использовать модульную аугментацию:

```tsx
import { Theme as MuiTheme } from '@mui/material/styles';

declare module '@mui/material/styles' {
  interface Theme {
    vars: Omit<
      MuiTheme,
      'typography' | 'mixins' | 'breakpoints' | 'direction' | 'transitions'
    >;
  }
}
```

### Настройка темы <meta data-oversett="" data-original-text="Customizing the theme">

Если вы хотите, например, переопределить цветовые схемы Material UI по умолчанию, вы можете использовать утилиту `experimental_extendTheme`.

```jsx
const theme = experimental_extendTheme({
  colorSchemes: {
    light: {
      palette: {
        primary: teal,
        secondary: deepOrange,
      },
    },
    dark: {
      palette: {
        primary: cyan,
        secondary: orange,
      },
    },
  },
});
```

{{"demo": "CssVarsCustomTheme.js" }}

Если вы используете [`ThemeProvider`](/material-ui/customization/theming/#theme-provider)вы можете заменить его новым экспериментальным провайдером.

```diff
-import { ThemeProvider, createTheme } from '@mui/material/styles';
+import { Experimental_CssVarsProvider as CssVarsProvider } from '@mui/material/styles';

 function App() {
   return (
-    <ThemeProvider theme={createTheme()}>
-      ...
-    </ThemeProvider>
+    <CssVarsProvider>
+      ...
+    </CssVarsProvider>
   )
 }
```

### Переключение между светлым и темным режимом <meta data-oversett="" data-original-text="Toggle between light and dark mode">

`Experimental_CssVarsProvider` по умолчанию предоставляет светлый и темный режим. Он сохраняет выбранный пользователем режим и синхронизирует его с локальным хранилищем браузера. Вы можете читать и обновлять режим через API `useColorScheme`.

```jsx
import {
  Experimental_CssVarsProvider as CssVarsProvider,
  useColorScheme,
} from '@mui/material/styles';

const ModeSwitcher = () => {
  const { mode, setMode } = useColorScheme();
  const [mounted, setMounted] = React.useState(false);

  React.useEffect(() => {
    setMounted(true);
  }, []);

  if (!mounted) {
    // for server-side rendering
    // Read more on https://github.com/pacocoursey/next-themes#avoid-hydration-mismatch
    return null;
  }

  return (
    <Button
      variant="outlined"
      onClick={() => {
        if (mode === 'light') {
          setMode('dark');
        } else {
          setMode('light');
        }
      }}
    >
      {mode === 'light' ? 'Dark' : 'Light'}
    </Button>
  );
};

function App() {
  return (
    <CssVarsProvider>
      <ModeSwitcher />
    </CssVarsProvider>
  );
}
```

### Рендеринг на стороне сервера <meta data-oversett="" data-original-text="Server-side rendering">

Чтобы предотвратить мерцание SSR в темном режиме во время фазы гидратации, поместите `getInitColorSchemeScript()` перед тегом `<Main />`.

#### Next.js <meta data-oversett="" data-original-text="Next.js">

Чтобы использовать API в проекте Next.js, добавьте следующий код в пользовательский [`pages/_document.js`](https://nextjs.org/docs/advanced-features/custom-document) файл:

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

#### Gatsby <meta data-oversett="" data-original-text="Gatsby">

Чтобы использовать API в проекте Gatsby, добавьте следующий код в пользовательский файл [`gatsby-ssr.js`](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-ssr/) файл:

```jsx
import React from 'react';
import { getInitColorSchemeScript } from '@mui/material/styles';

export function onRenderBody({ setPreBodyComponents }) {
  setPreBodyComponents([
    <React.Fragment key="mui-init-color-scheme-script">
      {getInitColorSchemeScript()}
    </React.Fragment>,
  ]);
}
```

### TypeScript <meta data-oversett="" data-original-text="TypeScript">

Вам необходимо импортировать дополнение темы, чтобы включить в тему `theme.vars` и другие утилиты, связанные с переменными CSS:

```ts
// this can be the root file of you application
import type {} from '@mui/material/themeCssVarsAugmentation';
```

Затем вы сможете получить доступ к `theme.vars` в любом из API стилей, например, в `styled`:

```ts
import { styled } from '@mui/material/styles';

const StyledComponent = styled('button')(({ theme }) => ({
  // typed-safe
  color: theme.vars.palette.primary.main,
}));
```

## API <meta data-oversett="" data-original-text="API">

### `<CssVarsProvider>` props <meta data-oversett="" data-original-text="<CssVarsProvider> props">

-   `defaultMode?: 'light' | 'dark' | 'system'` - Режим приложения по умолчанию (`light` по умолчанию).
-   `disableTransitionOnChange : boolean` - Отключать переходы CSS при переключении между режимами
-   `enableColorScheme: boolean` - Указывать браузеру, какая цветовая схема используется (светлая или темная) для рендеринга встроенного пользовательского интерфейса
-   `prefix: string` - префикс переменной CSS
-   `theme: ThemeInput` - тема, предоставляемая контексту React
-   `modeStorageKey?: string` - ключ localStorage, используемый для хранения приложения `mode`
-   `attribute?: string` - DOM-атрибут для применения цветовой схемы

### `useColorScheme: () => ColorSchemeContextValue` <meta data-oversett="" data-original-text="useColorScheme: () => ColorSchemeContextValue">

-   `mode: string` - выбранный пользователем режим
-   `setMode: mode => {…}` - Функция для установки `mode`. Значение `mode` сохраняется во внутреннем состоянии и локальном хранилище; если значение `mode` равно null, будет сброшен режим по умолчанию.

### `getInitColorSchemeScript: (options) => React.ReactElement` <meta data-oversett="" data-original-text="getInitColorSchemeScript: (options) => React.ReactElement">

**параметры**

-   `defaultMode?: 'light' | 'dark' | 'system'`: - режим по умолчанию приложения перед рендерингом дерева React (`light` по умолчанию)
-   `modeStorageKey?: string`: - ключ localStorage, используемый для хранения приложения `mode`
-   `attribute?: string` - DOM-атрибут для применения цветовой схемы
