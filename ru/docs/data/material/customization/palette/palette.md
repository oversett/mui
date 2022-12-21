

# Палитра <meta data-oversett="" data-original-text="Palette">

<p class="description">Палитра позволяет изменять цвет компонентов в соответствии с вашим брендом.</p>

## Цвета палитры <meta data-oversett="" data-original-text="Palette colors">

Тема предоставляет следующие цвета палитры (доступны по ссылке `theme.palette.`):

-   _основной_ - используется для представления основных элементов интерфейса для пользователя. Это цвет, который чаще всего отображается на экранах и компонентах вашего приложения.
-   _вторичный_ - используется для представления вторичных элементов интерфейса для пользователя. Он предоставляет больше способов подчеркнуть и выделить ваш продукт. Его наличие необязательно.
-   _ошибка_ - используется для обозначения элементов интерфейса, на которые пользователь должен обратить внимание.
-   _предупреждение_ - используется для представления потенциально опасных действий или важных сообщений.
-   _info_ - используется для представления пользователю информации, которая является нейтральной и не обязательно важной.
-   _success_ - используется для обозначения успешного завершения действия, которое было инициировано пользователем.

Если вы хотите узнать больше о цвете, вы можете ознакомиться с [разделом "Цвет](/material-ui/customization/color/)".

## Значения по умолчанию <meta data-oversett="" data-original-text="Default values">

Вы можете изучить значения палитры по умолчанию с помощью [проводника тем](/material-ui/customization/default-theme/?expand-path=$.palette) или открыв консоль dev tools на этой странице (`window.theme.palette`).

{{"demo": "Intentions.js", "bg": "inline", "hideToolbar": true}}

Палитра по умолчанию использует оттенки с префиксом `A` (`A200`, и т.д.) для вторичного цвета палитры, а для остальных цветов палитры - оттенки без префиксов.

## Персонализация <meta data-oversett="" data-original-text="Customization">

Вы можете переопределить значения палитры по умолчанию, включив объект палитры как часть вашей темы. Если любой из объектов:

-   [`.palette.primary`](/material-ui/customization/default-theme/?expand-path=$.palette.primary)
-   [`.palette.secondary`](/material-ui/customization/default-theme/?expand-path=$.palette.secondary)
-   [`.palette.error`](/material-ui/customization/default-theme/?expand-path=$.palette.error)
-   [`.palette.warning`](/material-ui/customization/default-theme/?expand-path=$.palette.warning)
-   [`.palette.info`](/material-ui/customization/default-theme/?expand-path=$.palette.info)
-   [`.palette.success`](/material-ui/customization/default-theme/?expand-path=$.palette.success)

объектов цвета палитры, то они заменят значения по умолчанию.

Значение цвета палитры может быть либо объектом [цвета](/material-ui/customization/color/#2014-material-design-color-palettes), либо объектом с одним или несколькими ключами, указанными в следующем интерфейсе TypeScript:

```ts
interface PaletteColor {
  light?: string;
  main: string;
  dark?: string;
  contrastText?: string;
}
```

### Использование объекта цвета <meta data-oversett="" data-original-text="Using a color object">

Самый простой способ настроить цвет палитры - импортировать один или несколько предоставленных цветов и применить их:

```js
import { createTheme } from '@mui/material/styles';
import blue from '@mui/material/colors/blue';

const theme = createTheme({
  palette: {
    primary: blue,
  },
});
```

### Предоставление цветов напрямую <meta data-oversett="" data-original-text="Providing the colors directly">

Если вы хотите предоставить более настраиваемые цвета, вы можете либо создать свой собственный цвет палитры, либо напрямую предоставить цвета некоторым или всем ключам `theme.palette`:

```js
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: {
      // light: will be calculated from palette.primary.main,
      main: '#ff4400',
      // dark: will be calculated from palette.primary.main,
      // contrastText: will be calculated to contrast with palette.primary.main
    },
    secondary: {
      light: '#0066ff',
      main: '#0044ff',
      // dark: will be calculated from palette.secondary.main,
      contrastText: '#ffcc00',
    },
    // Provide every color token (light, main, dark, and contrastText) when using
    // custom colors for props in Material UI's components.
    // Then you will be able to use it like this: `<Button color="custom">`
    // (For TypeScript, you need to add module augmentation for the `custom` value)
    custom: {
      light: '#ffa726',
      main: '#f57c00',
      dark: '#ef6c00',
      contrastText: 'rgba(0, 0, 0, 0.87)',
    },
    // Used by `getContrastText()` to maximize the contrast between
    // the background and the text.
    contrastThreshold: 3,
    // Used by the functions below to shift a color's luminance by approximately
    // two indexes within its tonal palette.
    // E.g., shift from Red 500 to Red 300 or Red 700.
    tonalOffset: 0.2,
  },
});
```

Как и в примере выше, если цвет палитры содержит пользовательские цвета, использующие любой из ключей "main", "light", "dark" или "contrastText", они отображаются следующим образом:

-   Если ключи "dark" и/или "light" опущены, их значение(я) будет вычислено из "main", в соответствии со значением "tonalOffset".
-   Если "contrastText" опущен, его значение будет рассчитано для контраста с "основным" в соответствии со значением "contrastThreshold".

Значения "tonalOffset" и "contrastThreshold" могут быть настроены по необходимости. Значение "tonalOffset" может быть либо числом от 0 до 1, которое будет применяться как к светлым, так и к темным вариантам, либо объектом со светлыми и темными вариантами, заданными следующим типом TypeScript:

```ts
type PaletteTonalOffset =
  | number
  | {
      light: number;
      dark: number;
    };
```

Более высокое значение для "tonalOffset" сделает вычисленные значения для "light" светлее, а "dark" темнее. Более высокое значение для "contrastThreshold" увеличивает точку, в которой цвет фона считается светлым, и ему присваивается темный "contrastText". Обратите внимание, что "contrastThreshold" следует нелинейной кривой и начинается со значения 3 (требующего минимального соотношения контрастности 3:1).

### Доступность <meta data-oversett="" data-original-text="Accessibility">

Чтобы обеспечить минимальную контрастность не менее 4,5:1, как определено в [правиле 1.4.3 стандарта WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html), создайте пользовательскую тему с помощью `contrastThreshold: 4.5`.

```js
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    // Used by `getContrastText()` to maximize the contrast between
    // the background and the text.
    contrastThreshold: 4.5,
  },
});
```

### Пример <meta data-oversett="" data-original-text="Example">

{{"demo": "Palette.js", "defaultCodeOpen": true}}

### Добавление новых цветов <meta data-oversett="" data-original-text="Adding new colors">

Вы можете добавлять новые цвета внутри и вне палитры темы следующим образом:

```js
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  status: {
    danger: '#e53e3e',
  },
  palette: {
    primary: {
      main: '#0971f1',
      darker: '#053e85',
    },
    neutral: {
      main: '#64748B',
      contrastText: '#fff',
    },
  },
});
```

Если вы используете TypeScript, вам также необходимо использовать [расширение модуля](/material-ui/guides/typescript/#customization-of-theme), чтобы тема принимала указанные выше значения.

```ts
declare module '@mui/material/styles' {
  interface Theme {
    status: {
      danger: React.CSSProperties['color'];
    };
  }

  interface Palette {
    neutral: Palette['primary'];
  }

  interface PaletteOptions {
    neutral: PaletteOptions['primary'];
  }

  interface PaletteColor {
    darker?: string;
  }

  interface SimplePaletteColorOptions {
    darker?: string;
  }

  interface ThemeOptions {
    status: {
      danger: React.CSSProperties['color'];
    };
  }
}
```

{{"demo": "CustomColor.js"}}

## Выбор цветов <meta data-oversett="" data-original-text="Picking colors">

Нужно вдохновение? Команда Material Design создала [инструмент настройки палитры](/material-ui/customization/color/#picking-colors), который поможет вам.

## Темный режим <meta data-oversett="" data-original-text="Dark mode">

Подробную информацию о том, как настроить темный режим для вашей темы, можно найти в [руководстве по темному режиму](/material-ui/customization/dark-mode/).
