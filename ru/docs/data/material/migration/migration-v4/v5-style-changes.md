

# Ломающие изменения в v5, часть первая: стили и темы <meta data-oversett="" data-original-text="Breaking changes in v5, part one: styles and themes">

<p class="description">Это справочное руководство по всем изменениям, внесенным в Material v5, и по тому, как с ними обращаться при переходе с v4. В этой части рассматриваются изменения в стилях и темах.</p>

## Миграция Material UI v5 <meta data-oversett="" data-original-text="Material UI v5 migration">

1.  [Начало работы](/material-ui/migration/migration-v4/)
2.  Ломающие изменения, часть первая: стиль и тема 👈 _Вы здесь_
3.  [Изменения во второй части: компоненты](/material-ui/migration/v5-component-changes/)
4.  [Миграция с JSS](/material-ui/migration/migrating-from-jss/)
5.  [Устранение неполадок](/material-ui/migration/troubleshooting/)

## Ломающие изменения, часть первая <meta data-oversett="" data-original-text="Breaking changes, part one">

В Material UI v5 внесен ряд изменений по сравнению с v4. Многие из этих изменений могут быть устранены автоматически с помощью [кодовых модулей](/material-ui/migration/migration-v4/#run-codemods), описанных в [главном руководстве по миграции](/material-ui/migration/migration-v4/).

В следующем документе перечислены все изменения, связанные со стилями и темами в v5, и способы их устранения.

После того, как вы закончите с этим документом, перейдите ко [второй части "Нарушающие изменения в v5: компоненты](/material-ui/migration/v5-component-changes/) ", чтобы продолжить процесс миграции.

:::warning
Изменения, которые обрабатываются кодмодами, обозначаются ✅ эмодзи в оглавлении в правой части экрана.

Если вы уже следовали инструкциям в основном руководстве по миграции и запустили кодмоды, то вам не нужно предпринимать никаких дополнительных действий по этим пунктам.

Все остальные изменения должны быть выполнены вручную.
:::

## Перенос стилевых переопределений темы в Emotion <meta data-oversett="" data-original-text="Migrate theme styleOverrides to Emotion">

Хотя ваши переопределения стилей, определенные в теме, могут частично работать, есть важное различие в том, как стилизуются вложенные элементы.

Синтаксис `$` (локальная ссылка на правило), используемый в JSS, не будет работать в Emotion. Вам нужно заменить эти селекторы на действительные селекторы классов.

### Замените имена классов состояния <meta data-oversett="" data-original-text="Replace state class names">

```diff
 const theme = createTheme({
   components: {
     MuiOutlinedInput: {
       styleOverrides: {
         root: {
-          '&$focused': {
+          '&.Mui-focused': {
             borderWidth: 1,
           }
         }
       }
     }
   }
 });
```

### Замените селекторы вложенных классов именами глобальных классов <meta data-oversett="" data-original-text="Replace nested classes selectors with global class names">

```diff
 const theme = createTheme({
   components: {
     MuiOutlinedInput: {
       styleOverrides: {
         root: {
-          '& $notchedOutline': {
+          '& .MuiOutlinedInput-notchedOutline': {
             borderWidth: 1,
           }
         }
       }
     }
   }
 });
```

:::info
Для каждого компонента мы экспортируем константу `[component]Classes`, которая содержит все вложенные классы для этого компонента.

Вы можете полагаться на это вместо жесткого кодирования классов.
:::

```diff
+import { outlinedInputClasses } from '@mui/material/OutlinedInput';

 const theme = createTheme({
   components: {
     MuiOutlinedInput: {
       styleOverrides: {
         root: {
-          '& $notchedOutline': {
+          [`& .${outlinedInputClasses.notchedOutline}`]: {
             borderWidth: 1,
           }
         }
       }
     }
   }
 });
```

Посмотрите на полный [список](/material-ui/customization/how-to-customize/#state-classes) доступных [глобальных имен классов состояний](/material-ui/customization/how-to-customize/#state-classes).

## ref <meta data-oversett="" data-original-text="ref">

### Рефакторинг компонентов классов без переадресации по ссылке <meta data-oversett="" data-original-text="Refactor non-ref-forwarding class components">

Поддержка компонентов классов без переадресации в реквизите `component` или в непосредственном `children` была прекращена.

Если вы используете `unstable_createStrictModeTheme` или не видели никаких предупреждений, связанных с `findDOMNode` в `React.StrictMode`, то вам не нужно предпринимать никаких дальнейших действий.

В противном случае ознакомьтесь с разделом [Caveat with refs](/material-ui/guides/composition/#caveat-with-refs) в руководстве по композиции, чтобы узнать, как осуществить миграцию. Это изменение затрагивает почти все компоненты, где вы используете реквизит `component` или передаете `children` компонентам, которые требуют, чтобы `children` был элементом (например, `<MenuList><CustomMenuItem /></MenuList>`).

### Исправление специфичности типов ссылок <meta data-oversett="" data-original-text="Fix ref type specificity">

Для некоторых компонентов вы можете получить ошибку типа при передаче `ref`. Чтобы избежать ошибки, вы должны использовать конкретный тип элемента. Например, `Card` ожидает, что тип `ref` будет `HTMLDivElement`, а `ListItem` ожидает, что его тип `ref` будет `HTMLLIElement`.

Вот пример:

```diff
 import * as React from 'react';
 import Card from '@mui/material/Card';
 import ListItem from '@mui/material/ListItem';

 export default function SpecificRefType() {
-  const cardRef = React.useRef<HTMLElement>(null);
+  const cardRef = React.useRef<HTMLDivElement>(null);

-  const listItemRef = React.useRef<HTMLElement>(null);
+  const listItemRef = React.useRef<HTMLLIElement>(null);
   return (
     <div>
       <Card ref={cardRef}></Card>
       <ListItem ref={listItemRef}></ListItem>
     </div>
   );
 }
```

Вот конкретные типы элементов, которые ожидает каждый компонент:

#### @mui/material <meta data-oversett="" data-original-text="@mui/material">

-   [Аккордеон](/material-ui/api/accordion/) - `HTMLDivElement`
-   [Оповещение](/material-ui/api/alert/) - `HTMLDivElement`
-   [Аватар](/material-ui/api/avatar/) - `HTMLDivElement`
-   [ButtonGroup](/material-ui/api/button-group/) - `HTMLDivElement`
-   [Карточка](/material-ui/api/card/) - `HTMLDivElement`
-   [Диалог](/material-ui/api/dialog/) - `HTMLDivElement`
-   [ImageList](/material-ui/api/image-list/) - `HTMLUListElement`
-   [Список](/material-ui/api/list/) - `HTMLUListElement`
-   [Tab](/material-ui/api/tab/) - `HTMLDivElement`
-   [Вкладки](/material-ui/api/tabs/) - `HTMLDivElement`
-   [ToggleButton](/material-ui/api/toggle-button/) - `HTMLButtonElement`

#### @mui/lab <meta data-oversett="" data-original-text="@mui/lab">

-   [Временная шкала](/material-ui/api/timeline/) - `HTMLUListElement`

## Библиотека стилей <meta data-oversett="" data-original-text="Style library">

### ✅ Настройка порядка введения CSS <meta data-oversett="" data-original-text="✅ Adjust CSS injection order">

Библиотека стилей, используемая по умолчанию в v5, - это [Emotion](https://emotion.sh/docs/introduction).

Если вы использовали JSS для переопределения стилей компонентов Material UI - например, созданных с помощью `makeStyles`\- вам нужно будет позаботиться о порядке введения CSS. Элементы JSS `<style`\>' должны быть введены в `<head>` после элементов Emotion `<style>`'.

Для этого необходимо, чтобы `StyledEngineProvider` с опцией `injectFirst` находился в верхней части дерева компонентов, как показано здесь:

```jsx
import * as React from 'react';
import { StyledEngineProvider } from '@mui/material/styles';

export default function GlobalCssPriority() {
  return (
    {/* Inject Emotion before JSS */}
    <StyledEngineProvider injectFirst>
      {/* Your component tree. Now you can override MUI's styles. */}
    </StyledEngineProvider>
  );
}
```

### ✅ Добавить prepend в createCache <meta data-oversett="" data-original-text="✅ Add prepend to createCache">

Если у вас есть пользовательский кэш и вы используете Emotion для стилизации вашего приложения, он будет переопределять кэш, предоставляемый Material UI.

Чтобы исправить порядок инъекций, добавьте параметр `prepend` к `createCache`, как показано ниже:

```diff
 import * as React from 'react';
 import { CacheProvider } from '@emotion/react';
 import createCache from '@emotion/cache';

 const cache = createCache({
   key: 'css',
+  prepend: true,
 });

 export default function PlainCssPriority() {
   return (
     <CacheProvider value={cache}>
       {/* Your component tree. Now you can override Material UI's styles. */}
     </CacheProvider>
   );
 }
```

:::warning
Если вы используете styled-components и у вас есть `StyleSheetManager` с пользовательским `target`, убедитесь, что target является первым элементом в HTML `<head>`.

Чтобы увидеть, как это можно сделать, посмотрите на [реализацию`StyledEngineProvider`](https://github.com/mui/material-ui/blob/master/packages/mui-styled-engine-sc/src/StyledEngineProvider/StyledEngineProvider.js) в пакете `@mui/styled-engine-sc`.
:::

## Структура темы <meta data-oversett="" data-original-text="Theme structure">

### ✅ Добавление помощника adaptV4Theme <meta data-oversett="" data-original-text="✅ Add adaptV4Theme helper">

Структура темы изменилась в v5. Вам необходимо обновить ее форму. Для более плавного перехода помощник `adaptV4Theme` позволяет итеративно обновить некоторые изменения темы до новой структуры темы.

```diff
-import { createMuiTheme } from '@mui/material/styles';
+import { createTheme, adaptV4Theme } from '@mui/material/styles';

-const theme = createMuiTheme({
+const theme = createTheme(adaptV4Theme({
   // v4 theme
-});
+}));
```

:::warning
Этот адаптер обрабатывает только входные аргументы `createTheme`. Если вы изменяете форму темы после ее создания, вам необходимо перенести структуру вручную.
:::

Адаптер поддерживает следующие изменения:

### Удалить желоба <meta data-oversett="" data-original-text="Remove gutters">

Абстракция "gutters" используется недостаточно часто, чтобы быть полезной.

```diff
-theme.mixins.gutters(),
+paddingLeft: theme.spacing(2),
+paddingRight: theme.spacing(2),
+[theme.breakpoints.up('sm')]: {
+  paddingLeft: theme.spacing(3),
+  paddingRight: theme.spacing(3),
+},
```

### ✅ Убрать суффикс px <meta data-oversett="" data-original-text="✅ Remove px suffix">

`theme.spacing` теперь по умолчанию возвращает единичные значения с единицами измерения px. Это изменение улучшает интеграцию со стилизованными компонентами и Emotion.

До:

```js
theme.spacing(2) => 16
```

После:

```js
theme.spacing(2) => '16px'
```

### ✅ Переименование theme.palette.type <meta data-oversett="" data-original-text="✅ Rename theme.palette.type">

Ключ `theme.palette.type` был переименован в `theme.palette.mode`, чтобы лучше следовать терминологии "темного режима", которая обычно используется для описания этой функции.

```diff
 import { createTheme } from '@mui/material/styles';
-const theme = createTheme({ palette: { type: 'dark' } }),
+const theme = createTheme({ palette: { mode: 'dark' } }),
```

### Изменить цвета по умолчанию theme.palette.info <meta data-oversett="" data-original-text="Change default theme.palette.info colors">

Цвета по умолчанию `theme.palette.info` были изменены таким образом, чтобы коэффициент контрастности соответствовал стандарту доступности AA как в светлом, так и в темном режимах.

```diff
  info = {
-  main: cyan[500],
+  main: lightBlue[700], // lightBlue[400] in "dark" mode

-  light: cyan[300],
+  light: lightBlue[500], // lightBlue[300] in "dark" mode

-  dark: cyan[700],
+  dark: lightBlue[900], // lightBlue[700] in "dark" mode
  }
```

### Изменение цветов по умолчанию theme.palette.success <meta data-oversett="" data-original-text="Change default theme.palette.success colors">

Цвета по умолчанию `theme.palette.success` были изменены для соответствия стандарту доступности AA по коэффициенту контрастности как в светлом, так и в темном режимах.

```diff
  success = {
-  main: green[500],
+  main: green[800], // green[400] in "dark" mode

-  light: green[300],
+  light: green[500], // green[300] in "dark" mode

-  dark: green[700],
+  dark: green[900], // green[700] in "dark" mode
  }
```

### Изменение цветов по умолчанию в палитре theme.palette.warning <meta data-oversett="" data-original-text="Change default theme.palette.warning colors">

Цвета по умолчанию `theme.palette.warning` были изменены для соответствия стандарту доступности AA по коэффициенту контрастности как в светлом, так и в темном режимах.

```diff
  warning = {
-  main: orange[500],
+  main: '#ED6C02', // orange[400] in "dark" mode

-  light: orange[300],
+  light: orange[500], // orange[300] in "dark" mode

-  dark: orange[700],
+  dark: orange[900], // orange[700] in "dark" mode
  }
```

### Восстановить ключ theme.palette.text.hint (если необходимо). <meta data-oversett="" data-original-text="Restore theme.palette.text.hint key (if needed)">

Ключ `theme.palette.text.hint` не использовался в компонентах Material UI и был удален. Если вы зависите от него, вы можете добавить его обратно:

```diff
  import { createTheme } from '@mui/material/styles';

-const theme = createTheme(),
+const theme = createTheme({
+  palette: { text: { hint: 'rgba(0, 0, 0, 0.38)' } },
+});
```

### Перестроить определения компонентов <meta data-oversett="" data-original-text="Restructure component definitions">

Определения компонентов в теме были реструктурированы под ключ `components`, чтобы их было легче найти.

#### 1\. реквизиты <meta data-oversett="" data-original-text="1. props">

```diff
 import { createTheme } from '@mui/material/styles';

 const theme = createTheme({
-  props: {
-    MuiButton: {
-      disableRipple: true,
-    },
-  },
+  components: {
+    MuiButton: {
+      defaultProps: {
+        disableRipple: true,
+      },
+    },
+  },
 });
```

#### 2\. переопределения <meta data-oversett="" data-original-text="2. overrides">

```diff
 import { createTheme } from '@mui/material/styles';

 const theme = createTheme({
-  overrides: {
-    MuiButton: {
-      root: { padding: 0 },
-    },
-  },
+  components: {
+    MuiButton: {
+      styleOverrides: {
+        root: { padding: 0 },
+      },
+    },
+  },
 });
```

## @mui/styles <meta data-oversett="" data-original-text="@mui/styles">

### Обновление импорта ThemeProvider <meta data-oversett="" data-original-text="Update ThemeProvider import">

Если вы используете утилиты из `@mui/styles` вместе с `@mui/material`, вам следует заменить использование `ThemeProvider` из `@mui/styles` на экспортированное из `@mui/material/styles`.

Таким образом, `theme`, предоставленный в контексте, будет доступен в обеих утилитах стилизации, экспортированных из `@mui/styles`, таких как `makeStyles`, `withStyles` и т.д., вместе с компонентами Material UI.

```diff
-import { ThemeProvider } from '@mui/styles';
+import { ThemeProvider } from '@mui/material/styles';
```

Обязательно добавьте `ThemeProvider` в корень вашего приложения, так как `defaultTheme` больше не доступен в утилитах, полученных из `@mui/styles`.

### ✅ Добавление модуля дополнения для DefaultTheme (TypeScript). <meta data-oversett="" data-original-text="✅ Add module augmentation for DefaultTheme (TypeScript)">

Пакет `@mui/styles` больше не является частью `@mui/material/styles`.

Если вы используете `@mui/styles` вместе с `@mui/material`, вам необходимо добавить модуль дополнения для `DefaultTheme`.

```ts
// in the file where you are creating the theme (invoking the function `createTheme()`)
import { Theme } from '@mui/material/styles';

declare module '@mui/styles' {
  interface DefaultTheme extends Theme {}
}
```

## @mui/material/colors <meta data-oversett="" data-original-text="@mui/material/colors">

### ✅ Изменение импорта цветов <meta data-oversett="" data-original-text="✅ Change color imports">

Вложенные импорты более чем одного уровня являются частными. Например, вы больше не можете импортировать `red` из `@mui/material/colors/red`.

```diff
-import red from '@mui/material/colors/red';
+import { red } from '@mui/material/colors';
```

## @mui/material/styles <meta data-oversett="" data-original-text="@mui/material/styles">

### ✅ Переименовать затухание в альфу <meta data-oversett="" data-original-text="✅ Rename fade to alpha">

`fade` был переименован в `alpha`, чтобы лучше описать его функциональность.

Предыдущее название вызывало путаницу, когда цвет ввода уже имел значение альфа. Помощник переопределяет альфа-значение цвета.

```diff
-import { fade } from '@mui/material/styles';
+import { alpha } from '@mui/material/styles';

  const classes = makeStyles(theme => ({
-  backgroundColor: fade(theme.palette.primary.main, theme.palette.action.selectedOpacity),
+  backgroundColor: alpha(theme.palette.primary.main, theme.palette.action.selectedOpacity),
  }));
```

### ✅ Обновление импорта createStyles <meta data-oversett="" data-original-text="✅ Update createStyles import">

Функция `createStyles` из `@mui/material/styles` была перенесена в функцию, экспортируемую из `@mui/styles`. Это необходимо для устранения зависимости от `@mui/styles` в пакете Material UI npm.

```diff
-import { createStyles } from '@mui/material/styles';
+import { createStyles } from '@mui/styles';
```

### ✅ Обновление createGenerateClassName import <meta data-oversett="" data-original-text="✅ Update createGenerateClassName import">

Функция `createGenerateClassName` больше не экспортируется из `@mui/material/styles`. Вы должны импортировать ее непосредственно из `@mui/styles`.

```diff
-import { createGenerateClassName } from '@mui/material/styles';
+import { createGenerateClassName } from '@mui/styles';
```

Чтобы генерировать пользовательские имена классов без использования `@mui/styles`, ознакомьтесь с более подробной информацией в [ClassName Generator](/material-ui/experimental-api/classname-generator/).

### ✅ Переименование createMuiTheme <meta data-oversett="" data-original-text="✅ Rename createMuiTheme">

Функция `createMuiTheme` была переименована в `createTheme`, чтобы сделать ее более интуитивно понятной для использования с `ThemeProvider`.

```diff
-import { createMuiTheme } from '@mui/material/styles';
+import { createTheme } from '@mui/material/styles';

-const theme = createMuiTheme({
+const theme = createTheme({
```

### ✅ Обновить импорт MuiThemeProvider <meta data-oversett="" data-original-text="✅ Update MuiThemeProvider import">

Компонент `MuiThemeProvider` больше не экспортируется из `@mui/material/styles`. Вместо него используйте `ThemeProvider`.

```diff
-import { MuiThemeProvider } from '@mui/material/styles';
+import { ThemeProvider } from '@mui/material/styles';
```

### ✅ Обновление импорта jssPreset <meta data-oversett="" data-original-text="✅ Update jssPreset import">

Объект `jssPreset` больше не экспортируется из `@mui/material/styles`. Вы должны импортировать его непосредственно из `@mui/styles`.

```diff
-import { jssPreset } from '@mui/material/styles';
+import { jssPreset } from '@mui/styles';
```

### ✅ Обновить импорт `makeStyles` <meta data-oversett="" data-original-text="✅ Update makeStyles import">

Утилита `makeStyles` JSS больше не экспортируется из `@mui/material/styles`. Вместо нее можно использовать `@mui/styles/makeStyles`.

Обязательно добавьте `ThemeProvider` в корень вашего приложения, так как `defaultTheme` больше не доступен.

Если вы используете эту утилиту вместе с `@mui/material`, рекомендуется вместо нее использовать компонент `ThemeProvider` из `@mui/material/styles`.

```diff
-import { makeStyles } from '@mui/material/styles';
+import { makeStyles } from '@mui/styles';
+import { createTheme, ThemeProvider } from '@mui/material/styles';

+const theme = createTheme();
  const useStyles = makeStyles((theme) => ({
    background: theme.palette.primary.main,
  }));
  function Component() {
    const classes = useStyles();
    return <div className={classes.root} />
  }

  // In the root of your app
  function App(props) {
-  return <Component />;
+  return <ThemeProvider theme={theme}><Component {...props} /></ThemeProvider>;
  }
```

### ✅ Обновление импорта ServerStyleSheets <meta data-oversett="" data-original-text="✅ Update ServerStyleSheets import">

Компонент `ServerStyleSheets` больше не экспортируется из `@mui/material/styles`. Вы должны импортировать его непосредственно из `@mui/styles`.

```diff
-import { ServerStyleSheets } from '@mui/material/styles';
+import { ServerStyleSheets } from '@mui/styles';
```

### стилизованный <meta data-oversett="" data-original-text="styled">

Утилита `styled` JSS больше не экспортируется из `@mui/material/styles`. Вместо нее можно использовать ту, что экспортируется из `@mui/styles`.

Обязательно добавьте `ThemeProvider` в корень вашего приложения, так как `defaultTheme` больше не доступна.

Если вы используете эту утилиту вместе с `@mui/material`, рекомендуется вместо нее использовать компонент `ThemeProvider` из `@mui/material/styles`.

```diff
-import { styled } from '@mui/material/styles';
+import { styled } from '@mui/styles';
+import { createTheme, ThemeProvider } from '@mui/material/styles';

+const theme = createTheme();
  const MyComponent = styled('div')(({ theme }) => ({ background: theme.palette.primary.main }));

  function App(props) {
-  return <MyComponent />;
+  return <ThemeProvider theme={theme}><MyComponent {...props} /></ThemeProvider>;
  }
```

### ✅ Обновление импорта StylesProvider <meta data-oversett="" data-original-text="✅ Update StylesProvider import">

Компонент `StylesProvider` больше не экспортируется из `@mui/material/styles`. Вы должны импортировать его непосредственно из `@mui/styles`.

```diff
-import { StylesProvider } from '@mui/material/styles';
+import { StylesProvider } from '@mui/styles';
```

### ✅ Обновление импорта UseThemeVariants <meta data-oversett="" data-original-text="✅ Update useThemeVariants import">

Хук `useThemeVariants` больше не экспортируется из `@mui/material/styles`. Вы должны импортировать его непосредственно из `@mui/styles`.

```diff
-import { useThemeVariants } from '@mui/material/styles';
+import { useThemeVariants } from '@mui/styles';
```

### ✅ Обновить импорт withStyles <meta data-oversett="" data-original-text="✅ Update withStyles import">

Утилита `withStyles` JSS больше не экспортируется из `@mui/material/styles`. Вы можете использовать `@mui/styles/withStyles` вместо нее.

Обязательно добавьте `ThemeProvider` в корень вашего приложения, так как `defaultTheme` больше не доступен.

Если вы используете эту утилиту вместе с `@mui/material`, вместо нее следует использовать компонент `ThemeProvider` из `@mui/material/styles`.

```diff
-import { withStyles } from '@mui/material/styles';
+import { withStyles } from '@mui/styles';
+import { createTheme, ThemeProvider } from '@mui/material/styles';

+const defaultTheme = createTheme();
  const MyComponent = withStyles((props) => {
    const { classes, className, ...other } = props;
    return <div className={clsx(className, classes.root)} {...other} />
  })(({ theme }) => ({ root: { background: theme.palette.primary.main }}));

  function App() {
-  return <MyComponent />;
+  return <ThemeProvider theme={defaultTheme}><MyComponent /></ThemeProvider>;
  }
```

### ✅ Замените innerRef на ref <meta data-oversett="" data-original-text="✅ Replace innerRef with ref">

Замените реквизит `innerRef` на реквизит `ref`. Теперь ссылки автоматически перенаправляются на внутренний компонент.

```diff
  import * as React from 'react';
  import { withStyles } from '@mui/styles';

  const MyComponent = withStyles({
    root: {
      backgroundColor: 'red',
    },
  })(({ classes }) => <div className={classes.root} />);

  function MyOtherComponent(props) {
    const ref = React.useRef();
-  return <MyComponent innerRef={ref} />;
+  return <MyComponent ref={ref} />;
  }
```

### Обновление импорта withTheme <meta data-oversett="" data-original-text="Update withTheme import">

Утилита `withTheme` HOC была удалена из пакета `@mui/material/styles`. Вместо нее вы можете использовать `@mui/styles/withTheme`.

Обязательно добавьте `ThemeProvider` в корень вашего приложения, так как `defaultTheme` больше не доступен.

Если вы используете эту утилиту вместе с `@mui/material`, рекомендуется вместо нее использовать компонент `ThemeProvider` из пакета `@mui/material/styles`.

```diff
-import { withTheme } from '@mui/material/styles';
+import { withTheme } from '@mui/styles';
+import { createTheme, ThemeProvider } from '@mui/material/styles';

+const theme = createTheme();
  const MyComponent = withTheme(({ theme }) => <div>{props.theme.direction}</div>);

  function App(props) {
-  return <MyComponent />;
+  return <ThemeProvider theme={theme}><MyComponent {...props} /></ThemeProvider>;
  }
```

### ✅ Удалить withWidth <meta data-oversett="" data-original-text="✅ Remove withWidth">

Этот HOC был удален. Если вам нужна эта функция, вы можете попробовать [альтернативу, использующую хук `useMediaQuery`](/material-ui/react-use-media-query/#migrating-from-withwidth) .

## @mui/icons-material <meta data-oversett="" data-original-text="@mui/icons-material">

### Уменьшить размер значка GitHub <meta data-oversett="" data-original-text="Reduce GitHub icon size">

Размер иконки GitHub был уменьшен с 24px до 22px в ширину, чтобы соответствовать размеру других иконок.

## @material-ui/pickers <meta data-oversett="" data-original-text="@material-ui/pickers">

У нас есть [специальная страница](/material-ui/guides/pickers-migration/) для миграции `@material-ui/pickers` на v5.

## Система <meta data-oversett="" data-original-text="System">

### ✅ Переименование реквизитов пробелов <meta data-oversett="" data-original-text="✅ Rename gap props">

Следующие системные функции и свойства были переименованы, поскольку они считаются устаревшими CSS:

-   `gridGap` становится `gap`
-   `gridRowGap` становится `rowGap`
-   `gridColumnGap` становится `columnGap`

### ✅ Добавление единиц интервала к реквизитам пробелов <meta data-oversett="" data-original-text="✅ Add spacing units to gap props">

Используйте единицу интервала в `gap`, `rowGap` и `columnGap`. Если ранее вы использовали число, вам нужно упомянуть px, чтобы обойти новое преобразование в `theme.spacing`.

```diff
  <Box
-  gap={2}
+  gap="2px"
  >
```

Замените реквизит `css` на `sx`, чтобы избежать столкновения со стилизованными компонентами и реквизитом `css` от Emotion.

```diff
-<Box css={{ color: 'primary.main' }} />
+<Box sx={{ color: 'primary.main' }} />
```

:::warning
Функция системной сетки не была документирована в v4.
:::
