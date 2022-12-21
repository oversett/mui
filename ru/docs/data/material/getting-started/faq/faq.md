

# Часто задаваемые вопросы <meta data-oversett="" data-original-text="Frequently Asked Questions">

<p class="description">Застряли на конкретной проблеме? Проверьте некоторые из этих распространенных проблем сначала в FAQ.</p>

Если вы все еще не можете найти то, что ищете, вы можете обратиться к нашей [странице поддержки](/material-ui/getting-started/support/).

## MUI - это круто. Как я могу поддержать проект? <meta data-oversett="" data-original-text="MUI is awesome. How can I support the project?">

Есть много способов поддержать MUI:

-   **Распространяйте информацию**. Проповедуйте MUI, разместив [ссылку на mui.com](https://mui.com/) на своем сайте, каждая обратная ссылка имеет значение. Следите за нами в [Twitter](https://twitter.com/MUI_hq), ставьте лайк и ретвитите важные новости. Или просто рассказывайте о нас своим друзьям.
-   **Дайте нам обратную связь**. Расскажите нам, что мы делаем хорошо или что мы можем улучшить. Пожалуйста, проголосуйте (👍) за те вопросы, в решении которых вы больше всего заинтересованы.
-   **Помогайте новым пользователям**. Вы можете отвечать на вопросы на[Stack Overflow](https://stackoverflow.com/questions/tagged/mui).
-   Внесите **изменения**.
    -   Редактируйте документацию. На каждой странице есть ссылка "EDIT THIS PAGE" в правом верхнем углу.
    -   Сообщайте об ошибках или отсутствующих функциях, [создавая проблему](https://github.com/mui/material-ui/issues/new).
    -   Просматривайте и комментируйте существующие [запросы](https://github.com/mui/material-ui/pulls) и [проблемы](https://github.com/mui/material-ui/issues).
    -   Помогите [перевести](https://translate.mui.com) документацию.
    -   [Улучшайте нашу документацию](https://github.com/mui/material-ui/tree/HEAD/docs), исправляйте ошибки или добавляйте функции, [отправляя запрос на](https://github.com/mui/material-ui/pulls) исправление.
-   **Поддержите нас финансово на [OpenCollective](https://opencollective.com/mui)**. Если вы используете MUI в коммерческом проекте и хотите поддержать его дальнейшее развитие, став спонсором, или в стороннем проекте или хобби и хотите стать беккером, вы можете сделать это через OpenCollective. Все пожертвованные средства управляются прозрачно, а спонсоры получают признание в README и на главной странице MUI.

## Почему элементы с фиксированным расположением перемещаются при открытии модала? <meta data-oversett="" data-original-text="Why do the fixed positioned elements move when a modal is opened?">

Прокрутка блокируется, как только открывается модальное окно. Это предотвращает взаимодействие с фоном, когда модальное окно должно быть единственным интерактивным содержимым. Однако удаление полосы прокрутки может привести к перемещению **элементов с фиксированным расположением**. В этой ситуации вы можете применить глобальное имя класса `.mui-fixed`, чтобы указать MUI на обработку этих элементов.

## Как я могу глобально отключить эффект ряби? <meta data-oversett="" data-original-text="How can I disable the ripple effect globally?">

Эффект пульсации исходит исключительно от компонента `BaseButton`. Вы можете отключить эффект пульсации глобально, указав следующее в вашей теме:

```js
import { createTheme } from '@mui/material';

const theme = createTheme({
  components: {
    // Name of the component ⚛️
    MuiButtonBase: {
      defaultProps: {
        // The props to apply
        disableRipple: true, // No more ripple, on the whole application 💣!
      },
    },
  },
});
```

## Как отключить переходы глобально? <meta data-oversett="" data-original-text="How can I disable transitions globally?">

MUI использует один и тот же помощник темы для создания всех переходов. Поэтому вы можете отключить все переходы, переопределив этот помощник в вашей теме:

```js
import { createTheme } from '@mui/material';

const theme = createTheme({
  transitions: {
    // So we have `transition: none;` everywhere
    create: () => 'none',
  },
});
```

Это может быть полезно для отключения переходов во время визуального тестирования или для улучшения производительности на низкопроизводительных устройствах.

Вы можете пойти еще дальше и отключить все переходы и эффекты анимации:

```js
import { createTheme } from '@mui/material';

const theme = createTheme({
  components: {
    // Name of the component ⚛️
    MuiCssBaseline: {
      styleOverrides: {
        '*, *::before, *::after': {
          transition: 'none !important',
          animation: 'none !important',
        },
      },
    },
  },
});
```

Обратите внимание, что для работы вышеописанного подхода требуется использование `CssBaseline`. Если вы решили не использовать его, вы все равно можете отключить переходы и анимацию, включив эти правила CSS:

```css
*,
*::before,
*::after {
  transition: 'none !important';
  animation: 'none !important';
}
```

## Должен ли я использовать Emotion для стилизации моего приложения? <meta data-oversett="" data-original-text="Do I have to use Emotion to style my app?">

Нет, это не обязательно. Но если вы используете стилизованный движок по умолчанию (`@mui/styled-engine`), то зависимость Emotion встроена, поэтому не требует дополнительных затрат на размер пакета.

Возможно, вы добавляете некоторые компоненты MUI в приложение, которое уже использует другое решение для стилизации, или уже знакомы с другим API и не хотите изучать новый? В этом случае перейдите к разделу "[Взаимодействие библиотек стилей](/material-ui/guides/interoperability/) ", где мы покажем, как просто изменить стиль компонентов MUI с помощью альтернативных библиотек стилей.

## Когда следует использовать inline-style против CSS? <meta data-oversett="" data-original-text="When should I use inline-style vs. CSS?">

Как правило, используйте inline-style только для динамических свойств стиля. Альтернатива CSS предоставляет больше преимуществ, таких как:

-   автопрефиксация
-   лучшая отладка
-   медиа-запросы
-   ключевые кадры

## Как использовать react-router? <meta data-oversett="" data-original-text="How do I use react-router?">

Мы подробно описываем [интеграцию со сторонними библиотеками маршрутизации](/material-ui/guides/routing/), такими как react-router, Gatsby или Next.js, в нашем руководстве.

## Как я могу получить доступ к элементу DOM? <meta data-oversett="" data-original-text="How can I access the DOM element?">

Все компоненты MUI, которые должны отображать что-то в DOM, передают свои ссылки на базовый компонент DOM. Это означает, что вы можете получить элементы DOM, читая ссылки, прикрепленные к компонентам MUI:

```jsx
// or a ref setter function
const ref = React.createRef();
// render
<Button ref={ref} />;
// usage
const element = ref.current;
```

Если вы не уверены, пересылает ли данный MUI-компонент свою ссылку, вы можете проверить документацию API в разделе "Реквизиты", например, [API Button](/material-ui/api/button/#props)включает следующее

:::info
Ссылка пересылается на корневой элемент.
:::

что указывает на то, что вы можете получить доступ к элементу DOM с помощью ссылки.

## У меня есть несколько экземпляров стилей на странице. <meta data-oversett="" data-original-text="I have several instances of styles on the page">

Если вы видите в консоли предупреждающее сообщение, подобное приведенному ниже, то, вероятно, на странице инициализировано несколько экземпляров `@mui/styles`.

:::warning
Похоже, что в этом приложении инициализировано несколько экземпляров `@mui/styles`. Это может вызвать проблемы с распространением тем, неработающие имена классов, проблемы со специфичностью и сделать ваше приложение больше без веской причины.
:::

### Возможные причины <meta data-oversett="" data-original-text="Possible reasons">

Есть несколько распространенных причин, по которым это может произойти:

-   У вас есть еще одна библиотека `@mui/styles` где-то в ваших зависимостях.
-   У вас монореповая структура проекта (например, lerna, yarn workspaces) и модуль `@mui/styles` является зависимостью более чем в одном пакете (этот пакет более или менее похож на предыдущий).
-   У вас есть несколько приложений, использующих `@mui/styles`, запущенных на одной странице (например, несколько точек входа в webpack загружены на одной странице).

### Дублированный модуль в node\_modules <meta data-oversett="" data-original-text="Duplicated module in node_modules">

Если вы думаете, что проблема может заключаться в дублировании модуля @mui/styles где-то в ваших зависимостях, есть несколько способов проверить это. Вы можете использовать команды `npm ls @mui/styles`, `yarn list @mui/styles` или `find -L ./node_modules | grep /@mui/styles/package.json` в папке вашего приложения.

Если ни одна из этих команд не выявила дублирование, попробуйте проанализировать ваш пакет на наличие нескольких экземпляров @mui/styles. Вы можете просто проверить источник вашего пакета или использовать такие инструменты, как [source-map-explorer](https://github.com/danvk/source-map-explorer) или [webpack-bundle-analyzer](https://github.com/webpack-contrib/webpack-bundle-analyzer).

Если вы определили, что дублирование является проблемой, с которой вы столкнулись, вы можете попробовать решить ее несколькими способами:

Если вы используете npm, вы можете попробовать запустить `npm dedupe`. Эта команда ищет локальные зависимости и пытается упростить структуру, перемещая общие зависимости дальше вверх по дереву.

Если вы используете webpack, вы можете изменить способ [разрешения](https://webpack.js.org/configuration/resolve/#resolve-modules) модуля @mui/styles. Вы можете переписать порядок по умолчанию, в котором webpack будет искать ваши зависимости, и сделать приоритет node\_modules вашего приложения выше, чем порядок разрешения node-модулей по умолчанию:

```diff
 resolve: {
+  alias: {
+    '@mui/styles': path.resolve(appFolder, 'node_modules', '@mui/styles'),
+  },
 },
```

### Использование с Lerna <meta data-oversett="" data-original-text="Usage with Lerna">

Одно из возможных решений для того, чтобы @mui/styles работал в монорепо Lerna с разными пакетами - это [поднять](https://github.com/lerna/lerna/blob/HEAD/doc/hoist.md) общие зависимости в корень файла вашего монорепо. Попробуйте запустить опцию bootstrap с флагом --hoist.

```sh
lerna bootstrap --hoist
```

В качестве альтернативы вы можете удалить @mui/styles из файла package.json и поднять его вручную в файл package.json верхнего уровня.

Пример файла package.json в корневой папке Lerna

```json
{
  "name": "my-monorepo",
  "devDependencies": {
    "lerna": "latest"
  },
  "dependencies": {
    "@mui/styles": "^4.0.0"
  },
  "scripts": {
    "bootstrap": "lerna bootstrap",
    "clean": "lerna clean",
    "start": "lerna run start",
    "build": "lerna run build"
  }
}
```

### Запуск нескольких приложений на одной странице <meta data-oversett="" data-original-text="Running multiple applications on one page">

Если на одной странице работает несколько приложений, подумайте об использовании одного модуля @mui/styles для всех них. Если вы используете webpack, вы можете использовать [CommonsChunkPlugin](https://webpack.js.org/plugins/commons-chunk-plugin/) для создания явного [чанка vendor](https://webpack.js.org/plugins/commons-chunk-plugin/#explicit-vendor-chunk), который будет содержать модуль @mui/styles:

```diff
  module.exports = {
    entry: {
+     vendor: ["@mui/styles"],
      app1: "./src/app.1.js",
      app2: "./src/app.2.js",
    },
    plugins: [
+     new webpack.optimize.CommonsChunkPlugin({
+       name: "vendor",
+       minChunks: Infinity,
+     }),
    ]
  }
```

## Мое приложение некорректно отображается на сервере <meta data-oversett="" data-original-text="My App doesn't render correctly on the server">

Если оно не работает, в 99% случаев это проблема конфигурации. Отсутствующее свойство, неправильный порядок вызова или отсутствующий компонент - серверный рендеринг строг к конфигурации.

Лучший способ выяснить, в чем дело, - сравнить свой проект с **уже работающим**. Проверьте [эталонную реализацию](/material-ui/guides/server-rendering/#reference-implementations), шаг за шагом.

## Почему цвета, которые я вижу, отличаются от того, что я вижу здесь? <meta data-oversett="" data-original-text="Why are the colors I am seeing different from what I see here?">

На сайте документации используется пользовательская тема. Следовательно, цветовая палитра отличается от темы по умолчанию, поставляемой MUI. Пожалуйста, обратитесь к [этой странице](/material-ui/customization/theming/), чтобы узнать о настройке темы.

## Почему компонент X требует узел DOM в реквизите вместо объекта ref? <meta data-oversett="" data-original-text="Why does component X require a DOM node in a prop instead of a ref object?">

Такие компоненты, как [Portal](/base/api/portal/#props) или [Popper](/material-ui/api/popper/#props) требуют DOM-узел в реквизите `container` или `anchorEl` соответственно. Кажется удобным просто передать объект ref в этих реквизитах и позволить MUI получить доступ к текущему значению. Это работает в простом сценарии:

```jsx
function App() {
  const container = React.useRef(null);

  return (
    <div className="App">
      <Portal container={container}>
        <span>portaled children</span>
      </Portal>
      <div ref={container} />
    </div>
  );
}
```

где `Portal` будет монтировать дочерние объекты в контейнер только тогда, когда `container.current` доступен. Вот наивная реализация Portal:

```jsx
function Portal({ children, container }) {
  const [node, setNode] = React.useState(null);

  React.useEffect(() => {
    setNode(container.current);
  }, [container]);

  if (node === null) {
    return null;
  }
  return ReactDOM.createPortal(children, node);
}
```

С помощью этой простой эвристики `Portal` может повторно отображаться после монтирования, потому что ссылки обновляются до запуска эффектов. Однако то, что ссылка обновляется, не означает, что она указывает на определенный экземпляр. Если ссылка прикреплена к компоненту переадресации ссылок, неясно, когда узел DOM будет доступен. В приведенном выше примере `Portal` запустит эффект один раз, но может не повторить рендеринг, потому что `ref.current` все еще `null`. Это особенно очевидно для React.lazy компонентов в Suspense. Приведенная выше реализация также может не учитывать изменение DOM-узла.

Вот почему нам требуется prop с фактическим узлом DOM, чтобы React мог позаботиться об определении того, когда `Portal` должен повторно отобразиться:

```jsx
function App() {
  const [container, setContainer] = React.useState(null);
  const handleRef = React.useCallback(
    (instance) => setContainer(instance),
    [setContainer],
  );

  return (
    <div className="App">
      <Portal container={container}>
        <span>Portaled</span>
      </Portal>
      <div ref={handleRef} />
    </div>
  );
}
```

## Для чего нужна зависимость clsx? <meta data-oversett="" data-original-text="What's the clsx dependency for?">

[clsx](https://github.com/lukeed/clsx) - это маленькая утилита для условного построения строк `className` из объекта, ключами которого являются строки класса, а значениями - булевы.

Вместо того чтобы написать:

```jsx
// let disabled = false, selected = true;

return (
  <div
    className={`MuiButton-root ${disabled ? 'Mui-disabled' : ''} ${
      selected ? 'Mui-selected' : ''
    }`}
  />
);
```

вы можете сделать:

```jsx
import clsx from 'clsx';

return (
  <div
    className={clsx('MuiButton-root', {
      'Mui-disabled': disabled,
      'Mui-selected': selected,
    })}
  />
);
```

## Я не могу использовать компоненты в качестве селекторов в утилите styled(). Что мне делать? <meta data-oversett="" data-original-text="I cannot use components as selectors in the styled() utility. What should I do?">

Если вы получаете ошибку: `TypeError: Cannot convert a Symbol value to a string`, посмотрите на страницу документации [styled()](/system/styled/#how-to-use-components-selector-api), где приведены инструкции по устранению этой ошибки.

## \[v4\] Почему мои компоненты не отображаются правильно в производственных сборках? <meta data-oversett="" data-original-text="[v4] Why aren't my components rendering correctly in production builds?">

Причина №1, по которой это происходит, скорее всего, связана с конфликтом имен классов, когда ваш код находится в производственной сборке. Для работы MUI значения `className` всех компонентов на странице должны генерироваться одним экземпляром [генератора имен классов](/system/styles/advanced/#class-names).

Чтобы исправить эту проблему, все компоненты на странице должны быть инициализированы таким образом, чтобы среди них всегда был только **один генератор имен классов**.

Вы можете случайно использовать два генератора имен классов в различных сценариях:

-   Вы случайно **установили** две версии MUI. Возможно, зависимость неправильно устанавливает MUI в качестве одноранговой зависимости.
-   Вы используете `StylesProvider` для **подмножества** вашего дерева React.
-   Вы используете бандлер, и он разделяет код таким образом, что создается несколько экземпляров генератора имен классов.

:::success
Если вы используете webpack с [SplitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/), попробуйте настроить [параметр`runtimeChunk` под `optimizations`.](https://webpack.js.org/configuration/optimization/#optimization-runtimechunk)
:::

В целом, от этой проблемы можно легко избавиться, обернув каждое MUI-приложение в [`StylesProvider`](/system/styles/api/#stylesprovider) компонентами в верхней части их деревьев компонентов **и используя единый генератор имен классов, общий для них**.

### \[v4\] CSS работает только при первой загрузке и пропадает <meta data-oversett="" data-original-text="[v4] CSS works only on first load and goes missing">

CSS генерируется только при первой загрузке страницы. Затем CSS пропадает на сервере при последующих запросах.

#### Действия, которые необходимо предпринять <meta data-oversett="" data-original-text="Action to Take">

Решение для стилизации полагается на кэш, _менеджер листов_, чтобы внедрять CSS только один раз для каждого типа компонента (если вы используете две кнопки, вам нужен CSS кнопки только один раз). Вам нужно создать **новый экземпляр `sheets` для каждого запроса**.

Пример исправления:

```diff
-// Create a sheets instance.
-const sheets = new ServerStyleSheets();

 function handleRender(req, res) {
+  // Create a sheets instance.
+  const sheets = new ServerStyleSheets();

   //…

   // Render the component to a string.
   const html = ReactDOMServer.renderToString(
```

### \[v4\] Несоответствие имени класса гидратации React <meta data-oversett="" data-original-text="[v4] React class name hydration mismatch">

:::warning
**⚠️ Предупреждение**

Проп className не совпадает.
:::

Имеет место несоответствие имени класса между клиентом и сервером. Это может сработать при первом запросе. Другим симптомом является изменение стиля между начальной загрузкой страницы и загрузкой клиентских скриптов.

#### Действия, которые необходимо предпринять <meta data-oversett="" data-original-text="Action to Take">

Значение имен классов основано на концепции [генератора имен классов](/system/styles/advanced/#class-names). Вся страница должна быть отрисована с помощью **одного генератора**. Этот генератор должен вести себя одинаково на сервере и на клиенте. Например:

-   Вы должны предоставлять новый генератор имен классов для каждого запроса. Но вы не должны совместно использовать `createGenerateClassName()` между разными запросами:
    
    Пример исправления:
    
    ```diff
    -// Create a new class name generator.
    -const generateClassName = createGenerateClassName();
    
     function handleRender(req, res) {
    +  // Create a new class name generator.
    +  const generateClassName = createGenerateClassName();
    
       //…
    
       // Render the component to a string.
       const html = ReactDOMServer.renderToString(
    ```
    
-   Вам необходимо убедиться, что на вашем клиенте и сервере используется **абсолютно одинаковая версия** MUI. Возможно, что несоответствие даже незначительных версий может вызвать проблемы со стилем. Чтобы проверить номера версий, запустите `npm list @mui/material` в среде, где вы собираете приложение, а также в среде развертывания.
    
    Вы также можете обеспечить одну и ту же версию в разных средах, указав конкретную версию MUI в зависимостях вашего package.json.
    
    _пример исправления (package.json):_
    
    ```diff
      "dependencies": {
        ...
    -   "@mui/material": "^4.0.0",
    +   "@mui/material": "4.0.0",
        ...
      },
    ```
    
-   Необходимо убедиться, что сервер и клиент используют одно и то же значение `process.env.NODE_ENV`.
