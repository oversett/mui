

# Серверный рендеринг <meta data-oversett="" data-original-text="Server rendering">

<p class="description">Наиболее распространенный случай использования рендеринга на стороне сервера - это обработка первоначального рендеринга, когда пользователь (или поисковая машина) впервые запрашивает ваше приложение.</p>

Когда сервер получает запрос, он преобразует необходимый компонент(ы) в строку HTML, а затем отправляет ее в качестве ответа клиенту. С этого момента клиент берет на себя обязанности по рендерингу.

## MUI на сервере <meta data-oversett="" data-original-text="MUI on the server">

MUI был разработан с нуля с ограничением рендеринга на сервере, но именно от вас зависит, насколько правильно он будет интегрирован. Важно обеспечить страницу необходимым CSS, иначе страница будет рендерить только HTML, а затем ждать, пока CSS будет внедрен клиентом, что приведет к мерцанию (FOUC). Чтобы внедрить стиль клиенту, нам необходимо:

1.  Создавайте свежий, новый [`emotion cache`](https://emotion.sh/docs/@emotion/cache) экземпляр при каждом запросе.
2.  Рендерить дерево React с помощью коллектора на стороне сервера.
3.  Извлечь CSS.
4.  Передать CSS клиенту.

На стороне клиента CSS будет внедрен второй раз, прежде чем удалить внедренный на стороне сервера CSS.

## Настройка <meta data-oversett="" data-original-text="Setting up">

В следующем рецепте мы рассмотрим, как настроить рендеринг на стороне сервера.

### Тема <meta data-oversett="" data-original-text="The theme">

Создайте тему, которая будет общей для клиента и сервера:

`theme.js`

```js
import { createTheme } from '@mui/material/styles';
import { red } from '@mui/material/colors';

// Create a theme instance.
const theme = createTheme({
  palette: {
    primary: {
      main: '#556cd6',
    },
    secondary: {
      main: '#19857b',
    },
    error: {
      main: red.A400,
    },
  },
});

export default theme;
```

### Серверная сторона <meta data-oversett="" data-original-text="The server-side">

Ниже описано, как будет выглядеть сторона сервера. Мы собираемся установить [промежуточное ПО Express](https://expressjs.com/en/guide/using-middleware.html) с помощью [app.use](https://expressjs.com/en/api.html) для обработки всех запросов, поступающих на сервер. Если вы не знакомы с Express или промежуточным ПО, знайте, что функция `handleRender` будет вызываться каждый раз, когда сервер получает запрос.

`server.js`

```js
import express from 'express';

// We are going to fill these out in the sections to follow.
function renderFullPage(html, css) {
  /* ... */
}

function handleRender(req, res) {
  /* ... */
}

const app = express();

// This is fired every time the server-side receives a request.
app.use(handleRender);

const port = 3000;
app.listen(port);
```

### Обработка запроса <meta data-oversett="" data-original-text="Handling the request">

Первое, что нам нужно сделать при каждом запросе, это создать новый `emotion cache`.

При рендеринге мы обернем `App`, корневой компонент, внутрь компонента [`CacheProvider`](https://emotion.sh/docs/cache-provider) и [`ThemeProvider`](/system/styles/api/#themeprovider) чтобы сделать конфигурацию стиля и `theme` доступной для всех компонентов в дереве компонентов.

Ключевым шагом в рендеринге на стороне сервера является рендеринг исходного HTML компонента **перед** отправкой его на сторону клиента. Для этого мы используем [ReactDOMServer.renderToString()](https://reactjs.org/docs/react-dom-server.html).

MUI использует Emotion в качестве движка стилей по умолчанию. Нам нужно извлечь стили из экземпляра Emotion. Для этого нам нужно использовать одну и ту же конфигурацию кэша для клиента и сервера:

`createEmotionCache.js`

```js
import createCache from '@emotion/cache';

export default function createEmotionCache() {
  return createCache({ key: 'css' });
}
```

Для этого мы создаем новый экземпляр кэша Emotion и используем его для извлечения критических стилей для html.

Мы увидим, как это передается в функции `renderFullPage`.

```jsx
import express from 'express';
import * as React from 'react';
import ReactDOMServer from 'react-dom/server';
import CssBaseline from '@mui/material/CssBaseline';
import { ThemeProvider } from '@mui/material/styles';
import { CacheProvider } from '@emotion/react';
import createEmotionServer from '@emotion/server/create-instance';
import App from './App';
import theme from './theme';
import createEmotionCache from './createEmotionCache';

function handleRender(req, res) {
  const cache = createEmotionCache();
  const { extractCriticalToChunks, constructStyleTagsFromChunks } =
    createEmotionServer(cache);

  // Render the component to a string.
  const html = ReactDOMServer.renderToString(
    <CacheProvider value={cache}>
      <ThemeProvider theme={theme}>
        {/* CssBaseline kickstart an elegant, consistent, and simple baseline to build upon. */}
        <CssBaseline />
        <App />
      </ThemeProvider>
    </CacheProvider>,
  );

  // Grab the CSS from emotion
  const emotionChunks = extractCriticalToChunks(html);
  const emotionCss = constructStyleTagsFromChunks(emotionChunks);

  // Send the rendered page back to the client.
  res.send(renderFullPage(html, emotionCss));
}

const app = express();

app.use('/build', express.static('build'));

// This is fired every time the server-side receives a request.
app.use(handleRender);

const port = 3000;
app.listen(port);
```

### Вставка HTML и CSS начального компонента <meta data-oversett="" data-original-text="Inject initial component HTML and CSS">

Последним шагом на стороне сервера является внедрение HTML и CSS начального компонента в шаблон для отображения на стороне клиента.

```js
function renderFullPage(html, css) {
  return `
    <!DOCTYPE html>
    <html>
      <head>
        <title>My page</title>
        ${css}
        <meta name="viewport" content="initial-scale=1, width=device-width" />
        <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" />
      </head>
      <body>
        <div id="root">${html}</div>
      </body>
    </html>
  `;
}
```

### Клиентская сторона <meta data-oversett="" data-original-text="The client-side">

Клиентская сторона проста. Все, что нам нужно сделать, это использовать ту же конфигурацию кэша, что и на серверной стороне. Давайте посмотрим на файл клиента:

`client.js`

```jsx
import * as React from 'react';
import ReactDOM from 'react-dom';
import CssBaseline from '@mui/material/CssBaseline';
import { ThemeProvider } from '@mui/material/styles';
import { CacheProvider } from '@emotion/react';
import App from './App';
import theme from './theme';
import createEmotionCache from './createEmotionCache';

const cache = createEmotionCache();

function Main() {
  return (
    <CacheProvider value={cache}>
      <ThemeProvider theme={theme}>
        {/* CssBaseline kickstart an elegant, consistent, and simple baseline to build upon. */}
        <CssBaseline />
        <App />
      </ThemeProvider>
    </CacheProvider>
  );
}

ReactDOM.hydrate(<Main />, document.querySelector('#root'));
```

## Эталонные реализации <meta data-oversett="" data-original-text="Reference implementations">

Мы разместили различные эталонные реализации, которые вы можете найти в [репозитории GitHub](https://github.com/mui/material-ui) в папке [`/examples`](https://github.com/mui/material-ui/tree/HEAD/examples) папка:

-   [Эталонная реализация этого руководства](https://github.com/mui/material-ui/tree/HEAD/examples/ssr)
-   [Gatsby](https://github.com/mui/material-ui/tree/HEAD/examples/gatsby)
-   [Next.js](https://github.com/mui/material-ui/tree/HEAD/examples/nextjs)[(версия TypeScript](https://github.com/mui/material-ui/tree/HEAD/examples/nextjs-with-typescript))

## Устранение неполадок <meta data-oversett="" data-original-text="Troubleshooting">

Ознакомьтесь с ответом на часто задаваемые вопросы: [Мое приложение некорректно отображается на сервере](/material-ui/getting-started/faq/#my-app-doesnt-render-correctly-on-the-server).
