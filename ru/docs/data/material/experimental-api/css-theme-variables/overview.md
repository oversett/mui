

# Переменные темы CSS <meta data-oversett="" data-original-text="CSS theme variables">

<p class="description">Обзор применения переменных тем CSS в Material UI.</p>

[Переменные CSS](https://www.w3.org/TR/css-variables-1/) - это современная кроссбраузерная функция, которая позволяет объявлять переменные в CSS и повторно использовать их в других свойствах. Вы можете использовать их для улучшения тематизации и настройки Material UI.

:::info
Если вы впервые сталкиваетесь с переменными CSS, вам следует ознакомиться с [веб-документами MDN по пользовательским свойствам CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties), прежде чем продолжать.
:::

## Введение <meta data-oversett="" data-original-text="Introduction">

Поддержка переменных тем CSS - это новая функция в Material UI, добавленная в версии [`v5.6.0`](https://github.com/mui/material-ui/releases/tag/v5.6.0) (но не включена по умолчанию). Она указывает компонентам Material UI использовать сгенерированные переменные темы CSS вместо необработанных значений.

## Преимущества <meta data-oversett="" data-original-text="Advantages">

-   Это позволяет предотвратить [мерцание SSR в темном режиме](https://github.com/mui/material-ui/issues/27651).
-   Вы можете создавать неограниченные цветовые схемы, помимо `light` и `dark`.
-   Это улучшает отладку не только для разработчиков, но и для дизайнеров вашей команды.
-   Цветовая схема вашего сайта автоматически синхронизируется между вкладками браузера.
-   Это упрощает интеграцию со сторонними инструментами, поскольку переменные темы CSS доступны глобально.
-   Это уменьшает необходимость во вложенной теме, когда вы хотите применить темные стили к определенной части вашего приложения.

## Компромиссы <meta data-oversett="" data-original-text="Trade-offs">

Для приложений на стороне сервера необходимо учитывать некоторые компромиссы:

|     | Сравнение с методом по умолчанию | Причина |
| --- | --- | --- |
| Размер HTML | Больше | Переменные CSS генерируются для светлого и темного режима во время сборки. |
| [First Contentful Paint (FCP)](https://web.dev/fcp/) | Больше | Поскольку размер HTML обычно больше, время загрузки HTML перед показом содержимого больше. |
| [Время до интерактивности (TTI)](https://web.dev/tti/) | Меньше (для темного режима) | Таблицы стилей не регенерируются между светлым и темным режимом, поэтому для выполнения JavaScript требуется меньше времени. |

:::warning
Сравнение, описанное в таблице выше, может быть неприменимо к большим и сложным приложениям, поскольку существует очень много факторов, которые могут влиять на показатели производительности.
:::

## Ментальная модель <meta data-oversett="" data-original-text="Mental model">

Принятие переменных CSS требует некоторых изменений в вашей ментальной модели тематизации и настройки выбранных пользователем режимов.

### Цвета <meta data-oversett="" data-original-text="Colors">

**[Подход по умолчанию](/material-ui/customization/dark-mode/)**: Светлые и темные цвета создаются отдельно.

```js
const lightTheme = createTheme();

const darkTheme = createTheme({
  palette: {
    mode: 'dark',
  },
});
```

**Переменные темы CSS**: Светлые и темные цвета объединяются в тему.

```js
// `extendTheme` is a new API
const theme = extendTheme({
  colorSchemes: {
    light: { // palette for light mode
      palette: {...}
    },
    dark: { // palette for dark mode
      palette: {...}
    }
  }
})
```

### Стилизация <meta data-oversett="" data-original-text="Styling">

**Подход по умолчанию**: Обычно полагается на JavaScript для переключения значения между режимами:

```js
createTheme({
  components: {
    MuiButton: {
      styleOverrides: {
        root: ({ theme }) => ({
          // use javascript conditional expression
          color: theme.palette.mode === 'dark' ? '#fff' : theme.palette.primary.main,
        }),
      },
    },
  },
});
```

**Переменные темы CSS**: Стилизация склоняется к каскадированию и конкретизации, используя соответствующий селектор, который позволяет предотвратить [мерцание SSR в темном режиме](https://github.com/mui/material-ui/issues/27651):

```js
extendTheme({
  components: {
    MuiButton: {
      styleOverrides: {
        root: ({ theme }) => ({
          color: theme.vars.palette.primary.main,
          // When the mode switches to dark, the attribute selector is attached to
          // the <html> tag by default.
          '[data-mui-color-scheme="dark"] &': {
            color: '#fff',
          },
        }),
      },
    },
  },
});
```

## Что дальше <meta data-oversett="" data-original-text="What's next">

-   Чтобы начать новый проект с переменными тем CSS, ознакомьтесь с [руководством по базовому использованию](/material-ui/experimental-api/css-theme-variables/usage/).
-   Для существующего проекта Material UI ознакомьтесь с [руководством по миграции](/material-ui/experimental-api/css-theme-variables/migration/).
-   Для создания и настройки тем ознакомьтесь с [руководством](/material-ui/experimental-api/css-theme-variables/customization/) по использованию.
