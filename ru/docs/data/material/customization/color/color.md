

# Цвет <meta data-oversett="" data-original-text="Color">

<p class="description">Передавайте смысл с помощью цвета. Из коробки вы получаете доступ ко всем цветам из руководства по Material Design.</p>

[Система цветов](https://m2.material.io/design/color/) Material Design может быть использована для создания цветовой темы, отражающей ваш бренд или стиль.

## Выбор цветов <meta data-oversett="" data-original-text="Picking colors">

### Официальный инструмент выбора цвета <meta data-oversett="" data-original-text="Official color tool">

Команда Material Design также создала потрясающий инструмент настройки палитры: [material.io/resources/color/](https://m2.material.io/resources/color/). Он поможет вам создать цветовую палитру для вашего пользовательского интерфейса, а также измерить уровень доступности любой цветовой комбинации.

<a href="https://m2.material.io/resources/color/#!/?view.left=0&amp;view.right=0&amp;primary.color=3F51B5&amp;secondary.color=F44336" target="_blank" rel="noopener nofollow"><img src="/static/images/color/colorTool.png" alt="Official color tool" style="width: 574px"></a>\
\

Полученные результаты можно передать в функцию `createTheme()`:

```js
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: {
      light: '#757ce8',
      main: '#3f50b5',
      dark: '#002884',
      contrastText: '#fff',
    },
    secondary: {
      light: '#ff7961',
      main: '#f44336',
      dark: '#ba000d',
      contrastText: '#000',
    },
  },
});
```

### Playground <meta data-oversett="" data-original-text="Playground">

Чтобы проверить цветовую схему [material.io/design/color](https://m2.material.io/design/color/) с помощью документации MUI, просто выберите цвета с помощью палитры и ползунков ниже. Также вы можете ввести шестнадцатеричные значения в текстовые поля Primary и Secondary.

{{"demo": "ColorTool.js", "hideToolbar": true, "bg": true}}

Вывод, показанный в примере цвета, можно вставить непосредственно в [`createTheme()`](/material-ui/customization/theming/#createtheme-options-args-theme) функцию (для использования с [`ThemeProvider`](/material-ui/customization/theming/#theme-provider)):

```jsx
import { createTheme } from '@mui/material/styles';
import { purple } from '@mui/material/colors';

const theme = createTheme({
  palette: {
    primary: {
      main: purple[500],
    },
    secondary: {
      main: '#f44336',
    },
  },
});
```

Необходимо указать только оттенки `main` (если вы не хотите дополнительно настроить `light`, `dark` или `contrastText`), так как остальные цвета будут рассчитаны по `createTheme()`, как описано в разделе " [Настройка темы](/material-ui/customization/palette/) ".

Если вы используете первичные и/или вторичные оттенки по умолчанию, то при указании объекта color, `createTheme()` будет использовать соответствующие оттенки из цвета материала для основного, светлого и темного.

### Инструменты сообщества <meta data-oversett="" data-original-text="Tools by the community">

-   [mui-theme-creator](https://bareynol.github.io/mui-theme-creator/): Инструмент для разработки и настройки тем для библиотеки компонентов MUI. Включает базовые шаблоны сайтов для демонстрации различных компонентов и их влияния на тему.
-   [Генератор палитры материалов](https://m2.material.io/inline-tools/color/): Генератор палитры материалов может быть использован для создания палитры для любого введенного вами цвета.

## Цветовые палитры Material Design 2014 года <meta data-oversett="" data-original-text="2014 Material Design color palettes">

Эти цветовые палитры, первоначально созданные Material Design в 2014 году, состоят из цветов, гармонично сочетающихся между собой, и могут быть использованы для разработки палитры вашего бренда. Чтобы создать собственные гармоничные палитры, воспользуйтесь инструментом генерации палитр.

### Важные термины <meta data-oversett="" data-original-text="Important Terms">

-   **Палитра**: Палитра - это коллекция цветов, т.е. оттенков и их переливов. MUI предоставляет все цвета из руководства Material Design.[Эта цветовая палитра](#color-palette) была разработана с использованием цветов, которые гармонично сочетаются друг с другом.
-   **Оттенок и тени**: Один цвет в палитре состоит из оттенка, например "красный", и оттенка, например "500". "Красный 50" - самый светлый оттенок красного_(розовый!_), а "красный 900" - самый темный. Кроме того, большинство оттенков сопровождаются "акцентными" оттенками, перед которыми ставится знак `A`.

### Цветовая палитра <meta data-oversett="" data-original-text="Color palette">

Учитывая _HUE_ (красный, розовый и т.д.) и _SHADE_ (500, 600 и т.д.), вы можете импортировать цвет следующим образом:

```jsx
import { red } from '@mui/material/colors';

const color = red[500];
```

{{"demo": "Color.js", "hideToolbar": true, "bg": "inline"}}

### Примеры <meta data-oversett="" data-original-text="Examples">

Например, вы можете сослаться на дополнительные основные и акцентные цвета, "красный 500" и "фиолетовый A200", следующим образом:

```js
import { purple, red } from '@mui/material/colors';

const primary = red[500]; // #f44336
const accent = purple['A200']; // #e040fb
const accent = purple.A200; // #e040fb (alternative method)
```

### Доступность <meta data-oversett="" data-original-text="Accessibility">

[Правило 1.4.3 WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html) рекомендует, чтобы для визуального представления текста и изображений текста коэффициент контрастности составлял не менее 4,5:1. Material UI в настоящее время обеспечивает только коэффициент контрастности 3:1. Если вы хотите соответствовать требованиям WCAG 2.1 AA, вы можете увеличить минимальный коэффициент контрастности, как описано в разделе "[Настройка темы](/material-ui/customization/palette/#accessibility) ".
