

# Миграция с JSS (необязательно) <meta data-oversett="" data-original-text="Migrating from JSS (optional)">

<p class="description">Это руководство объясняет, как перейти с JSS на Emotion при обновлении с Material UI v4 на v5.</p>

## Миграция Material UI v5 <meta data-oversett="" data-original-text="Material UI v5 migration">

1.  [Начало работы](/material-ui/migration/migration-v4/)
2.  [Внесение изменений, часть первая: стиль и тема](/material-ui/migration/v5-style-changes/)
3.  [Внесение изменений, часть вторая: компоненты](/material-ui/migration/v5-component-changes/)
4.  Миграция с JSS 👈 _Вы здесь_
5.  [Устранение неполадок](/material-ui/migration/troubleshooting/)

## Переход с JSS на Emotion <meta data-oversett="" data-original-text="Migrating from JSS to Emotion">

Одним из самых больших изменений в v5 является замена JSS на [Emotion](https://emotion.sh/docs/introduction) (или [styled-components](https://styled-components.com/) в качестве альтернативы) в качестве решения по стилизации по умолчанию.

Обратите внимание, что вы можете продолжать использовать JSS для добавления переопределений для компонентов (например, `makeStyles`, `withStyles`) даже после перехода на v5. Затем, если в какой-то момент вы захотите перейти на новый механизм стилизации, вы можете постепенно рефакторить свои компоненты.

:::info
Если вы используете Next.js и не уверены, как настроить SSR для работы с Emotion и JSS, посмотрите этот [пример проекта](https://github.com/mui/material-ui/tree/master/examples/nextjs-with-typescript-v4-migration).
:::

В этом документе рассматриваются все шаги, необходимые для перехода от JSS.

Хотя вы можете использовать любой из следующих двух вариантов, первый считается предпочтительным:

### 1\. Использовать стилизованный или sx API <meta data-oversett="" data-original-text="1. Use styled or sx API">

#### Кодмод <meta data-oversett="" data-original-text="Codemod">

Мы предоставляем [codemod](https://github.com/mui/material-ui/blob/master/packages/mui-codemod/README.md#jss-to-styled), чтобы помочь перенести стили JSS на `styled` API, но этот подход увеличивает специфичность CSS.

:::info
Обычно вы не будете писать стили подобным образом. Но это лучшее преобразование, которое мы смогли создать с помощью кодмода.

Если вы захотите доработать их позже, вы можете обратиться к примерам, показанным в разделах ниже.
:::

```sh
npx @mui/codemod v5.0.0/jss-to-styled <path>
```

Пример трансформации:

```diff
 import Typography from '@mui/material/Typography';
-import makeStyles from '@mui/styles/makeStyles';
+import { styled } from '@mui/material/styles';

-const useStyles = makeStyles((theme) => ({
-  root: {
-    display: 'flex',
-    alignItems: 'center',
-    backgroundColor: theme.palette.primary.main
-  },
-  cta: {
-    borderRadius: theme.shape.radius
-  },
-  content: {
-    color: theme.palette.common.white,
-    fontSize: 16,
-    lineHeight: 1.7
-  },
-}))
+const PREFIX = 'MyCard';
+const classes = {
+  root: `${PREFIX}-root`,
+  cta: `${PREFIX}-cta`,
+  content: `${PREFIX}-content`,
+}
+const Root = styled('div')(({ theme }) => ({
+  [`&.${classes.root}`]: {
+    display: 'flex',
+    alignItems: 'center',
+    backgroundColor: theme.palette.primary.main
+  },
+  [`& .${classes.cta}`]: {
+    borderRadius: theme.shape.radius
+  },
+  [`& .${classes.content}`]: {
+    color: theme.palette.common.white,
+    fontSize: 16,
+    lineHeight: 1.7
+  },
+}))

 export const MyCard = () => {
-  const classes = useStyles();
   return (
-    <div className={classes.root}>
+    <Root className={classes.root}>
       {/* The benefit of this approach is that the code inside Root stays the same. */}
       <Typography className={classes.content}>...</Typography>
       <Button className={classes.cta}>Go</Button>
-    </div>
+    </Root>
   )
 }
```

:::success
Вам следует запустить этот кодмод на небольшом участке файлов и затем проверить изменения, прежде чем продолжать, потому что в некоторых случаях вам может понадобиться корректировка кода после трансформации - этот кодмод не охватывает все случаи.
:::

#### Руководство <meta data-oversett="" data-original-text="Manual">

Мы рекомендуем API `sx` вместо `styled` для создания отзывчивых стилей или переопределения второстепенных CSS.[Подробнее о `sx` читайте здесь](/system/getting-started/the-sx-prop/).

```diff
 import Chip from '@mui/material/Chip';
-import makeStyles from '@mui/styles/makeStyles';
+import Box from '@mui/material/Box';
+import { styled } from '@mui/material/styles';

-const useStyles = makeStyles((theme) => ({
-  wrapper: {
-    display: 'flex',
-  },
-  chip: {
-    padding: theme.spacing(1, 1.5),
-    boxShadow: theme.shadows[1],
-  }
-}));

 function App() {
-  const classes = useStyles();
   return (
-    <div>
-      <Chip className={classes.chip} label="Chip" />
-    </div>
+    <Box sx={{ display: 'flex' }}>
+      <Chip label="Chip" sx={{ py: 1, px: 1.5, boxShadow: 1 }} />
+    </Box>
   );
 }
```

В некоторых случаях вы можете захотеть создать несколько стилизованных компонентов в одном файле вместо того, чтобы увеличивать специфичность CSS.

Например:

```diff
-import makeStyles from '@mui/styles/makeStyles';
+import { styled } from '@mui/material/styles';

-const useStyles = makeStyles((theme) => ({
-  root: {
-    display: 'flex',
-    alignItems: 'center',
-    borderRadius: 20,
-    background: theme.palette.grey[50],
-  },
-  label: {
-    color: theme.palette.primary.main,
-  }
-}))
+const Root = styled('div')(({ theme }) => ({
+  display: 'flex',
+  alignItems: 'center',
+  borderRadius: 20,
+  background: theme.palette.grey[50],
+}))

+const Label = styled('span')(({ theme }) => ({
+  color: theme.palette.primary.main,
+}))

 function Status({ label }) {
-  const classes = useStyles();
   return (
-    <div className={classes.root}>
-      {icon}
-      <span className={classes.label}>{label}</span>
-    </div>
+    <Root>
+      {icon}
+      <Label>{label}</Label>
+    </Root>
   )
 }
```

:::success
[Этот инструмент jss-to-styled](https://siriwatk.dev/tool/jss-to-styled) помогает преобразовать JSS в несколько стилизованных компонентов без увеличения специфичности CSS.

Этот инструмент _не_ поддерживается MUI.
:::

### 2\. Используйте [tss-react](https://github.com/garronej/tss-react) <meta data-oversett="" data-original-text="2. Use tss-react">

:::error
Этот API не будет работать, если вы [используете `styled-components` в качестве базового механизма стилизации вместо `@emotion`.](/material-ui/guides/interoperability/#styled-components)
:::

API похож на JSS `makeStyles`, но под капотом он использует `@emotion/react`. Он также имеет гораздо лучшую поддержку TypeScript, чем `makeStyles` в v4.

Чтобы использовать его, вам нужно добавить его в зависимости вашего проекта:

С помощью npm:

```sh
npm install tss-react
```

С yarn:

```sh
yarn add tss-react
```

#### Codemod <meta data-oversett="" data-original-text="Codemod">

Мы предоставляем [codemod](https://github.com/mui/material-ui/blob/master/packages/mui-codemod/README.md#jss-to-tss-react), чтобы помочь перенести стили JSS на API `tss-react`.

```sh
npx @mui/codemod v5.0.0/jss-to-tss-react <path>
```

Пример преобразования:

```diff
 import React from 'react';
-import makeStyles from '@material-ui/styles/makeStyles';
+import { makeStyles } from 'tss-react/mui';
 import Button from '@mui/material/Button';
 import Link from '@mui/material/Link';

-const useStyles = makeStyles((theme) => {
+const useStyles = makeStyles()((theme) => {
   return {
     root: {
       color: theme.palette.primary.main,
     },
     apply: {
       marginRight: theme.spacing(2),
     },
   };
 });

 function Apply() {
-  const classes = useStyles();
+  const { classes } = useStyles();

   return (
     <div className={classes.root}>
       <Button component={Link} to="https://support.mui.com" className={classes.apply}>
         Apply now
       </Button>
     </div>
   );
 }

 export default Apply;
```

Если вы используете синтаксис `$` и `clsx` для объединения нескольких классов CSS, преобразование будет выглядеть следующим образом:

```diff
 import * as React from 'react';
-import { makeStyles } from '@material-ui/core/styles';
-import clsx from 'clsx';
+import { makeStyles } from 'tss-react/mui';

-const useStyles = makeStyles((theme) => ({
+const useStyles = makeStyles<void, 'child' | 'small'>()((theme, _params, classes) => ({
   parent: {
     padding: 30,
-    '&:hover $child': {
+    [`&:hover .${classes.child}`]: {
       backgroundColor: 'red',
     },
   },
   small: {},
   child: {
     backgroundColor: 'blue',
     height: 50,
-    '&$small': {
+    [`&.${classes.small}`]: {
       backgroundColor: 'lightblue',
       height: 30
     }
   },
 }));

 function App() {
-  const classes = useStyles();
+  const { classes, cx } = useStyles();
   return (
     <div className={classes.parent}>
       <div className={classes.child}>
         Background turns red when the mouse hovers over the parent.
       </div>
-      <div className={clsx(classes.child, classes.small)}>
+      <div className={cx(classes.child, classes.small)}>
         Background turns red when the mouse hovers over the parent.
         I am smaller than the other child.
       </div>
     </div>
   );
 }

 export default App;
```

:::error
При использовании JavaScript (а не TypeScript) удалите `<void, 'child' | 'small'>`.
:::

Ниже приведен полный пример с использованием синтаксиса `$`, параметров `useStyles()`, объединением классов из реквизита `classes` [(см. doc](https://docs.tss-react.dev/your-own-classes-prop)) и [явным именем таблицы стилей](https://docs.tss-react.dev/api/makestyles#naming-the-stylesheets-useful-for-debugging-and-theme-style-overrides).

```diff
-import clsx from 'clsx';
-import { makeStyles, createStyles } from '@material-ui/core/styles';
+import { makeStyles } from 'tss-react/mui';

-const useStyles = makeStyles((theme) => createStyles<
-  'root' | 'small' | 'child', {color: 'primary' | 'secondary', padding: number}
->
-({
-  root: ({color, padding}) => ({
+const useStyles = makeStyles<{color: 'primary' | 'secondary', padding: number}, 'child' | 'small'>({name: 'App'})((theme, { color, padding }, classes) => ({
+  root: {
     padding: padding,
-    '&:hover $child': {
+    [`&:hover .${classes.child}`]: {
       backgroundColor: theme.palette[color].main,
     }
-  }),
+  },
   small: {},
   child: {
     border: '1px solid black',
     height: 50,
-    '&$small': {
+    [`&.${classes.small}`]: {
       height: 30
     }
   }
-}), {name: 'App'});
+}));

 function App({classes: classesProp}: {classes?: any}) {
-  const classes = useStyles({color: 'primary', padding: 30, classes: classesProp});
+  const { classes, cx } = useStyles({
+    color: 'primary',
+    padding: 30
+  }, {
+    props: {
+      classes: classesProp
+    }
+  });

   return (
     <div className={classes.root}>
       <div className={classes.child}>
         The Background take the primary theme color when the mouse hovers the parent.
       </div>
-      <div className={clsx(classes.child, classes.small)}>
+      <div className={cx(classes.child, classes.small)}>
         The Background take the primary theme color when the mouse hovers the parent.
         I am smaller than the other child.
       </div>
     </div>
   );
 }

 export default App;
```

После запуска codemod, поищите в коде "TODO jss-to-tss-react codemod", чтобы найти случаи, которые codemod не смог надежно обработать.

Кроме случаев с комментариями TODO могут быть и другие, которые не полностью обрабатываются кодмодом - в частности, если части стилей возвращаются функциями.

Если стили, спрятанные в функции, используют синтаксис `$` или параметры `useStyles`, то эти стили не будут перенесены должным образом.

:::error
Вам следует отказаться от [`clsx`](https://www.npmjs.com/package/clsx) в пользу [`cx`](https://emotion.sh/docs/@emotion/css#cx).

Ключевое преимущество `cx` заключается в том, что он определяет имена классов, генерируемые Emotion, чтобы гарантировать, что стили будут перезаписаны в правильном порядке.

Приоритет стилей из нескольких CSS-классов по умолчанию отличается между JSS и tss-react, поэтому может потребоваться ручная перестановка параметров `cx` - подробнее см. в [этом комментарии](https://github.com/mui/material-ui/pull/31802#issuecomment-1093478971).
:::

Чтобы гарантировать, что имена ваших классов всегда включают фактическое имя ваших компонентов, вы можете предоставить `name` как неявно именованный ключ (`name: { App }`).

Подробности см. в [этом документе tss-react doc](https://docs.tss-react.dev/api/makestyles#naming-the-stylesheets-useful-for-debugging-and-theme-style-overrides).

Вы можете получить предупреждения eslint, [подобные этому](https://user-images.githubusercontent.com/6702424/148657837-eae48942-fb86-4516-abe4-5dc10f44f0be.png), если вы деконструируете более одного элемента.

Не стесняйтесь отключить `eslint(prefer-const)`, [как это](https://github.com/thieryw/gitlanding/blob/b2b0c71d95cfd353979c86dfcfa1646ef1665043/.eslintrc.js#L17) сделано в обычном проекте, или [как это сделано](https://github.com/InseeFrLab/onyxia-web/blob/a264ec6a6a7110cb1a17b2e22cc0605901db6793/package.json#L133) в CRA.

#### withStyles() <meta data-oversett="" data-original-text="withStyles()">

`tss-react` также имеет [безопасную для типов реализацию](https://docs.tss-react.dev/api/withstyles) [`withStyles()` из v4.](https://v4.mui.com/styles/api/#withstyles-styles-options-higher-order-component)

:::info
Эквивалент синтаксиса `$` также поддерживается в tss's `withStyles()`.[См. doc](https://docs.tss-react.dev/nested-selectors#withstyles).
:::

```diff
-import Button from '@material-ui/core/Button';
+import Button from '@mui/material/Button';
-import withStyles from '@material-ui/styles/withStyles';
+import { withStyles } from 'tss-react/mui';

 const MyCustomButton = withStyles(
+  Button,
   (theme) => ({
     root: {
       minHeight: '30px',
     },
     textPrimary: {
       color: theme.palette.text.primary,
     },
     '@media (min-width: 960px)': {
       textPrimary: {
         fontWeight: 'bold',
       },
     },
   }),
-)(Button);
+);

 export default MyCustomButton;
```

#### Переопределения стилей темы <meta data-oversett="" data-original-text="Theme style overrides">

[Глобальные переопределения тем](https://v4.mui.com/customization/components/#global-theme-override) поддерживаются TSS из коробки.

Следуйте инструкциям в соответствующем разделе документа [Breaking changes](/material-ui/migration/v5-style-changes/#restructure-component-definitions) doc и [предоставьте `name` на `makeStyles`.](https://docs.tss-react.dev/api/makestyles#naming-the-stylesheets-useful-for-debugging-and-theme-style-overrides)

В Material UI v5 [переопределения стиля также принимают обратные вызовы](https://mui.com/material-ui/customization/theme-components/).

По умолчанию TSS может предоставить только тему. Если вы хотите предоставить реквизиты и `ownerState`, [пожалуйста, обратитесь к этой документации](https://docs.tss-react.dev/mui-theme-styleoverrides).

:::warning
tss-react _не_ поддерживается MUI.

Если у вас есть вопросы по настройке SSR (Next.js), или если вы хотите узнать, как настроить объект `theme`, пожалуйста, обратитесь к документации по tss-react, в частности, к [разделу интеграции с MUI](https://github.com/garronej/tss-react#mui-integration).

Вы также можете [отправить проблему](https://github.com/garronej/tss-react/issues/new) для любой ошибки или запроса функции, а также [начать обсуждение](https://github.com/garronej/tss-react/discussions), если вам нужна помощь.
:::

## Завершите миграцию <meta data-oversett="" data-original-text="Complete the migration">

После того как вы перенесли все стили, удалите ненужный `@mui/styles`, деинсталлировав пакет.

С помощью npm:

```sh
npm uninstall @mui/styles
```

С помощью yarn:

```sh
yarn remove @mui/styles
```

:::warning
`@emotion/styled` является одноранговой зависимостью `@mui/material`. Вы должны сохранить его в своих зависимостях, даже если вы никогда явно не используете его.
:::
