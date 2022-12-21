---
product: material-ui
title: Media queries in React for responsive design
githubLabel: 'hook: useMediaQuery'
---

# useMediaQuery <meta data-oversett="" data-original-text="useMediaQuery">

<p class="description">Это крючок медиазапроса CSS для React. Он прослушивает совпадения с медиа-запросом CSS. Он позволяет отрисовывать компоненты в зависимости от того, соответствует запрос или нет.</p>

Некоторые ключевые особенности:

-   ⚛️ Имеет идиоматический React API.
-   🚀 Он перформативен, он наблюдает за документом, чтобы определить, когда его медиа-запросы изменяются, вместо того, чтобы периодически опрашивать значения.
-   📦 [1 kB gzipped](/size-snapshot/).
-   🤖 Поддерживает рендеринг на стороне сервера.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Базовый медиазапрос <meta data-oversett="" data-original-text="Basic media query">

Вы должны указать медиа-запрос в первом аргументе хука. Строка медиа-запроса может быть любым допустимым CSS медиа-запросом, например. [`'(prefers-color-scheme: dark)'`](/material-ui/customization/dark-mode/#system-preference).

{{"demo": "SimpleMediaQuery.js", "defaultCodeOpen": true}}

⚠️ Вы не можете использовать `'print'` из-за ограничений браузеров, например, [Firefox](https://bugzilla.mozilla.org/show_bug.cgi?id=774398).

## Использование помощников точки останова MUI <meta data-oversett="" data-original-text="Using MUI's breakpoint helpers">

Вы можете использовать [помощники точки останова](/material-ui/customization/breakpoints/) MUI следующим образом:

```jsx
import { useTheme } from '@mui/material/styles';
import useMediaQuery from '@mui/material/useMediaQuery';

function MyComponent() {
  const theme = useTheme();
  const matches = useMediaQuery(theme.breakpoints.up('sm'));

  return <span>{`theme.breakpoints.up('sm') matches: ${matches}`}</span>;
}
```

{{"demo": "ThemeHelper.js", "defaultCodeOpen": false}}

В качестве альтернативы вы можете использовать функцию обратного вызова, принимая тему в качестве первого аргумента:

```jsx
import useMediaQuery from '@mui/material/useMediaQuery';

function MyComponent() {
  const matches = useMediaQuery((theme) => theme.breakpoints.up('sm'));

  return <span>{`theme.breakpoints.up('sm') matches: ${matches}`}</span>;
}
```

⚠️ Поддержка темы **по умолчанию отсутствует**, ее необходимо внедрить в родительский провайдер темы.

## Использование синтаксиса JavaScript <meta data-oversett="" data-original-text="Using JavaScript syntax">

Вы можете использовать [json2mq](https://github.com/akiran/json2mq) для генерации строки медиа-запроса из объекта JavaScript.

{{"demo": "JavaScriptMedia.js", "defaultCodeOpen": true}}

## Тестирование <meta data-oversett="" data-original-text="Testing">

Вам необходима реализация [matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) в вашем тестовом окружении.

Например, [jsdom пока не поддерживает ее](https://jestjs.io/docs/manual-mocks#mocking-methods-which-are-not-implemented-in-jsdom). Рекомендуется использовать [css-mediaquery](https://github.com/ericf/css-mediaquery) для его эмуляции.

```js
import mediaQuery from 'css-mediaquery';

function createMatchMedia(width) {
  return (query) => ({
    matches: mediaQuery.match(query, {
      width,
    }),
    addListener: () => {},
    removeListener: () => {},
  });
}

describe('MyTests', () => {
  beforeAll(() => {
    window.matchMedia = createMatchMedia(window.innerWidth);
  });
});
```

## Рендеринг только на стороне клиента <meta data-oversett="" data-original-text="Client-side only rendering">

Чтобы выполнить гидратацию на стороне сервера, хук должен рендерить дважды. Первый раз с `false`, значением сервера, и второй раз с разрешенным значением. Этот цикл рендеринга с двойным проходом имеет недостаток. Он медленнее. Вы можете установить опцию `noSsr` на `true`, если вы делаете рендеринг **только на стороне клиента**.

```js
const matches = useMediaQuery('(min-width:600px)', { noSsr: true });
```

Или можно включить его глобально в теме:

```js
const theme = createTheme({
  components: {
    MuiUseMediaQuery: {
      defaultProps: {
        noSsr: true,
      },
    },
  },
});
```

## Рендеринг на стороне сервера <meta data-oversett="" data-original-text="Server-side rendering">

:::warning
Рендеринг на стороне сервера и клиентские медиа-запросы в корне противоречат друг другу. Будьте внимательны к компромиссу. Поддержка может быть только частичной.
:::

Попробуйте сначала полагаться на клиентские медиазапросы CSS. Например, вы можете использовать:

-   [`<Box display>`](/system/display/#hiding-elements)
-   [`themes.breakpoints.up(x)`](/material-ui/customization/breakpoints/#css-media-queries)
-   или [`sx prop`](/system/getting-started/the-sx-prop/)

Если ни одна из вышеперечисленных альтернатив не подходит, вы можете продолжить чтение этого раздела документации.

Во-первых, вам нужно угадать характеристики клиентского запроса от сервера. У вас есть выбор между использованием:

-   **Агент пользователя**. Разобрать строку агента пользователя клиента для извлечения информации. Рекомендуется использовать [ua-parser-js](https://github.com/faisalman/ua-parser-js) для разбора агента пользователя.
-   **Подсказки клиента**. Считывать подсказки, которые клиент посылает серверу. Имейте в виду, что эта функция [поддерживается не везде](https://caniuse.com/#search=client%20hint).

Наконец, вам нужно предоставить реализацию [matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) на `useMediaQuery` с угаданными ранее характеристиками. Рекомендуется использовать [css-mediaquery](https://github.com/ericf/css-mediaquery) для эмуляции matchMedia.

Например, на стороне сервера:

```js
import ReactDOMServer from 'react-dom/server';
import parser from 'ua-parser-js';
import mediaQuery from 'css-mediaquery';
import { createTheme, ThemeProvider } from '@mui/material/styles';

function handleRender(req, res) {
  const deviceType = parser(req.headers['user-agent']).device.type || 'desktop';
  const ssrMatchMedia = (query) => ({
    matches: mediaQuery.match(query, {
      // The estimated CSS width of the browser.
      width: deviceType === 'mobile' ? '0px' : '1024px',
    }),
  });

  const theme = createTheme({
    components: {
      // Change the default options of useMediaQuery
      MuiUseMediaQuery: {
        defaultProps: {
          ssrMatchMedia,
        },
      },
    },
  });

  const html = ReactDOMServer.renderToString(
    <ThemeProvider theme={theme}>
      <App />
    </ThemeProvider>,
  );

  // …
}
```

{{"demo": "ServerSide.js", "defaultCodeOpen": false}}

Убедитесь, что вы предоставили такую же пользовательскую реализацию matchMedia на стороне клиента, чтобы гарантировать совпадение гидратации.

## Переход с `withWidth()` <meta data-oversett="" data-original-text="Migrating from withWidth()">

Компонент высшего порядка `withWidth()` вводит ширину экрана страницы. Вы можете воспроизвести то же поведение с помощью хука `useWidth`:

{{"demo": "UseWidth.js"}}

## API <meta data-oversett="" data-original-text="API">

### `useMediaQuery(query, [options]) => matches` <meta data-oversett="" data-original-text="useMediaQuery(query, [options]) => matches">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `query` _(string_ | _func_): Строка, представляющая медиа-запрос для обработки, или функция обратного вызова, принимающая тему (в контексте), которая возвращает строку.
2.  `options` _(object_ \[необязательно\]):

-   `options.defaultMatches` _(bool_ \[optional\]): Поскольку `window.matchMedia()` недоступен на сервере, при первом монтировании мы возвращаем соответствие по умолчанию. Значение по умолчанию - `false`.
-   `options.matchMedia` _(func_ \[необязательно\]): Вы можете предоставить свою собственную реализацию _matchMedia_. Это может быть использовано для обработки окна содержимого iframe.
-   `options.noSsr` _(bool_ \[необязательно\]): По умолчанию `false`. Чтобы выполнить гидратацию на стороне сервера, хук должен выполнить рендеринг дважды. Первый раз с `false`, значением сервера, и второй раз с разрешенным значением. Этот цикл рендеринга с двойным проходом имеет недостаток. Он медленнее. Вы можете установить этот параметр на `true`, если вы делаете рендеринг **только на стороне клиента**.
-   `options.ssrMatchMedia` _(func_ \[необязательно\]): Вы можете предоставить свою собственную реализацию _matchMedia_ в [контексте рендеринга на стороне сервера](#server-side-rendering).

Примечание: Вы можете изменить параметры по умолчанию, используя [`default props`](/material-ui/customization/theme-components/#default-props) функцию темы с помощью ключа `MuiUseMediaQuery`.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`matches`: Возвращает `true`, если документ в данный момент соответствует медиа-запросу, и `false`, если не соответствует.

#### Примеры <meta data-oversett="" data-original-text="Examples">

```jsx
import * as React from 'react';
import useMediaQuery from '@mui/material/useMediaQuery';

export default function SimpleMediaQuery() {
  const matches = useMediaQuery('(min-width:600px)');

  return <span>{`(min-width:600px) matches: ${matches}`}</span>;
}
```
