

# Тематика <meta data-oversett="" data-original-text="Theming">

<p class="description">Настройте MUI с помощью своей темы. Вы можете изменить цвета, типографику и многое другое.</p>

Тема задает цвет компонентов, темноту поверхностей, уровень тени, соответствующую непрозрачность чернильных элементов и т.д.

Темы позволяют применить единый тон к вашему приложению. Они позволяют **настроить все аспекты дизайна** вашего проекта в соответствии с конкретными потребностями вашего бизнеса или бренда.

Для обеспечения большей согласованности между приложениями на выбор предлагаются светлые и темные темы. По умолчанию компоненты используют светлый тип темы.

## Поставщик темы <meta data-oversett="" data-original-text="Theme provider">

Если вы хотите настроить тему, вам необходимо использовать компонент `ThemeProvider`, чтобы внедрить тему в ваше приложение. Однако это необязательно; компоненты MUI поставляются с темой по умолчанию.

`ThemeProvider` Полагается на [контекстную функцию React](https://reactjs.org/docs/context.html) для передачи темы компонентам, поэтому вам нужно убедиться, что `ThemeProvider` является родителем компонентов, которые вы хотите настроить. Вы можете узнать больше об этом в [разделе API](#themeprovider).

## Переменные конфигурации темы <meta data-oversett="" data-original-text="Theme configuration variables">

Изменение переменных конфигурации темы является наиболее эффективным способом приведения MUI в соответствие с вашими потребностями. В следующих разделах рассматриваются наиболее важные переменные темы:

-   [`.palette`](/material-ui/customization/palette/)
-   [`.typography`](/material-ui/customization/typography/)
-   [`.spacing`](/material-ui/customization/spacing/)
-   [`.breakpoints`](/material-ui/customization/breakpoints/)
-   [`.zIndex`](/material-ui/customization/z-index/)
-   [`.transitions`](/material-ui/customization/transitions/)
-   [`.components`](/material-ui/customization/theme-components/)

Вы можете заглянуть в [раздел "Тема по умолчанию"](/material-ui/customization/default-theme/), чтобы полностью ознакомиться с темой по умолчанию.

### Пользовательские переменные <meta data-oversett="" data-original-text="Custom variables">

При использовании темы MUI с [MUI System](/system/getting-started/overview/) или [любым другим решением для стилизации](/material-ui/guides/interoperability/) может быть удобно добавить дополнительные переменные в тему, чтобы вы могли использовать их везде. Например:

```jsx
const theme = createTheme({
  status: {
    danger: orange[500],
  },
});
```

**WARNING**: `vars` - это приватное поле, используемое для поддержки переменных CSS. При попытке его использования будет выброшена ошибка:

```jsx
createTheme({
  vars: { ... },
})
```

Если вы используете TypeScript, вам также нужно будет использовать [расширение модуля](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation), чтобы тема принимала вышеуказанные значения.

```tsx
declare module '@mui/material/styles' {
  interface Theme {
    status: {
      danger: string;
    };
  }
  // allow configuration using `createTheme`
  interface ThemeOptions {
    status?: {
      danger?: string;
    };
  }
}
```

{{"demo": "CustomStyles.js"}}

## Конструктор тем <meta data-oversett="" data-original-text="Theme builder">

<video autoplay="" muted="" loop="" width="320"><source src="/static/studies.mp4" type="video/mp4"></video>

Сообщество создало отличные инструменты для создания темы:

-   [mui-theme-creator](https://bareynol.github.io/mui-theme-creator/): Инструмент, помогающий создавать и настраивать темы для библиотеки компонентов MUI. Включает базовые шаблоны сайтов, чтобы показать различные компоненты и то, как на них влияет тема.
-   [Генератор палитры материалов](https://m2.material.io/inline-tools/color/): Генератор палитры материалов можно использовать для создания палитры для любого введенного вами цвета.

## Доступ к теме в компоненте <meta data-oversett="" data-original-text="Accessing the theme in a component">

Вы можете получить доступ к переменным темы внутри ваших функциональных компонентов React с помощью хука `useTheme`:

```jsx
import { useTheme } from '@mui/material/styles';

function DeepChild() {
  const theme = useTheme();
  return <span>{`spacing ${theme.spacing}`}</span>;
}
```

## Вложение темы <meta data-oversett="" data-original-text="Nesting the theme">

[Вы можете вложить](/system/styles/advanced/#theme-nesting) несколько провайдеров тем.

{{"demo": "ThemeNesting.js"}}

Внутренняя тема будет **переопределять** внешнюю тему. Вы можете расширить внешнюю тему, предоставив функцию:

{{"demo": "ThemeNestingExtend.js"}}

## API <meta data-oversett="" data-original-text="API">

### `createTheme(options, ...args) => theme` <meta data-oversett="" data-original-text="createTheme(options, ...args) => theme">

Сгенерируйте тему на основе полученных параметров. Затем передайте ее в качестве параметра [`ThemeProvider`](#themeprovider).

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `options` _(объект_): Берет неполный объект темы и добавляет недостающие части.
2.  `...args` _(object\[\]_): Глубокое слияние аргументов с возвращаемой темой.

:::warning
Только первый аргумент (`options`) обрабатывается функцией `createTheme`. Если вы хотите фактически объединить параметры двух тем и создать на их основе новую, вы можете глубоко объединить эти два параметра и предоставить их в качестве первого аргумента функции `createTheme`.
:::

```js
import { deepmerge } from '@mui/utils';
import { createTheme } from '@mui/material/styles';

const theme = createTheme(deepmerge(options1, options2));
```

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`theme` _(объект_): Полный, готовый к использованию объект темы.

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
import { createTheme } from '@mui/material/styles';
import { green, purple } from '@mui/material/colors';

const theme = createTheme({
  palette: {
    primary: {
      main: purple[500],
    },
    secondary: {
      main: green[500],
    },
  },
});
```

#### Композиция тем: использование опций темы для определения других опций <meta data-oversett="" data-original-text="Theme composition: using theme options to define other options">

Когда значение опции темы зависит от другой опции темы, вы должны составлять тему поэтапно.

```js
import { createTheme } from '@mui/material/styles';

let theme = createTheme({
  palette: {
    primary: {
      main: '#0052cc',
    },
    secondary: {
      main: '#edf2ff',
    },
  },
});

theme = createTheme(theme, {
  palette: {
    info: {
      main: theme.palette.secondary.main,
    },
  },
});
```

Рассматривайте создание темы как двухэтапный процесс композиции: сначала вы определяете основные параметры оформления; затем вы будете использовать эти параметры оформления для составления других параметров.

**ВНИМАНИЕ**: `theme.vars` - это частное поле, используемое для поддержки переменных CSS. Пожалуйста, используйте другое имя для пользовательского объекта.

### `responsiveFontSizes(theme, options) => theme` <meta data-oversett="" data-original-text="responsiveFontSizes(theme, options) => theme">

Сгенерировать настройки отзывчивой типографики на основе полученных опций.

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `theme` _(объект_): Объект темы для улучшения.
2.  `options` _(объект_ \[необязательно\]):

-   `breakpoints` _(array<string>_ \[необязательно\]): По умолчанию `['sm', 'md', 'lg']`. Массив [точек останова](/material-ui/customization/breakpoints/) (идентификаторы).
-   `disableAlign` _(bool_ \[необязательно\]): По умолчанию `false`. Следует ли слегка изменять размер шрифта, чтобы высота строк сохранялась и соответствовала сетке высоты строк Material Design 4px. Для этого в стилях темы необходимо задать высоту строк без единиц.
-   `factor` _(число_ \[необязательно\]): По умолчанию `2`. Это значение определяет силу изменения размера шрифта. Чем больше значение, тем меньше разница между размерами шрифтов на маленьких экранах. Чем меньше значение, тем больше размеры шрифтов на маленьких экранах. Значение должно быть больше 1.
-   `variants` _(array<string>_ \[необязательно\]): По умолчанию все. Варианты шрифтов для обработки.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`theme` _(объект_): Новая тема с отзывчивой типографикой.

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
import { createTheme, responsiveFontSizes } from '@mui/material/styles';

let theme = createTheme();
theme = responsiveFontSizes(theme);
```

### `unstable_createMuiStrictModeTheme(options, ...args) => theme` <meta data-oversett="" data-original-text="unstable_createMuiStrictModeTheme(options, ...args) => theme">

**ПРЕДУПРЕЖДЕНИЕ**: Не используйте этот метод в производстве.

Генерирует тему, которая уменьшает количество предупреждений внутри [`React.StrictMode`](https://reactjs.org/docs/strict-mode.html) например, `Warning: findDOMNode is deprecated in StrictMode`.

#### Требования <meta data-oversett="" data-original-text="Requirements">

В настоящее время `unstable_createMuiStrictModeTheme` не добавляет никаких дополнительных требований.

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `options` _(объект_): Берет неполный объект темы и добавляет недостающие части.
2.  `...args` _(object\[\]_): Глубокое объединение аргументов с возвращаемой темой.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`theme` _(объект_): Полный, готовый к использованию объект темы.

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
import { unstable_createMuiStrictModeTheme } from '@mui/material/styles';

const theme = unstable_createMuiStrictModeTheme();

function App() {
  return (
    <React.StrictMode>
      <ThemeProvider theme={theme}>
        <LandingPage />
      </ThemeProvider>
    </React.StrictMode>
  );
}
```

### `ThemeProvider` <meta data-oversett="" data-original-text="ThemeProvider">

Этот компонент принимает реквизит `theme` и применяет его ко всему дереву React, вокруг которого он оборачивается. Предпочтительно использовать его в **корне дерева компонентов**.

#### Реквизит <meta data-oversett="" data-original-text="Props">

| Имя | Тип | Описание |
| --- | --- | --- |
| дети \* | узел | Дерево вашего компонента. |
| тема \* | союз: объект \| func | Объект темы, обычно являющийся результатом [`createTheme()`](#createtheme-options-args-theme). Предоставленная тема будет объединена с темой по умолчанию. Вы можете предоставить функцию для расширения внешней темы. |

#### Примеры <meta data-oversett="" data-original-text="Examples">

```jsx
import * as React from 'react';
import { red } from '@mui/material/colors';
import { ThemeProvider, createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: {
      main: red[500],
    },
  },
});

function App() {
  return <ThemeProvider theme={theme}>...</ThemeProvider>;
}
```
