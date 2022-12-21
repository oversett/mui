

# Плотность <meta data-oversett="" data-original-text="Density">

<p class="description">Как применить плотность к компонентам MUI.</p>

## Применение плотности <meta data-oversett="" data-original-text="Applying density">

Этот раздел объясняет, как применять плотность. В нем не рассматриваются потенциальные случаи использования или соображения по поводу применения плотности в вашем приложении. В руководстве по Material Design есть [исчерпывающее руководство](https://m2.material.io/design/layout/applying-density.html), в котором эти темы рассматриваются более подробно.

## Применение плотности <meta data-oversett="" data-original-text="Implementing density">

Повышенная плотность может быть применена к некоторым компонентам с помощью реквизитов. На страницах компонентов есть как минимум один пример использования соответствующего компонента с повышенной плотностью.

В зависимости от компонента, плотность применяется либо за счет уменьшения интервалов, либо просто за счет уменьшения размера.

Следующие компоненты имеют реквизиты, применяющие повышенную плотность:

-   [Кнопка](/material-ui/api/button/)
-   [Фаб](/material-ui/api/fab/)
-   [FilledInput](/material-ui/api/filled-input/)
-   [FormControl](/material-ui/api/form-control/)
-   [FormHelperText](/material-ui/api/form-helper-text/)
-   [IconButton](/material-ui/api/icon-button/)
-   [InputBase](/material-ui/api/input-base/)
-   [InputLabel](/material-ui/api/input-label/)
-   [ListItem](/material-ui/api/list-item/)
-   [OutlinedInput](/material-ui/api/outlined-input/)
-   [Таблица](/material-ui/api/table/)
-   [Текстовое поле](/material-ui/api/text-field/)
-   [Панель инструментов](/material-ui/api/toolbar/)

## Изучение плотности темы <meta data-oversett="" data-original-text="Explore theme density">

Этот инструмент позволяет применять плотность с помощью интервалов и реквизитов компонентов. Вы можете просмотреть, как это влияет на общее восприятие компонентов MUI.

Если вы включите высокую плотность, к документам будет применена пользовательская тема. Эта тема предназначена только для демонстрации. _Не следует_ применять эту тему ко всему приложению, так как это может негативно сказаться на пользовательском опыте. В [руководстве по Material Design](https://m2.material.io/design/layout/applying-density.html) есть примеры того, когда не следует применять плотность.

Тема настраивается с помощью следующих параметров:

```js
const theme = createTheme({
  components: {
    MuiButton: {
      defaultProps: {
        size: 'small',
      },
    },
    MuiFilledInput: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiFormControl: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiFormHelperText: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiIconButton: {
      defaultProps: {
        size: 'small',
      },
    },
    MuiInputBase: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiInputLabel: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiListItem: {
      defaultProps: {
        dense: true,
      },
    },
    MuiOutlinedInput: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiFab: {
      defaultProps: {
        size: 'small',
      },
    },
    MuiTable: {
      defaultProps: {
        size: 'small',
      },
    },
    MuiTextField: {
      defaultProps: {
        margin: 'dense',
      },
    },
    MuiToolbar: {
      defaultProps: {
        variant: 'dense',
      },
    },
  },
});
```

{{"demo": "DensityTool.js", "hideToolbar": true}}
