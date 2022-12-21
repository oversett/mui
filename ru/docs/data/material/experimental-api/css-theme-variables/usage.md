

# Переменные темы CSS - Использование <meta data-oversett="" data-original-text="CSS theme variables - Usage">

<p class="description">Узнайте, как использовать экспериментальные API для принятия переменных темы CSS.</p>

## Начало работы <meta data-oversett="" data-original-text="Getting started">

`Experimental_CssVarsProvider` это провайдер, который генерирует переменные темы CSS и прикрепляет ссылку на объект темы (контекст React).

```js
import { Experimental_CssVarsProvider as CssVarsProvider } from '@mui/material/styles';

function App() {
  return <CssVarsProvider>...</CssVarsProvider>;
}
```

После рендеринга `App` на экране вы увидите переменные темы CSS в таблице стилей html `:root`. По умолчанию переменные сглажены и имеют префикс `--mui`:

```css
/* generated global stylesheet */
:root {
  --mui-palette-primary-main: #1976d2;
  --mui-palette-primary-light: #42a5f5;
  --mui-palette-primary-dark: #1565c0;
  --mui-palette-primary-contrastText: #fff;
  /* ...other variables */
}
```

:::info
`CssVarsProvider` построен поверх [`ThemeProvider`](/material-ui/customization/theming/#themeprovider) с дополнительными возможностями, такими как генерация переменных CSS, синхронизация хранилищ, неограниченные цветовые схемы и многое другое.
:::

## Переключение между светлым и темным режимом <meta data-oversett="" data-original-text="Toggle between light and dark mode">

Хук `useColorScheme` позволяет считывать и обновлять выбранный пользователем режим:

```jsx
import {
  Experimental_CssVarsProvider as CssVarsProvider,
  useColorScheme,
} from '@mui/material/styles';

// ModeSwitcher is an example interface for toggling between modes.
// Material UI does not provide the toggle interface—you have to build it yourself.
const ModeSwitcher = () => {
  const { mode, setMode } = useColorScheme();
  const [mounted, setMounted] = React.useState(false);

  React.useEffect(() => {
    setMounted(true);
  }, []);

  if (!mounted) {
    // for server-side rendering
    // learn more at https://github.com/pacocoursey/next-themes#avoid-hydration-mismatch
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

## Использование переменных темы <meta data-oversett="" data-original-text="Using theme variables">

-   `theme.vars` (рекомендуется): объект, который ссылается на переменные темы CSS.
    
    ```js
    const Button = styled('button')(({ theme }) => ({
      backgroundColor: theme.vars.palette.primary.main, // var(--mui-palette-primary-main)
      color: theme.vars.palette.primary.contrastText, // var(--mui-palette-primary-contrastText)
    }));
    ```
    
    В **TypeScript** переменные темы не включены по умолчанию. Следуйте [настройкам TypeScript](#typescript), чтобы включить переменные темы.
    
    :::warning
    Убедитесь, что компоненты, обращающиеся к `theme.vars.*`, отрисовываются под новым провайдером, иначе вы получите `TypeError`.
    :::
    
-   **Native CSS**: если вы не можете получить доступ к объекту темы, например, в чистом файле CSS, вы можете использовать [`var()`](https://developer.mozilla.org/en-US/docs/Web/CSS/var) напрямую:
    
    ```css
    /* external-scope.css */
    .external-section {
      background-color: var(--mui-palette-grey-50);
    }
    ```
    
    :::warning
    Если вы настроили [пользовательский префикс](/material-ui/experimental-api/css-theme-variables/customization/#changing-variable-prefixes), убедитесь, что он заменяет стандартный `--mui`.
    :::
    

## Рендеринг на стороне сервера <meta data-oversett="" data-original-text="Server-side rendering">

Поместите `getInitColorSchemeScript()` перед тегом `<Main />`, чтобы предотвратить мерцание SSR в темном режиме во время фазы гидратации.

### Next.js <meta data-oversett="" data-original-text="Next.js">

Добавьте следующий код в пользовательский [`pages/_document.js`](https://nextjs.org/docs/advanced-features/custom-document) файл:

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

Добавьте следующий код в пользовательский [`gatsby-ssr.js`](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-ssr/) файл:

```jsx
import React from 'react';
import { getInitColorSchemeScript } from '@mui/material/styles';

export function onRenderBody({ setPreBodyComponents }) {
  setPreBodyComponents([getInitColorSchemeScript()]);
}
```

## TypeScript <meta data-oversett="" data-original-text="TypeScript">

Тип переменных темы не включен по умолчанию. Вам необходимо импортировать модуль augmentation для включения типов:

```ts
// The import can be in any file that is included in your `tsconfig.json`
import type {} from '@mui/material/themeCssVarsAugmentation';
import { styled } from '@mui/material/styles';

const StyledComponent = styled('button')(({ theme }) => ({
  // ✅ typed-safe
  color: theme.vars.palette.primary.main,
}));
```
