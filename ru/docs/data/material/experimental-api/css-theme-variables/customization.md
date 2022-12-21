

# Переменные темы CSS - Настройка <meta data-oversett="" data-original-text="CSS theme variables - Customization">

<p class="description">Руководство по настройке переменных темы CSS в Material UI.</p>

## Тематика <meta data-oversett="" data-original-text="Theming">

`experimental_extendTheme` это API, который расширяет тему по умолчанию. Он возвращает тему, которая может быть использована только `Experimental_CssVarsProvider`.

```js
import {
  Experimental_CssVarsProvider as CssVarsProvider,
  experimental_extendTheme as extendTheme,
} from '@mui/material/styles';

const theme = extendTheme();
// ...custom theme

function App() {
  return <CssVarsProvider theme={theme}>...</CssVarsProvider>;
}
```

:::warning
`extendTheme` это не то же самое, что [`createTheme`](/material-ui/customization/theming/#createtheme-options-args-theme). Не используйте их взаимозаменяемо.

-   `createTheme()` возвращает тему для `ThemeProvider`.
-   `extendTheme()` возвращает тему для `CssVarsProvider`.
:::

### Цветовые схемы <meta data-oversett="" data-original-text="Color schemes">

Основное отличие от подхода по умолчанию заключается в настройке палитры. С помощью API `extendTheme` вы можете задать палитру сразу для всех цветовых схем (`light` и `dark` встроены) в узле `colorSchemes`.

Вот пример того, как настроить палитру `primary`:

```js
import { pink } from '@mui/material/colors';

const theme = extendTheme({
  colorSchemes: {
    light: {
      palette: {
        primary: {
          main: pink[600],
        },
      },
    },
    dark: {
      palette: {
        primary: {
          main: pink[400],
        },
      },
    },
  },
});
```

### Компоненты <meta data-oversett="" data-original-text="Components">

[Настройка компонентов](/material-ui/customization/theme-components/) остается такой же, как и по умолчанию. Мы рекомендуем использовать значение из `theme.vars.*`, когда это возможно, для лучшего опыта отладки:

```js
const theme = extendTheme({
  components: {
    MuiChip: {
      styleOverrides: {
        root: ({ theme, ownerState }) => ({
          ...(ownerState.variant === 'outlined' &&
            ownerState.color === 'primary' && {
              // this is the same as writing:
              // backgroundColor: 'var(--mui-palette-background-paper)',
              backgroundColor: theme.vars.palette.background.paper,
            }),
        }),
      },
    },
  },
});
```

### Канальные маркеры <meta data-oversett="" data-original-text="Channel tokens">

Канальный маркер - это переменная, состоящая из [каналов цветового пространства](https://www.w3.org/TR/css-color-4/#color-syntax), но без альфа-компонента. Значение канального маркера разделяется пробелом, например, `12 223 31`, который можно комбинировать с [цветовыми функциями](https://www.w3.org/TR/css-color-4/#color-functions) для создания полупрозрачного цвета.

`extendTheme()` автоматически генерирует маркеры каналов, которые, вероятно, будут часто использоваться, из палитры тем. Эти цвета имеют суффикс `Channel`, например:

```js
const theme = extendTheme();
const light = theme.colorSchemes.light;

console.log(light.palette.primary.mainChannel); // '25 118 210'
// This token is generated from `theme.colorSchemes.light.palette.primary.main`.
```

Вы можете использовать маркеры каналов для создания полупрозрачного цвета следующим образом:

```js
const theme = extendTheme({
  components: {
    MuiChip: {
      styleOverrides: {
        root: ({ theme, ownerState }) => ({
          ...(ownerState.variant === 'outlined' &&
            ownerState.color === 'primary' && {
              backgroundColor: `rgba(${theme.vars.palette.primary.mainChannel} / 0.12)`,
            }),
        }),
      },
    },
  },
});
```

:::warning
Не используйте запятую (`,`) в качестве разделителя, потому что цвета каналов используют пустые пробелы для определения [прозрачности](https://www.w3.org/TR/css-color-4/#transparency):

```js
`rgba(${theme.vars.palette.primary.mainChannel}, 0.12)`, // 🚫 this does not work
`rgba(${theme.vars.palette.primary.mainChannel} / 0.12)`, // ✅ always use `/`
```
:::

## Добавление новых маркеров тем <meta data-oversett="" data-original-text="Adding new theme tokens">

Вы можете добавить другие пары ключ-значение во входные данные темы, которые будут сгенерированы как часть переменных темы CSS:

```js
const theme = extendTheme({
  colorSchemes: {
    light: {
      palette: {
        // The best part is that you can refer to the variables wherever you like 🤩
        gradient:
          'linear-gradient(to left, var(--mui-palete-primary-main), var(--mui-palette-primary-dark))',
        border: {
          subtle: 'var(--mui-palette-neutral-200)',
        },
      },
    },
    dark: {
      palette: {
        gradient:
          'linear-gradient(to left, var(--mui-palete-primary-light), var(--mui-palette-primary-main))',
        border: {
          subtle: 'var(--mui-palette-neutral-600)',
        },
      },
    },
  },
});

function App() {
  return <CssVarsProvider theme={theme}>...</CssVarsProvider>;
}
```

Затем вы можете получить доступ к этим переменным из объекта `theme.vars`:

```js
const Divider = styled('hr')(({ theme }) => ({
  height: 1,
  border: '1px solid',
  borderColor: theme.vars.palette.border.subtile,
  backgroundColor: theme.vars.palette.gradient,
}));
```

Или используйте `var()` для прямого обращения к переменной CSS:

```css
/* global.css */
.external-section {
  background-color: var(--mui-palette-gradient);
}
```

:::warning
Если вы используете [пользовательский префикс](/material-ui/experimental-api/css-theme-variables/customization/#changing-variable-prefixes), не забудьте заменить стандартный `--mui`.
:::

### TypeScript <meta data-oversett="" data-original-text="TypeScript">

Вы должны дополнить палитру тем, чтобы избежать ошибок типа:

```ts
declare module '@mui/material/styles' {
  interface PaletteOptions {
    gradient: string;
    border: {
      subtle: string;
    };
  }
  interface Palette {
    gradient: string;
    border: {
      subtle: string;
    };
  }
}
```

## Изменение префиксов переменных <meta data-oversett="" data-original-text="Changing variable prefixes">

Чтобы изменить префикс переменной по умолчанию (`--mui`), укажите строку в свойстве `cssVarPrefix`, как показано ниже:

```js
const theme = extendTheme({ cssVarPrefix: 'any' });

// the stylesheet will be like this:
// --any-palette-primary-main: ...;
```

Чтобы удалить префикс, используйте в качестве значения пустую строку:

```js
const theme = extendTheme({ cssVarPrefix: '' });

// the stylesheet will be like this:
// --palette-primary-main: ...;
```

## Пользовательские стили для каждого режима <meta data-oversett="" data-original-text="Custom styles per mode">

Чтобы настроить стиль без создания новых токенов, вы можете воспользоваться утилитой `theme.getColorSchemeSelector`:

```js
const Button = styled('button')(({ theme }) => ({
  // in default mode.
  backgroundColor: theme.vars.palette.primary.main,
  color: '#fff',
  '&:hover': {
    backgroundColor: theme.vars.palette.primary.dark,
  },

  // in dark mode.
  [theme.getColorSchemeSelector('dark')]: {
    backgroundColor: theme.vars.palette.primary.dark,
    color: theme.vars.palette.primary.main,
    '&:hover': {
      color: '#fff',
      backgroundColor: theme.vars.palette.primary.dark,
    },
  },
}));
```

:::info
Использование этой утилиты эквивалентно написанию простой строки `'[data-mui-color-scheme="dark"] &'`, если у вас нет пользовательской конфигурации.
:::

## Принудительное использование определенной цветовой схемы <meta data-oversett="" data-original-text="Force a specific color scheme">

Укажите `data-mui-color-scheme="dark"` для любого узла DOM, чтобы заставить дочерние компоненты отображаться так, как будто они находятся в темном режиме.

```js
<div data-mui-color-scheme="dark">
  <Paper sx={{ p: 2 }}>
    <TextField label="Email" type="email" margin="normal" />
    <TextField label="Password" type="password" margin="normal" />
    <Button>Sign in</Button>
  </Paper>
</div>
```

## Приложение с темной цветовой схемой <meta data-oversett="" data-original-text="Dark color scheme application">

Для приложения, которое имеет только темный режим, установите режим по умолчанию `dark`:

```js
const theme = extendTheme({
  // ...
});

// remove the `light` color scheme to optimize the HTML size for server-side application
delete theme.colorSchemes.light;

function App() {
  return (
    <CssVarsProvider theme={theme} defaultMode="dark">
      ...
    </CssVarsProvider>
  );
}
```

Для приложения на стороне сервера задайте одинаковое значение для. [`getInitColorSchemeScript()`](/material-ui/experimental-api/css-theme-variables/usage/#server-side-rendering):

```js
getInitColorSchemeScript({
  defaultMode: 'dark',
});
```

:::warning
При разработке обязательно очистите локальное хранилище и обновите страницу после настройки `defaultMode`.
:::
