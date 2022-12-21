

# Устранение неполадок <meta data-oversett="" data-original-text="Troubleshooting">

<p class="description">В этом документе описаны известные проблемы и общие проблемы, возникающие при переходе с Material UI v4 на v5.</p>

## Миграция Material UI v5 <meta data-oversett="" data-original-text="Material UI v5 migration">

1.  [Начало работы](/material-ui/migration/migration-v4/)
2.  [Первая часть: стиль и тема](/material-ui/migration/v5-style-changes/)
3.  [Внесение изменений, часть вторая: компоненты](/material-ui/migration/v5-component-changes/)
4.  [Миграция с JSS](/material-ui/migration/migrating-from-jss/)
5.  Устранение неполадок 👈 _вы здесь_

## Нарушение стилей после перехода на v5 <meta data-oversett="" data-original-text="Styles broken after migrating to v5">

Есть две причины, по которым стили компонентов могут быть нарушены после выполнения всех шагов процесса миграции.

Во-первых, проверьте, правильно ли вы настроили `StyledEngineProvider`, как показано в разделе " [Библиотека стилей](/material-ui/migration/v5-style-changes/#style-library) ".

Если `StyledEngineProvider` уже используется в верхней части вашего приложения, а стили все еще не работают, возможно, в вашем приложении все еще присутствует `@material-ui/core`.

Это может быть вызвано другими зависимостями в приложении, которые все еще полагаются на Material UI v4.

Чтобы проверить это, запустите `npm ls @material-ui/core` (или `yarn why @material-ui/core`). Если ваш проект содержит такие зависимости, вы увидите список, который выглядит примерно так:

```sh
$ npm ls @material-ui/core
project@0.1.0 /path/to/project
└─┬  @mui/x-data-grid@4.0.0
  └── @material-ui/core@4.12.3
```

Приведенный выше результат показывает, что `@material-ui/core` является зависимостью от `@mui/x-data-grid`.

