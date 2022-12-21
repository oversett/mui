

# Точки останова <meta data-oversett="" data-original-text="Breakpoints">

<p class="description">API, позволяющий использовать точки останова в самых разных контекстах.</p>

Для оптимального пользовательского опыта интерфейсы Material Design должны иметь возможность адаптировать свой макет в различных точках останова. MUI использует **упрощенную** реализацию оригинальной [спецификации](https://m2.material.io/design/layout/responsive-layout-grid.html#breakpoints).

Точки останова используются внутри различных компонентов, чтобы сделать их отзывчивыми, но вы также можете воспользоваться ими для управления макетом вашего приложения с помощью компонента [Grid](/material-ui/react-grid/).

## Точки останова по умолчанию <meta data-oversett="" data-original-text="Default breakpoints">

Каждая точка останова (ключ) соответствует _фиксированной_ ширине экрана (значение):

-   **xs,** extra-small: 0px
-   **sm,** маленький: 600px
-   **md,** средний: 900px
-   **lg,** большой: 1200px
-   **xl,** extra-large: 1536px

Эти значения могут быть [настроены](#custom-breakpoints).

## Медиазапросы CSS <meta data-oversett="" data-original-text="CSS Media Queries">

Медиа-запросы CSS - это идиоматический подход, позволяющий сделать ваш пользовательский интерфейс отзывчивым. Тема предоставляет пять стилей-помощников для этого:

-   [theme.breakpoints.up(key)](#theme-breakpoints-up-key-media-query)
-   [theme.breakpoints.down(key)](#theme-breakpoints-down-key-media-query)
-   [theme.breakpoints.only(key)](#theme-breakpoints-only-key-media-query)
-   [theme.breakpoints.not(key)](#theme-breakpoints-not-key-media-query)
-   [theme.breakpoints.between(start, end)](#theme-breakpoints-between-start-end-media-query)

В следующем демонстрационном примере мы изменяем цвет фона (красный, синий и зеленый) в зависимости от ширины экрана.

```jsx
const styles = (theme) => ({
  root: {
    padding: theme.spacing(1),
    [theme.breakpoints.down('md')]: {
      backgroundColor: theme.palette.secondary.main,
    },
    [theme.breakpoints.up('md')]: {
      backgroundColor: theme.palette.primary.main,
    },
    [theme.breakpoints.up('lg')]: {
      backgroundColor: green[500],
    },
  },
});
```

{{"demo": "MediaQuery.js"}}

## Медиазапросы JavaScript <meta data-oversett="" data-original-text="JavaScript Media Queries">

Иногда использования CSS недостаточно. Вы можете захотеть изменить дерево рендеринга React на основе значения точки останова в JavaScript.

### хук useMediaQuery <meta data-oversett="" data-original-text="useMediaQuery hook">

Вы можете узнать больше на странице [useMediaQuery](/material-ui/react-use-media-query/).

## Пользовательские точки останова <meta data-oversett="" data-original-text="Custom breakpoints">

Вы определяете точки останова вашего проекта в разделе `theme.breakpoints` вашей темы.

-   [`theme.breakpoints.values`](/material-ui/customization/default-theme/?expand-path=$.breakpoints.values): [Значения](#default-breakpoints) по умолчанию. Ключи - это ваши экранные имена, а значения - минимальная ширина, с которой должна начинаться точка останова.
-   `theme.breakpoints.unit`: По умолчанию `'px'`. Единица измерения, используемая для значений точки останова.
-   `theme.breakpoints.step`: По умолчанию `5`. Приращение, деленное на 100, используемое для реализации эксклюзивных точек останова. Например, `{ step: 5 }` означает, что `down(500)` приведет к `'(max-width: 499.95px)'`.

Если вы измените значения точек останова по умолчанию, вам необходимо указать их все:

```jsx
const theme = createTheme({
  breakpoints: {
    values: {
      xs: 0,
      sm: 600,
      md: 900,
      lg: 1200,
      xl: 1536,
    },
  },
});
```

Не стесняйтесь иметь столько точек останова, сколько хотите, и называйте их так, как вам удобно для вашего проекта.

```js
const theme = createTheme({
  breakpoints: {
    values: {
      mobile: 0,
      tablet: 640,
      laptop: 1024,
      desktop: 1200,
    },
  },
});
```

Если вы используете TypeScript, вам также необходимо использовать [расширение модуля](/material-ui/guides/typescript/#customization-of-theme), чтобы тема принимала вышеуказанные значения.

```ts
declare module '@mui/material/styles' {
  interface BreakpointOverrides {
    xs: false; // removes the `xs` breakpoint
    sm: false;
    md: false;
    lg: false;
    xl: false;
    mobile: true; // adds the `mobile` breakpoint
    tablet: true;
    laptop: true;
    desktop: true;
  }
}
```

## API <meta data-oversett="" data-original-text="API">

### `theme.breakpoints.up(key) => media query` <meta data-oversett="" data-original-text="theme.breakpoints.up(key) => media query">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `key` _(строка_ | _число_): Ключ точки останова (`xs`, `sm` и т. д.) или число ширины экрана в px.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`media query`: Строка медиа-запроса, готовая к использованию с большинством решений для стилизации, которая соответствует ширине экрана, превышающей размер экрана, заданный ключом точки останова (включительно).

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
const styles = (theme) => ({
  root: {
    backgroundColor: 'blue',
    // Match [md, ∞)
    //       [900px, ∞)
    [theme.breakpoints.up('md')]: {
      backgroundColor: 'red',
    },
  },
});
```

### `theme.breakpoints.down(key) => media query` <meta data-oversett="" data-original-text="theme.breakpoints.down(key) => media query">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `key` _(строка_ | _число_): Ключ точки останова (`xs`, `sm`, и т.д.) или число ширины экрана в px.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`media query`: Строка медиа-запроса, готовая к использованию с большинством решений для стилизации, которая соответствует ширине экрана, меньшей, чем размер экрана, заданный ключом точки останова (эксклюзивный).

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
const styles = (theme) => ({
  root: {
    backgroundColor: 'blue',
    // Match [0, md)
    //       [0, 900px)
    [theme.breakpoints.down('md')]: {
      backgroundColor: 'red',
    },
  },
});
```

### `theme.breakpoints.only(key) => media query` <meta data-oversett="" data-original-text="theme.breakpoints.only(key) => media query">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `key` _(строка_): Ключ точки останова (`xs`, `sm` и т.д.).

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`media query`: Строка медиазапроса, готовая к использованию с большинством решений для стилизации, которая соответствует ширине экрана, начиная с размера экрана, заданного ключом точки останова (включительно), и заканчивая размером экрана, заданным следующим ключом точки останова (исключая).

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
const styles = (theme) => ({
  root: {
    backgroundColor: 'blue',
    // Match [md, md + 1)
    //       [md, lg)
    //       [900px, 1200px)
    [theme.breakpoints.only('md')]: {
      backgroundColor: 'red',
    },
  },
});
```

### `theme.breakpoints.not(key) => media query` <meta data-oversett="" data-original-text="theme.breakpoints.not(key) => media query">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `key` _(строка_): Ключ точки останова (`xs`, `sm` и т.д.).

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`media query`: Строка медиазапроса, готовая к использованию с большинством решений для стилизации, которая соответствует ширине экрана, останавливаясь на размере экрана, заданном ключом точки останова (исключая), и начиная с размера экрана, заданного следующим ключом точки останова (включая).

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
const styles = (theme) => ({
  root: {
    backgroundColor: 'blue',
    // Match [xs, md) and [md + 1, ∞)
    //       [xs, md) and [lg, ∞)
    //       [0px, 900px) and [1200px, ∞)
    [theme.breakpoints.not('md')]: {
      backgroundColor: 'red',
    },
  },
});
```

### `theme.breakpoints.between(start, end) => media query` <meta data-oversett="" data-original-text="theme.breakpoints.between(start, end) => media query">

#### Аргументы <meta data-oversett="" data-original-text="Arguments">

1.  `start` _(строка_): Ключ точки останова (`xs`, `sm`, и т.д.) или номер ширины экрана в пикселях.
2.  `end` _(строка_): Ключ точки останова (`xs`, `sm`, и т.д.) или номер ширины экрана в пикселях.

#### Возвращает <meta data-oversett="" data-original-text="Returns">

`media query`: Строка медиазапроса, готовая к использованию с большинством решений для стилизации, которая соответствует ширине экрана больше, чем размер экрана, заданный ключом точки останова в первом аргументе (включительно) и меньше, чем размер экрана, заданный ключом точки останова во втором аргументе (исключая).

#### Примеры <meta data-oversett="" data-original-text="Examples">

```js
const styles = (theme) => ({
  root: {
    backgroundColor: 'blue',
    // Match [sm, md)
    //       [600px, 900px)
    [theme.breakpoints.between('sm', 'md')]: {
      backgroundColor: 'red',
    },
  },
});
```

## Значения по умолчанию <meta data-oversett="" data-original-text="Default values">

Вы можете изучить значения точек останова по умолчанию с помощью [проводника тем](/material-ui/customization/default-theme/?expand-path=$.breakpoints) или открыв консоль dev tools на этой странице (`window.theme.breakpoints`).
