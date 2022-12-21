

# Компоненты <meta data-oversett="" data-original-text="Components">

<p class="description">Вы можете настроить стили компонента, реквизиты по умолчанию и многое другое, используя его ключи в теме. Это помогает достичь согласованности стилей во всем приложении.</p>

## Реквизиты по умолчанию <meta data-oversett="" data-original-text="Default props">

Каждый компонент Material UI имеет предустановленные значения по умолчанию для каждого из своих реквизитов. Чтобы изменить эти значения по умолчанию, используйте ключ `defaultProps`, открытый в ключе темы `components`:

```js
const theme = createTheme({
  components: {
    // Name of the component
    MuiButtonBase: {
      defaultProps: {
        // The props to change the default for.
        disableRipple: true, // No more ripple, on the whole application 💣!
      },
    },
  },
});
```

{{"demo": "DefaultProps.js"}}

Если вы используете TypeScript и [лабораторные компоненты](/material-ui/about-the-lab/), ознакомьтесь с [этой статьей, чтобы узнать, как переопределить их стили](/material-ui/about-the-lab/#typescript).

## Глобальные переопределения стилей <meta data-oversett="" data-original-text="Global style overrides">

Ключ `styleOverrides` темы позволяет потенциально изменить каждый стиль, внедряемый Material UI в DOM. Это полезно, если вы хотите применить полностью индивидуальную систему дизайна к компонентам Material UI.

```js
const theme = createTheme({
  components: {
    // Name of the component
    MuiButton: {
      styleOverrides: {
        // Name of the slot
        root: {
          // Some CSS
          fontSize: '1rem',
        },
      },
    },
  },
});
```

{{"demo": "GlobalThemeOverride.js"}}

Каждый компонент состоит из нескольких различных частей. Эти части соответствуют классам, которые доступны компоненту - подробный список смотрите в разделе **CSS** на странице API компонента. Вы можете использовать эти классы внутри ключа `styleOverrides` для изменения соответствующих частей компонента.

```js
const theme = createTheme({
  components: {
    MuiButton: {
      styleOverrides: {
        root: ({ ownerState }) => ({
          ...(ownerState.variant === 'contained' &&
            ownerState.color === 'primary' && {
              backgroundColor: '#202020',
              color: '#fff',
            }),
        }),
      },
    },
  },
});
```

### Переопределения на основе реквизитов <meta data-oversett="" data-original-text="Overrides based on props">

Вы можете передать обратный вызов в качестве значения в каждый слот компонента `styleOverrides` для применения стилей на основе реквизитов.

Реквизит `ownerState` представляет собой комбинацию публичных реквизитов, которые вы передаете компоненту + внутреннее состояние компонента.

```js
const finalTheme = createTheme({
  components: {
    MuiSlider: {
      styleOverrides: {
        valueLabel: ({ ownerState, theme }) => ({
          ...(ownerState.orientation === 'vertical' && {
            backgroundColor: 'transparent',
            color: theme.palette.grey[500],
          }),
        }),
      },
    },
  },
});
```

{{"demo": "GlobalThemeOverrideCallback.js"}}

### Синтаксис `sx` (экспериментальный) <meta data-oversett="" data-original-text="The sx syntax (experimental)">

Реквизит `sx` служит в качестве ярлыка для определения пользовательских стилей, обращающихся к объекту темы. Этот реквизит позволяет писать встроенные стили, используя супермножество CSS. Узнайте больше о [концепции, лежащей в основе реквизита `sx`](/system/getting-started/the-sx-prop/) , и о том [, чем `sx` отличается от утилиты `styled`](/system/styled/#difference-with-the-sx-prop) .

Вы можете использовать реквизит `sx` внутри ключа `styleOverrides` для изменения стилей в теме с помощью сокращенной нотации CSS. Это особенно удобно, если вы уже используете реквизит `sx` в своих компонентах, поскольку вы можете использовать тот же синтаксис в своей теме и быстро переносить стили между ними.

:::info
Реквизит `sx` является стабильной функцией для настройки компонентов в Material UI v5, но он все еще считается _экспериментальным_, если используется непосредственно внутри объекта темы.
:::

{{"demo": "GlobalThemeOverrideSx.js", "defaultCodeOpen": false}}

```tsx
const finalTheme = createTheme({
  components: {
    MuiChip: {
      styleOverrides: {
        root: ({ theme }) =>
          theme.unstable_sx({
            px: 1,
            py: 0.25,
            borderRadius: 1,
          }),
        label: {
          padding: 'initial',
        },
        icon: ({ theme }) =>
          theme.unstable_sx({
            mr: 0.5,
            ml: '-2px',
          }),
      },
    },
  },
});
```

### Специфика <meta data-oversett="" data-original-text="Specificity">

Если вы используете подход тематизации для настройки компонентов, вы все равно сможете переопределить их с помощью реквизита `sx`, поскольку он имеет более высокую специфичность CSS, даже если вы используете экспериментальный синтаксис `sx` внутри темы.

## Создание новых вариантов компонентов <meta data-oversett="" data-original-text="Creating new component variants">

Вы можете использовать ключ `variants` в разделе темы `components` для создания новых вариантов компонентов Material UI. Эти новые варианты могут определять, какие стили должны быть у компонента, когда применяется конкретное значение параметра варианта.

Варианты указываются в массиве под именем компонента. Для каждого из них в HTML добавляется CSS-класс `<head>`. Порядок важен, поэтому убедитесь, что стили, которые должны победить, указаны последними.

```js
const theme = createTheme({
  components: {
    MuiButton: {
      variants: [
        {
          props: { variant: 'dashed' },
          style: {
            textTransform: 'none',
            border: `2px dashed ${blue[500]}`,
          },
        },
        {
          props: { variant: 'dashed', color: 'secondary' },
          style: {
            border: `4px dashed ${red[500]}`,
          },
        },
      ],
    },
  },
});
```

Если вы используете TypeScript, вам нужно будет указать новые варианты/цвета, используя [дополнения модуля](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#module-augmentation).

```tsx
declare module '@mui/material/Button' {
  interface ButtonPropsVariantOverrides {
    dashed: true;
  }
}
```

{{"demo": "GlobalThemeVariants.js"}}

## Переменные темы <meta data-oversett="" data-original-text="Theme variables">

Другой способ переопределить внешний вид всех экземпляров компонента - настроить [переменные конфигурации темы](/material-ui/customization/theming/#theme-configuration-variables).

```js
const theme = createTheme({
  typography: {
    button: {
      fontSize: '1rem',
    },
  },
});
```

{{"demo": "ThemeVariables.js"}}
