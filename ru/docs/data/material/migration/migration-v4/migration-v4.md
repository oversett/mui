

# Переход на v5: начало работы <meta data-oversett="" data-original-text="Migrating to v5: getting started">

<p class="description">Это руководство объясняет, как и зачем переходить с Material UI v4 на v5.</p>

## Миграция Material UI v5 <meta data-oversett="" data-original-text="Material UI v5 migration">

1.  Начало работы 👈 _Вы здесь_
2.  [Изменения, которые необходимо внести, часть первая: стиль и тема](/material-ui/migration/v5-style-changes/)
3.  [Внесение изменений часть вторая: компоненты](/material-ui/migration/v5-component-changes/)
4.  [Миграция с JSS](/material-ui/migration/migrating-from-jss/)
5.  [Устранение неполадок](/material-ui/migration/troubleshooting/)

## Введение <meta data-oversett="" data-original-text="Introduction">

Это первый документ из серии, состоящей из нескольких частей, в которой мы расскажем вам об обновлении вашего приложения с Material UI v4 до v5.

Мы настоятельно рекомендуем использовать наши [кодмоды](#run-codemods) для повышения эффективности - они автоматически устранят многие из [изменений](#address-breaking-changes), появившихся в v5.

Одним из самых больших изменений в v5 является замена JSS на [Emotion](https://emotion.sh/docs/introduction) в качестве решения для стилизации по умолчанию.

Обратите внимание, что вы можете продолжать использовать JSS для добавления переопределений к компонентам (например, `makeStyles`, `withStyles`) даже после перехода на v5. После того, как вы завершите обновление v5, мы рекомендуем постепенно переходить на новый механизм стилизации.

Этот процесс описан в разделе [Миграция с JSS](/material-ui/migration/migrating-from-jss/).

:::info
Вам нужно вернуться к более старой версии документации? Посмотрите [документацию по v4 здесь](https://v4.mui.com/).
:::

:::info
Если вы используете Next.js и не уверены, как настроить SSR для работы с Emotion и JSS, посмотрите этот [пример проекта](https://github.com/mui/material-ui/tree/master/examples/nextjs-with-typescript-v4-migration).
:::

## Почему вам стоит перейти <meta data-oversett="" data-original-text="Why you should migrate">

Material UI v5 включает в себя множество исправлений ошибок и улучшений по сравнению с v4.

Главным из этих улучшений является новый движок стилей, который обеспечивает значительное повышение производительности при работе с динамическими стилями, а также более приятный опыт разработчика.

Кроме того, v5 - единственная версия, которая полностью поддерживает React 18, поэтому вам необходимо перейти на нее, чтобы воспользоваться преимуществами последних возможностей React.

Чтобы узнать больше, ознакомьтесь с [записью в блоге о выпуске Material UI v5](https://mui.com/blog/mui-core-v5/).

:::success
Создавайте небольшие коммиты по мере продвижения, чтобы обеспечить плавный переход.

Если вы столкнулись с какими-либо проблемами на этом пути, обратитесь к документу " [Устранение неполадок](/material-ui/migration/troubleshooting/) ".

Для проблем, не рассмотренных там, [создайте проблему](https://github.com/mui/material-ui/issues/new?assignees=&labels=status%3A+needs+triage&template=1.bug.yml) с таким названием: **\[Migration\] Краткое описание вашей проблемы**.
:::

## Поддерживаемые браузеры и версии Node <meta data-oversett="" data-original-text="Supported browsers and Node versions">

Цели пакета по умолчанию изменились в v5.

Точные версии будут выведены в релизе из запроса browserslist `"> 0.5%, last 2 versions, Firefox ESR, not dead, not IE 11, maintained node versions"`.

Пакет по умолчанию поддерживает следующие минимальные версии:

-   Node 12 (по сравнению с 8)
-   Chrome 90 (по сравнению с 49)
-   Edge 91 (по сравнению с 14)
-   Firefox 78 (по сравнению с 52)
-   Safari 14 (macOS) и 12.5 (iOS) (в сравнении с 10)
-   и многое другое (см. [.browserslistrc (`stable` entry)](https://github.com/mui/material-ui/blob/HEAD/.browserslistrc#L11)).

Material UI больше не поддерживает IE 11. Если вам нужна поддержка IE 11, обратите внимание на наш [пакет для старых](/material-ui/guides/minimizing-bundle-size/#legacy-bundle) версий.

## Обновление версии React и TypeScript <meta data-oversett="" data-original-text="Update React &amp; TypeScript version">

### Обновите React <meta data-oversett="" data-original-text="Update React">

Минимальная поддерживаемая версия React была увеличена с v16.8.0 до v17.0.0.

Если вы используете версию React ниже 17.0.0, обновите свои пакеты до версии не ниже v4.11.2 для Material UI и v17.0.0 для React.

С помощью npm:

```sh
npm update @material-ui/core@^4.11.2 react@^17.0.0
```

С помощью yarn:

```sh
yarn upgrade @material-ui/core@^4.11.2 react@^17.0.0
```

### Обновите TypeScript <meta data-oversett="" data-original-text="Update TypeScript">

Минимальная поддерживаемая версия TypeScript была увеличена с v3.2 до v3.5.

:::info
Мы стараемся соответствовать типам, выпущенным [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) (т.е. пакетам, опубликованным на npm в пространстве имен `@types` ).

Мы не будем менять минимально поддерживаемую версию в минорной версии Material UI. Однако мы обычно рекомендуем не использовать TypeScript версии старше, чем минимально поддерживаемая версия DefinitelyTyped.
:::

Если ваш проект включает эти пакеты, вам необходимо их обновить:

-   `react-scripts`
-   `@types/react`
-   `@types/react-dom`

:::warning
📝 Убедитесь, что ваше приложение по-прежнему работает без ошибок, и зафиксируйте изменения, прежде чем переходить к следующему шагу.
:::

## Настройте `ThemeProvider` <meta data-oversett="" data-original-text="Set up ThemeProvider">

Перед переходом на v5 убедитесь, что `ThemeProvider` определен в корне вашего приложения и в тестах - даже если вы используете тему по умолчанию - и что `useStyles` _не_ вызывается раньше `ThemeProvider`.

Со временем вы, возможно, захотите [перейти с JSS на Emotion](/material-ui/migration/migrating-from-jss/), но пока вы можете продолжать использовать JSS с пакетом `@mui/styles`. Этот пакет требует `ThemeProvider`.

Корень вашего приложения должен выглядеть примерно так:

```js
import { ThemeProvider, createMuiTheme, makeStyles } from '@material-ui/core/styles';

const theme = createMuiTheme();

const useStyles = makeStyles((theme) => {
  root: {
    // some CSS that accesses the theme
  }
});

function App() {
  const classes = useStyles(); // ❌ If you have this, consider moving it
  // inside of a component wrapped with <ThemeProvider />
  return <ThemeProvider theme={theme}>{children}</ThemeProvider>;
}
```

:::warning
📝 Убедитесь, что ваше приложение по-прежнему работает без ошибок, и зафиксируйте изменения, прежде чем переходить к следующему шагу.
:::

## Обновление пакетов MUI <meta data-oversett="" data-original-text="Update MUI packages">

### Material UI v5 и `@mui/styles` <meta data-oversett="" data-original-text="Material UI v5 and @mui/styles">

Установите пакеты Material UI v5.

С помощью npm:

```sh
npm install @mui/material @mui/styles
```

С помощью yarn:

```sh
yarn add @mui/material @mui/styles
```

Если вы используете `@material-ui/lab` или `@material-ui/icons`, вам необходимо установить новые пакеты.

### `@material-ui/lab` <meta data-oversett="" data-original-text="@material-ui/lab">

С помощью npm:

```sh
npm install @mui/lab
```

С yarn:

```sh
yarn add @mui/lab
```

### `@material-ui/icons` <meta data-oversett="" data-original-text="@material-ui/icons">

С npm:

```sh
npm install @mui/icons-material
```

С yarn:

```sh
yarn add @mui/icons-material
```

### Сборщики даты и времени <meta data-oversett="" data-original-text="Date and time pickers">

Компоненты подборщика даты и времени были перенесены в MUI X. Если вы используете `@material-ui/date-pickers` или подборщики из пакета `@mui/lab`, вам необходимо перейти на `@mui/x-date-pickers`. Подробности смотрите в разделе [Миграция из лаборатории](https://mui.com/x/react-date-pickers/migration-lab/).

### Зависимости от пикеров <meta data-oversett="" data-original-text="Peer dependencies">

Далее добавьте пакеты Emotion.

С помощью npm:

```sh
npm install @emotion/react @emotion/styled
```

С помощью yarn:

```sh
yarn add @emotion/react @emotion/styled
```

#### styled-components (необязательно) <meta data-oversett="" data-original-text="styled-components (optional)">

Если вы хотите использовать Material UI v5 со стилизованными компонентами вместо Emotion, ознакомьтесь с [руководством по установке Material UI](/material-ui/getting-started/installation/).

Обратите внимание, что если ваше приложение использует рендеринг на стороне сервера (SSR), существует [известная ошибка](https://github.com/mui/material-ui/issues/29742) в плагине Babel для styled-components, которая не позволяет использовать `@mui/styled-engine-sc` (адаптер для styled-components).

Мы настоятельно рекомендуем использовать стандартную настройку с Emotion.

:::warning
📝 Убедитесь, что ваше приложение по-прежнему работает без ошибок, и зафиксируйте изменения, прежде чем переходить к следующему шагу.
:::

### Замените все импорты <meta data-oversett="" data-original-text="Replace all imports">

С выходом v5 имена всех связанных пакетов были изменены с `@material-ui/*` на `@mui/*` в рамках нашего обновленного брендинга. Подробности см. в [этой статье блога](/blog/material-ui-is-now-mui/).

<details><summary>Обновленные имена пакетов</summary><pre><code class="language-text">@material-ui/core -&gt; @mui/material
@material-ui/unstyled -&gt; @mui/base
@material-ui/icons -&gt; @mui/icons-material
@material-ui/styles -&gt; @mui/styles
@material-ui/system -&gt; @mui/system
@material-ui/lab -&gt; @mui/lab
@material-ui/types -&gt; @mui/types
@material-ui/styled-engine -&gt; @mui/styled-engine
@material-ui/styled-engine-sc -&gt;@mui/styled-engine-sc
@material-ui/private-theming -&gt; @mui/private-theming
@material-ui/codemod -&gt; @mui/codemod
@material-ui/docs -&gt; @mui/docs
@material-ui/envinfo -&gt; @mui/envinfo
</code></pre></details>

### Удаление старых пакетов <meta data-oversett="" data-original-text="Remove old packages">

После того, как вы установили все необходимые пакеты и убедились, что ваше приложение по-прежнему работает, вы можете безопасно удалить старые пакеты `@material-ui/*`, запустив `npm uninstall @material-ui/*` или `yarn remove @material-ui/*`.

:::success
[Предварительно безопасный кодмод](#preset-safe) (более подробно описано ниже) делает это автоматически.
:::

## Исправить специфику CSS (необязательно) <meta data-oversett="" data-original-text="Fix CSS specificity (optional)">

Если вы хотите применить стили к компонентам, импортируя CSS-файл, вам необходимо повысить специфичность, чтобы иметь возможность нацеливать нужные компоненты.

Рассмотрим следующий пример:

```js
import './style.css';
import Chip from '@mui/material/Chip';

const ChipWithGreenIcon = () => (
  <Chip
    classes={{ deleteIcon: 'green' }}
    label="delete icon is green"
    onDelete={() => {}}
  />
);
```

В этом примере, чтобы правильно применить определенный стиль к значку удаления `Chip`, одним из вариантов является увеличение специфичности ваших CSS-классов, как показано ниже:

```css
.MuiChip-root .green {
  color: green;
}
```

В отличие от этого, следующий фрагмент CSS не применит стиль к значку удаления:

```css
.green {
  color: green;
}
```

## Запустите кодмоды <meta data-oversett="" data-original-text="Run codemods">

Следующие кодовые модули автоматически скорректируют основную часть вашего кода с учетом изменений в v5.

Убедитесь, что ваше приложение по-прежнему работает без ошибок после выполнения каждого кода, и зафиксируйте изменения, прежде чем переходить к следующему шагу.

### preset-safe <meta data-oversett="" data-original-text="preset-safe">

Этот кодмод содержит большинство трансформаторов, необходимых для миграции. Его следует применять только **один раз для каждой папки.**

```sh
npx @mui/codemod v5.0.0/preset-safe <path>
```

:::info
Если вы хотите запускать трансформаторы по одному, ознакомьтесь с [кодовым модулем preset-safe](https://github.com/mui/material-ui/blob/master/packages/mui-codemod/README.md#-preset-safe).
:::

### variant-prop <meta data-oversett="" data-original-text="variant-prop">

Этот кодмод преобразует компоненты `<TextField/>`, `<FormControl/>` и `<Select/>`, применяя `variant="standard"`, если вариант не определен - вариант по умолчанию изменился с `"standard"` в v4 на `"outlined"` в v5.

:::error
Вы _не_ должны использовать этот кодмод, если вы уже определили `variant: "outlined"` как вариант по умолчанию в теме.
:::

```js
// ❌ if you have a theme setup like this, don't run this codemod.
// these default props can be removed later because `outlined` is the default value in v5
createMuiTheme({
  components: {
    MuiTextField: {
      defaultProps: {
        variant: 'outlined',
      },
    },
  },
});
```

Если вы хотите сохранить `variant="standard"` в своих компонентах, запустите этот кодмод или настройте соответствующий реквизит темы по умолчанию.

```sh
npx @mui/codemod v5.0.0/variant-prop <path>
```

Более подробную информацию можно найти в [README кодемода variant-prop](https://github.com/mui/material-ui/blob/master/packages/mui-codemod/README.md#variant-prop).

### link-underline-hover <meta data-oversett="" data-original-text="link-underline-hover">

Этот кодмод преобразует компонент `<Link />`, применяя `underline="hover"`, если не определен реквизит `underline` - `underline` по умолчанию изменился с `"hover"` в v4 на `"always"` в v5.

:::error
Вы _не_ должны использовать этот кодмод, если вы уже определили `underline: "always"` как значение по умолчанию в теме.
:::

```js
// if you have theme setup like this, ❌ don't run this codemod.
// this default props can be removed later because `always` is the default value in v5
createMuiTheme({
  components: {
    MuiLink: {
      defaultProps: {
        underline: 'always',
      },
    },
  },
});
```

Если вы хотите сохранить `underline="hover"`, запустите этот кодмод или настройте соответствующий реквизит темы по умолчанию.

```sh
npx @mui/codemod v5.0.0/link-underline-hover <path>
```

Для получения более подробной информации ознакомьтесь с [README кодемода link-underline-hover](https://github.com/mui/material-ui/blob/master/packages/mui-codemod/README.md#link-underline-hover).

## Устранение нежелательных изменений <meta data-oversett="" data-original-text="Address breaking changes">

Комоды справляются со многими изменениями, но другие необходимо устранять вручную.

Независимо от того, решите вы использовать кодовые модули или нет, теперь вы готовы перейти к первому из двух документов, касающихся [изменений](/material-ui/migration/v5-style-changes/).
