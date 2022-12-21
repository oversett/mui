---
product: material-ui
title: React Icon Component
components: Icon, SvgIcon
githubLabel: 'components: SvgIcon'
materialDesign: https://m2.material.io/design/iconography/system-icons.html
---

# Иконки <meta data-oversett="" data-original-text="Icons">

<p class="description">Указания и рекомендации по использованию иконок в MUI.</p>

MUI обеспечивает поддержку иконок тремя способами:

1.  Стандартизированные [иконки материалов](#material-svg-icons), экспортируемые как компоненты React (SVG-иконки).
2.  С помощью компонента [SvgIcon](#svgicon), React-обертки для пользовательских SVG-иконок.
3.  С помощью компонента [Icon](#icon-font-icons), React-обертки для пользовательских иконок шрифтов.

## Материальные SVG-иконки <meta data-oversett="" data-original-text="Material SVG icons">

Google создал более 2 100 официальных иконок Material, каждая в пяти различных "темах" (см. ниже). Для каждой SVG-иконки мы экспортируем соответствующий React-компонент из пакета `@mui/icons-material`. Вы можете [найти полный список этих иконок](/material-ui/material-icons/).

### Установка <meta data-oversett="" data-original-text="Installation">

Чтобы установить и сохранить в пакете `package.json` зависимости, выполните приведенную ниже команду с помощью **npm**:

```sh
npm install @mui/icons-material
```

или **yarn**:

```sh
yarn add @mui/icons-material
```

Эти компоненты используют компонент MUI `SvgIcon` для рендеринга SVG-пути для каждой иконки, и поэтому имеют зависимость от `@mui/material`.

Если вы еще не используете Material UI в своем проекте, вы можете добавить его, следуя [руководству по установке](/material-ui/getting-started/installation/).

### Использование <meta data-oversett="" data-original-text="Usage">

Импортируйте иконки, используя один из этих двух вариантов:

-   Вариант 1:
    
    ```jsx
    import AccessAlarmIcon from '@mui/icons-material/AccessAlarm';
    import ThreeDRotation from '@mui/icons-material/ThreeDRotation';
    ```
    
-   Вариант 2:
    
    ```jsx
    import { AccessAlarm, ThreeDRotation } from '@mui/icons-material';
    ```
    

Наиболее безопасным для размера пакета является вариант 1, но некоторые разработчики предпочитают вариант 2. Убедитесь, что вы следуете [руководству по минимизации размера пакета](/material-ui/guides/minimizing-bundle-size/#option-two-use-a-babel-plugin) перед использованием второго подхода.

Каждый значок материала также имеет "тему": Заполненная (по умолчанию), Очерченная, Закругленная, Двухцветная и Резкая. Чтобы импортировать компонент значка с темой, отличной от темы по умолчанию, добавьте название темы к имени значка. Например, `@mui/icons-material/Delete` icon with:

-   Заполненная тема (по умолчанию) экспортируется как `@mui/icons-material/Delete`,
-   Очерченная тема экспортируется как `@mui/icons-material/DeleteOutlined`,
-   Закругленная тема экспортируется как `@mui/icons-material/DeleteRounded`,
-   Двухцветная тема экспортируется как `@mui/icons-material/DeleteTwoTone`,
-   Тема Sharp экспортируется как `@mui/icons-material/DeleteSharp`.

:::warning
В руководстве по Material Design иконки именуются "snake\_case" (например, `delete_forever`, `add_a_photo`), в то время как `@mui/icons-material` экспортирует соответствующие иконки, используя именование "PascalCase" (например, `DeleteForever`, `AddAPhoto`). Есть три исключения из этого правила именования: `3d_rotation` экспортируется как `ThreeDRotation`, `4k` экспортируется как `FourK`, а `360` экспортируется как `ThreeSixty`.
:::

{{"demo": "SvgMaterialIcons.js"}}

### Тестирование <meta data-oversett="" data-original-text="Testing">

Для целей тестирования каждая иконка, экспортируемая из `@mui/icons-material`, имеет атрибут `data-testid` с именем иконки. Например:

```jsx
import DeleteIcon from '@mui/icons-material/Delete';
```

имеет следующий атрибут после установки:

```html
<svg data-testid="DeleteIcon"></svg>
```

## SvgIcon . <meta data-oversett="" data-original-text="SvgIcon">

Если вам нужна пользовательская SVG иконка (недоступная в [Material Icons](/material-ui/material-icons/)), вы можете использовать обертку `SvgIcon`. Этот компонент расширяет родной элемент `<svg>`:

-   Он поставляется со встроенной доступностью.
-   SVG-элементы должны быть масштабированы для области просмотра 24x24px, чтобы полученную иконку можно было использовать как есть или включить в качестве дочерней для других компонентов MUI, использующих иконки. Это можно настроить с помощью атрибута `viewBox`. Чтобы унаследовать значение `viewBox` от исходного изображения, можно использовать реквизит `inheritViewBox`.
-   По умолчанию компонент наследует текущий цвет. По желанию можно применить один из цветов темы с помощью реквизита `color`.

```jsx
function HomeIcon(props) {
  return (
    <SvgIcon {...props}>
      <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z" />
    </SvgIcon>
  );
}
```

### Цвет <meta data-oversett="" data-original-text="Color">

{{"demo": "SvgIconsColor.js"}}

### Размер <meta data-oversett="" data-original-text="Size">

{{"demo": "SvgIconsSize.js"}}

### Свойство компонента <meta data-oversett="" data-original-text="Component prop">

Вы можете использовать обертку `SvgIcon`, даже если ваши иконки сохранены в формате `.svg`.[svgr](https://github.com/gregberge/svgr) имеет загрузчики для импорта SVG файлов и использования их в качестве компонентов React. Например, с помощью webpack:

```jsx
// webpack.config.js
{
  test: /\.svg$/,
  use: ['@svgr/webpack'],
}

// ---
import StarIcon from './star.svg';

<SvgIcon component={StarIcon} inheritViewBox />
```

Также можно использовать его с "url-loader" или "file-loader". Именно такой подход используется в Create React App.

```jsx
// webpack.config.js
{
  test: /\.svg$/,
  use: ['@svgr/webpack', 'url-loader'],
}

// ---
import { ReactComponent as StarIcon } from './star.svg';

<SvgIcon component={StarIcon} inheritViewBox />
```

### createSvgIcon <meta data-oversett="" data-original-text="createSvgIcon">

Компонент `createSvgIcon` используется для создания [материальных иконок](#material-icons). Его можно использовать для обертывания SVG-пути компонентом SvgIcon.

```jsx
const HomeIcon = createSvgIcon(
  <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z" />,
  'Home',
);
```

{{"demo": "CreateSvgIcon.js"}}

### Font Awesome <meta data-oversett="" data-original-text="Font Awesome">

Если вы обнаружили, что при использовании FontAwesomeIcon из `@fortawesome/react-fontawesome` возникают проблемы с версткой, вы можете попробовать передать данные Font Awesome SVG непосредственно в SvgIcon.

Ниже приведено сравнение компонента `FontAwesomeIcon` и обернутого компонента `SvgIcon`.

{{"demo": "FontAwesomeSvgIconDemo.js"}}

Реквизит FontAwesomeIcon из `fullWidth` также может быть использован для приблизительного определения правильных размеров, но он не идеален.

### Другие библиотеки <meta data-oversett="" data-original-text="Other Libraries">

#### MDI <meta data-oversett="" data-original-text="MDI">

[materialdesignicons.com](https://materialdesignicons.com/) предоставляет более 2 000 иконок. Для получения нужной иконки скопируйте SVG `path`, который они предоставляют, и используйте его в качестве дочернего компонента `SvgIcon` или с `createSvgIcon()`.

Примечание: [mdi-material-ui](https://github.com/TeamWertarbyte/mdi-material-ui) уже обернул каждую из этих SVG-иконок компонентом `SvgIcon`, так что вам не придется делать это самостоятельно.

## Иконка (иконки шрифтов) <meta data-oversett="" data-original-text="Icon (Font icons)">

Компонент `Icon` отобразит иконку из любого шрифта, поддерживающего лигатуры. В качестве предварительного условия вы должны включить в свой проект такой шрифт, как[Material Icons](https://google.github.io/material-design-icons/#icon-font-for-the-web). Чтобы использовать иконку, просто оберните имя иконки (лигатуру шрифта), например, компонентом `Icon`:

```jsx
import Icon from '@mui/material/Icon';

<Icon>star</Icon>;
```

По умолчанию иконка наследует текущий цвет текста. По желанию вы можете задать цвет иконки, используя одно из свойств цвета темы: `primary`, `secondary`, `action`, `error` И `disabled`.

### Значки из шрифтового материала <meta data-oversett="" data-original-text="Font Material Icons">

`Icon` по умолчанию установит правильное имя базового класса для шрифта Material Icons (заполненный вариант). Все, что вам нужно сделать, это загрузить шрифт, например, через Google Web Fonts:

```html
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/icon?family=Material+Icons"
/>
```

{{"demo": "Icons.js"}}

### Пользовательский шрифт <meta data-oversett="" data-original-text="Custom font">

Для других шрифтов можно настроить имя базового класса с помощью реквизита `baseClassName`. Например, в Material Design можно отображать двухцветные значки:

```jsx
import Icon from '@mui/material/Icon';

<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css?family=Material+Icons+Two+Tone"
  // Import the two tones MD variant                           ^^^^^^^^
/>;
```

{{"demo": "TwoToneIcons.js"}}

#### Глобальное имя базового класса <meta data-oversett="" data-original-text="Global base class name">

Изменение реквизита `baseClassName` для каждого использования компонента повторяется. Вы можете изменить реквизит по умолчанию глобально с помощью темы.

```js
const theme = createTheme({
  components: {
    MuiIcon: {
      defaultProps: {
        // Replace the `material-icons` default value.
        baseClassName: 'material-icons-two-tone',
      },
    },
  },
});
```

Затем вы можете использовать двухцветный шрифт напрямую:

```jsx
<Icon>add_circle</Icon>
```

### Font Awesome <meta data-oversett="" data-original-text="Font Awesome">

[Font Awesome](https://fontawesome.com/icons) можно использовать с компонентом `Icon` следующим образом:

{{"demo": "FontAwesomeIcon.js"}}

Обратите внимание, что иконки Font Awesome были разработаны не так, как иконки Material Icons (сравните две предыдущие демонстрации). Иконки fa обрезаны, чтобы использовать все доступное пространство. Вы можете настроить это с помощью глобального переопределения:

```js
const theme = createTheme({
  components: {
    MuiIcon: {
      styleOverrides: {
        root: {
          // Match 24px = 3 * 2 + 1.125 * 16
          boxSizing: 'content-box',
          padding: 3,
          fontSize: '1.125rem',
        },
      },
    },
  },
});
```

{{"demo": "FontAwesomeIconSize.js"}}

## Font vs SVG. Какой подход использовать? <meta data-oversett="" data-original-text="Font vs SVG. Which approach to use?">

Оба подхода работают хорошо, однако есть некоторые тонкие различия, особенно в плане производительности и качества рендеринга. При любой возможности SVG предпочтительнее, так как он позволяет разделить код, поддерживает больше иконок и рендерится быстрее и лучше.

Для получения более подробной информации посмотрите, [почему GitHub перешел от шрифтовых иконок к SVG-иконкам](https://github.blog/2016-02-22-delivering-octicons-with-svg/).

## Доступность <meta data-oversett="" data-original-text="Accessibility">

Иконки могут передавать различную значимую информацию, поэтому важно обеспечить их доступность там, где это необходимо. Есть два варианта использования, которые вы захотите рассмотреть:

-   **Декоративные иконки**, которые используются только для визуального или брендингового усиления. Если их убрать со страницы, пользователи все равно поймут и смогут пользоваться вашей страницей.
-   **Семантические иконки** - это те, которые используются для передачи смысла, а не просто для украшения. К ним относятся иконки без текста, которые используются в качестве интерактивных элементов управления - кнопок, элементов формы, переключателей и т.д.

### Декоративные значки <meta data-oversett="" data-original-text="Decorative icons">

Если ваши иконки чисто декоративные, то вы уже закончили! Атрибут `aria-hidden=true` добавляется для того, чтобы ваши иконки были правильно доступны (невидимы).

### Семантические иконки <meta data-oversett="" data-original-text="Semantic icons">

#### Семантические SVG иконки <meta data-oversett="" data-original-text="Semantic SVG icons">

Вы должны включить реквизит `titleAccess` со значимым значением. Атрибут `role="img"` и элемент `<title>` добавляются для того, чтобы ваши иконки были правильно доступны.

В случае фокусируемых интерактивных элементов, например, при использовании с кнопкой иконки, вы можете использовать свойство `aria-label`:

```jsx
import IconButton from '@mui/material/IconButton';
import SvgIcon from '@mui/material/SvgIcon';

// ...

<IconButton aria-label="delete">
  <SvgIcon>
    <path d="M20 12l-1.41-1.41L13 16.17V4h-2v12.17l-5.58-5.59L4 12l8 8 8-8z" />
  </SvgIcon>
</IconButton>;
```

#### Семантические значки шрифта <meta data-oversett="" data-original-text="Semantic font icons">

Вам необходимо предоставить текстовую альтернативу, видимую только для вспомогательных технологий.

```jsx
import Box from '@mui/material/Box';
import Icon from '@mui/material/Icon';
import { visuallyHidden } from '@mui/utils';

// ...

<Icon>add_circle</Icon>
<Box component="span" sx={visuallyHidden}>Create a user</Box>
```

#### Ссылка <meta data-oversett="" data-original-text="Reference">

-   [https://www.tpgi.com/using-aria-enhance-svg-accessibility/](https://www.tpgi.com/using-aria-enhance-svg-accessibility/)
