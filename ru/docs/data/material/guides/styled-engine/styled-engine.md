

# `@mui/styled-engine` <meta data-oversett="" data-original-text="@mui/styled-engine">

<p class="description">Настройка предпочитаемой библиотеки стилей.</p>

По умолчанию для генерации стилей CSS для компонентов MUI используется библиотека стилей [emotion](https://github.com/emotion-js/emotion). Все компоненты MUI полагаются на API `styled()` для внедрения CSS на страницу. Этот API поддерживается несколькими популярными библиотеками стилей, что позволяет переключаться между ними в MUI.

## Как переключиться на компоненты со стилями <meta data-oversett="" data-original-text="How to switch to styled-components">

:::error
Использование `styled-components` в качестве движка на данный момент не работает при использовании в SSR проектах. Причина в том, что `babel-plugin-styled-components` не правильно подхватывает использование утилиты `styled()` внутри пакетов `@mui`. Для более подробной информации, посмотрите этот [вопрос](https://github.com/mui/material-ui/issues/29742). Мы настоятельно рекомендуем использовать Emotion для SSR проектов.
:::

Если у вас уже установлены [styled-components](https://github.com/styled-components/styled-components), то можно использовать только его. В настоящее время доступны два пакета на выбор:

-   `@mui/styled-engine` - тонкая обертка вокруг API [Эмоции `styled()`](https://emotion.sh/docs/styled), с добавлением нескольких других необходимых утилит, таких как компонент `<GlobalStyles />`, помощники `css` и `keyframe` и т.д. Это используется по умолчанию.
-   `@mui/styled-engine-sc` - аналогичная обертка вокруг `styled-components`.

Эти два пакета реализуют один и тот же интерфейс, что позволяет заменить один на другой. По умолчанию `@mui/material` имеет `@mui/styled-engine` в качестве зависимости, но вы можете настроить свой пакет на замену его на `@mui/styled-engine-sc`.

### yarn <meta data-oversett="" data-original-text="yarn">

Если вы используете yarn, вы можете настроить его с помощью разрешения пакетов:

**package.json**

```diff
 {
   "dependencies": {
-    "@mui/styled-engine": "latest"
+    "@mui/styled-engine": "npm:@mui/styled-engine-sc@latest"
   },
+  "resolutions": {
+    "@mui/styled-engine": "npm:@mui/styled-engine-sc@latest"
+  },
 }
```

### npm <meta data-oversett="" data-original-text="npm">

Поскольку разрешения пакетов недоступны в npm в данный момент, вам нужно обновить конфигурацию вашего бандлера, чтобы добавить этот псевдоним. Вот пример того, как это можно сделать, если вы используете `webpack`:

**webpack.config.js**

```diff
 module.exports = {
   //...
+  resolve: {
+    alias: {
+      '@mui/styled-engine': '@mui/styled-engine-sc'
+    },
+  },
 };
```

Если вы используете TypeScript, вам также необходимо обновить TSConfig.

**tsconfig.json**

```diff
 {
   "compilerOptions": {
+    "paths": {
+      "@mui/styled-engine": ["./node_modules/@mui/styled-engine-sc"]
+    }
   },
 }
```

### Next.js <meta data-oversett="" data-original-text="Next.js">

**next.config.js**

```diff
+const withTM = require('next-transpile-modules')([
+  '@mui/material',
+  '@mui/system',
+  '@mui/icons-material', // If @mui/icons-material is being used
+]);

+module.exports = withTM({
 webpack: (config) => {
   config.resolve.alias = {
     ...config.resolve.alias,
+    '@mui/styled-engine': '@mui/styled-engine-sc',
    };
    return config;
  }
+});
```

### Готовые к использованию примеры <meta data-oversett="" data-original-text="Ready-to-use examples">

Если вы используете create-react-app, в примерах проектов есть готовый к использованию шаблон. Вы можете использовать эти примеры `styled-component` в качестве справочника:

-   [create-react-app](https://github.com/mui/material-ui/tree/master/examples/create-react-app-with-styled-components)
-   [create-react-app с TypeScript](https://github.com/mui/material-ui/tree/master/examples/create-react-app-with-styled-components-typescript)
-   [и многие другие](https://github.com/mui/material-ui/tree/master/examples)

:::warning
`@emotion/react` `@emotion/styled` и являются необязательными зависимостями от , поэтому вам необходимо установить их самостоятельно. Более подробную информацию см. в `styled-components` `@mui/material`[руководстве по установке](/material-ui/getting-started/installation/).
:::

Этот подход с заменой пакетов идентичен замене React на [Preact](https://github.com/preactjs/preact). Команда Preact задокументировала большое количество конфигураций установки. Если вы застряли с MUI + styled-components, не стесняйтесь проверить, как они решают проблему, так как вы, вероятно, сможете перенести решение.