В данном конкретном примере вам нужно увеличить версию `@mui/x-data-grid` до [v5](https://www.npmjs.com/package/@mui/x-data-grid), чтобы она зависела от `@mui/material`.

## Storybook и Emotion <meta data-oversett="" data-original-text="Storybook and Emotion">

Если ваш проект использует Storybook v6.x, вам нужно обновить конфигурацию webpack `.storybook/main.js`, чтобы использовать последнюю версию Emotion:

```js
// .storybook/main.js

const path = require('path');
const toPath = (filePath) => path.join(process.cwd(), filePath);

module.exports = {
  webpackFinal: async (config) => {
    return {
      ...config,
      resolve: {
        ...config.resolve,
        alias: {
          ...config.resolve.alias,
          '@emotion/core': toPath('node_modules/@emotion/react'),
          'emotion-theming': toPath('node_modules/@emotion/react'),
        },
      },
    };
  },
};
```

Затем обновите `.storybook/preview.js`, чтобы вкладка "Документы" Storybook не отображала пустую страницу:

```js
// .storybook/preview.js

import { ThemeProvider, createTheme } from '@mui/material/styles';
import { ThemeProvider as Emotion10ThemeProvider } from 'emotion-theming';

const defaultTheme = createTheme(); // or your custom theme

const withThemeProvider = (Story, context) => {
  return (
    <Emotion10ThemeProvider theme={defaultTheme}>
      <ThemeProvider theme={defaultTheme}>
        <Story {...context} />
      </ThemeProvider>
    </Emotion10ThemeProvider>
  );
};

export const decorators = [withThemeProvider];

// ...other storybook exports
```

:::info
Это решение было протестировано на следующих версиях:

```json
{
  "@storybook/react": "6.3.8",
  "@storybook/addon-docs": "6.3.8",
  "@emotion/react": "11.4.1",
  "@emotion/styled": "11.3.0",
  "@mui/material": "5.0.2"
}
```

Обратите внимание, что это обходной путь, который может не подойти для вашей ситуации, если вы используете другие версии.

Для получения более подробной информации ознакомьтесь с этими проблемами на GitHub:

-   [https://github.com/storybookjs/storybook/issues/16099](https://github.com/storybookjs/storybook/issues/16099)
-   [https://github.com/mui/material-ui/issues/24282#issuecomment-796755133](https://github.com/mui/material-ui/issues/24282#issuecomment-796755133)
:::

## Невозможно прочитать свойство scrollTop равное null <meta data-oversett="" data-original-text="Cannot read property scrollTop of null">

Эта ошибка возникает в компонентах `Fade`, `Grow`, `Slide`, `Zoom` из-за отсутствия узла DOM.

Убедитесь, что дочерние компоненты передают `ref` в DOM для пользовательских компонентов:

```jsx
// Ex. 1-1 ❌ This will cause an error because the Fragment is not a DOM node:
<Fade in>
  <React.Fragment>
    <CustomComponent />
  </React.Fragment>
</Fade>
```

```jsx
// Ex. 1-2 ✅ Add a DOM node such as this div:
<Fade in>
  <div>
    <CustomComponent />
  </div>
</Fade>
```

```jsx
// Ex. 2-1 ❌ This will cause an error because `CustomComponent` does not forward `ref` to the DOM:
function CustomComponent() {
  return <div>...</div>;
}

<Fade in>
  <CustomComponent />
</Fade>;
```

```jsx
// Ex. 2-2 ✅ Add `React.forwardRef` to forward `ref` to the DOM:
const CustomComponent = React.forwardRef(function CustomComponent(props, ref) {
  return (
    <div ref={ref}>
      ...
    </div>
  )
})

<Fade in>
  <CustomComponent />
</Fade>
```

Для более подробной информации ознакомьтесь с [этой проблемой](https://github.com/mui/material-ui/issues/27154) на GitHub.

## \[Типы\] Свойство "palette", "spacing" не существует для типа 'DefaultTheme'. <meta data-oversett="" data-original-text="[Types] Property &quot;palette&quot;, &quot;spacing&quot; does not exist on type 'DefaultTheme'">

Эта ошибка возникает потому, что `makeStyles` теперь экспортируется из пакета `@mui/styles`, который не знает о `Theme` в основном пакете.

Чтобы исправить это, необходимо дополнить `DefaultTheme` (пустой объект) в `@mui/styles` модулем `Theme` из ядра.

Подробнее о дополнении модулей читайте в [официальной документации по TypeScript](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation).

### TypeScript <meta data-oversett="" data-original-text="TypeScript">

Добавьте этот фрагмент в файл вашей темы:

```ts
// it could be your App.tsx file or theme file that is included in your tsconfig.json
import { Theme } from '@mui/material/styles';

declare module '@mui/styles/defaultTheme' {
  // eslint-disable-next-line @typescript-eslint/no-empty-interface (remove this line if you don't have the rule enabled)
  interface DefaultTheme extends Theme {}
}
```

### JavaScript <meta data-oversett="" data-original-text="JavaScript">

Если вы используете IDE, например VSCode, которая может определять типы из файла `d.ts`, создайте `index.d.ts` в папке `src` и добавьте следующие строки кода:

```js
// index.d.ts
declare module '@mui/private-theming' {
  import type { Theme } from '@mui/material/styles';

  interface DefaultTheme extends Theme {}
}
```

## \[Jest\] SyntaxError: Unexpected token 'export' <meta data-oversett="" data-original-text="[Jest] SyntaxError: Unexpected token 'export'">

`@mui/material/colors/red` считается приватным с версии 1.0.0. Чтобы исправить эту ошибку, вы должны заменить импорт. Для более подробной информации смотрите [эту проблему на GitHub](https://github.com/mui/material-ui/issues/27296).

Мы рекомендуем использовать этот кодмод для исправления всех импортов в вашем проекте:

```sh
npx @mui/codemod v5.0.0/optimal-imports <path>
```

Вы можете исправить его вручную следующим образом:

```diff
-import red from '@mui/material/colors/red';
+import { red } from '@mui/material/colors';
```

## makeStyles - TypeError: Cannot read property 'drawer' of undefined <meta data-oversett="" data-original-text="makeStyles - TypeError: Cannot read property 'drawer' of undefined">

Эта ошибка возникает при вызове `useStyles` или `withStyles` вне области видимости `<ThemeProvider>`, как в следующем примере:

```js
import * as React from 'react';
import { ThemeProvider, createTheme } from '@mui/material/styles';
import makeStyles from '@mui/styles/makeStyles';
import Card from '@mui/material/Card';
import CssBaseline from '@mui/material/CssBaseline';

const useStyles = makeStyles((theme) => ({
  root: {
    display: 'flex',
    backgroundColor: theme.palette.primary.main,
    color: theme.palette.common.white,
  },
}));

const theme = createTheme();

function App() {
  const classes = useStyles(); // ❌ called outside of ThemeProvider
  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <Card className={classes.root}>...</Card>
    </ThemeProvider>
  );
}

export default App;
```

Вы можете исправить это, переместив `useStyles` внутрь другого компонента так, чтобы он вызывался под `<ThemeProvider>`:

```js
// ...imports

function AppContent(props) {
  const classes = useStyles(); // ✅ This is safe because it is called inside ThemeProvider
  return <Card className={classes.root}>...</Card>;
}

function App(props) {
  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <AppContent {...props} />
    </ThemeProvider>
  );
}

export default App;
```

## TypeError: Cannot read properties of undefined (reading 'pxToRem') <meta data-oversett="" data-original-text="TypeError: Cannot read properties of undefined (reading 'pxToRem')">

Эта ошибка возникает при попытке получить доступ к пустой теме.

Убедитесь, что вы решили следующие проблемы:

1.  `styled` следует импортировать только из `@mui/material/styles` (если вы не используете автономный `@mui/system`):

```js
import { styled } from '@mui/material/styles';
```

2.  `useStyles` не может быть вызвана вне `<ThemeProvider>`. Чтобы исправить эту проблему, следуйте [инструкциям в этом разделе](#makestyles-typeerror-cannot-read-property-drawer-of-undefined).

Для получения более подробной информации см. [этот вопрос на GitHub](https://github.com/mui/material-ui/issues/28496).

## Все еще есть проблемы? <meta data-oversett="" data-original-text="Still having problems?">

Если вы столкнулись с проблемой, не описанной здесь, пожалуйста, [создайте проблему на GitHub](https://github.com/mui/material-ui/issues/new?assignees=&labels=status%3A+needs+triage&template=1.bug.yml) с таким форматом заголовка: **\[Migration\] Краткое описание вашей проблемы**.
