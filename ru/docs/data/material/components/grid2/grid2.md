---
product: material-ui
title: React Grid component
githubLabel: 'component: Grid'
materialDesign: https://m2.material.io/design/layout/understanding-layout.html
---

# Сетка версии 2 <meta data-oversett="" data-original-text="Grid version 2">

<p class="description">Сетка отзывчивого макета адаптируется к размеру и ориентации экрана, обеспечивая согласованность макетов.</p>

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

Компонент `Grid` хорошо работает для макета с известным числом колонок. Колонки можно настроить с несколькими точками разрыва, чтобы указать диапазон колонок каждого дочернего элемента.

## Что изменилось <meta data-oversett="" data-original-text="What's changed">

Мы создали компонент `Grid` с нуля, чтобы:

-   Исправить [известные проблемы](https://github.com/mui/material-ui/pull/32746), появившиеся в Material UI v5.
-   Упростить логику работы с переменными CSS, удалив ненужный реквизит `item` и уменьшив специфичность CSS.
-   Ввести правильное исправление для [предотвращения появления полосы прокрутки](#prevent-scrollbar) при переключении между подходами к отрицательным полям.
-   Установить отрицательные поля одинакового размера со всех сторон контейнера сетки по умолчанию.

Поскольку новая реализация считается разрушающим изменением, мы представили ее в качестве `Unstable_Grid2`, чтобы собрать отзывы сообщества, прежде чем сделать ее стабильной в следующем крупном выпуске Material UI.

Мы предлагаем всем попробовать новую версию `Grid`, посетив [руководство по миграции Grid v2](/material-ui/migration/migration-grid-v2/).

:::info
С этого момента импорт называется `Grid` v1 и `Grid` v2:

```js
import Grid from '@mui/material/Grid'; // Grid version 1
import Grid2 from '@mui/material/Unstable_Grid2'; // Grid version 2
```
:::

## Как это работает <meta data-oversett="" data-original-text="How it works">

Система сетки реализована с помощью компонента `Grid`:

-   Он использует [CSS Flexbox](https://www.w3.org/TR/css-flexbox-1/) (а не CSS Grid) для высокой гибкости.
-   Сетка всегда является гибким элементом. Используйте компонент `container`, чтобы добавить гибкий контейнер.
-   Ширина элементов задается в процентах, поэтому они всегда плавные и имеют размер относительно родительского элемента.
-   Существует пять точек разрыва сетки по умолчанию: xs, sm, md, lg и xl. Если вам нужны пользовательские точки разрыва, посмотрите раздел " [Пользовательские точки разрыва сетки](#custom-breakpoints)".
-   Для каждой точки разрыва можно задать целочисленные значения, чтобы указать, сколько из 12 доступных колонок занимает компонент, когда ширина области просмотра удовлетворяет [ограничениям точки разрыва](/material-ui/customization/breakpoints/#default-breakpoints).
-   Для создания промежутков между дочерними компонентами используются отрицательные поля и подкладки, которые ведут себя аналогично [свойству `gap` CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/gap).
-   _Не_ поддерживает разделение строк. Дочерние элементы не могут охватывать несколько рядов. Мы рекомендуем использовать [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout), если вам нужна эта функциональность.
-   Он _не_ размещает дочерние элементы автоматически. Он будет пытаться разместить дочерние элементы по одному, и если места не хватит, остальные дочерние элементы будут начинаться со следующей строки, и так далее. Если вам нужно автоматическое размещение, мы рекомендуем использовать [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Auto-placement_in_CSS_Grid_Layout).

:::warning
Компонент `Grid` - это сетка _макетов_, а не сетка _данных_. Если вам нужна сетка данных, обратите внимание на [компонент MUI X `DataGrid`](/x/react-data-grid/) .
:::

## Жидкие сетки <meta data-oversett="" data-original-text="Fluid grids">

Жидкие сетки используют колонки, которые масштабируют и изменяют размер содержимого. В макете жидкой сетки можно использовать точки останова, чтобы определить, нужно ли кардинально изменить макет.

### Базовая сетка <meta data-oversett="" data-original-text="Basic grid">

Для создания макета сетки необходим контейнер. Используйте реквизит `container` для создания контейнера сетки, который обертывает элементы сетки ( `Grid` всегда является элементом).

Ширина колонок - это целочисленные значения от 1 до 12. Они могут быть применены в любой точке останова, чтобы указать, сколько колонок занимает компонент.

Значение, заданное для точки останова, применяется ко всем другим более широким точкам останова, если оно не переопределено - подробнее см. в разделе " [Множественные точки останова](#multiple-breakpoints) ". Например, компонент с `xs={12}` занимает всю ширину области просмотра независимо от его размера.

{{"demo": "BasicGrid.js", "bg": true}}

### Множественные точки останова <meta data-oversett="" data-original-text="Multiple breakpoints">

Компоненты могут иметь несколько значений ширины, что приводит к изменению макета в определенной точке останова. Значения ширины, заданные для больших точек останова, переопределяют значения, заданные для меньших точек останова.

Например, компонент с `xs={12} sm={6}` занимает всю ширину области просмотра, если область просмотра имеет [ширину менее 600 пикселей](/material-ui/customization/breakpoints/#default-breakpoints). Когда область просмотра увеличивается сверх этого размера, компонент занимает половину общей ширины - шесть колонок, а не 12.

{{"demo": "FullWidthGrid.js", "bg": true}}

## Расстановка <meta data-oversett="" data-original-text="Spacing">

Используйте реквизит `spacing` для управления пространством между дочерними элементами. Значение интервала может быть любым положительным числом (включая десятичные дроби) или строкой. Реквизит преобразуется в свойство CSS с помощью помощника [`theme.spacing()`](/material-ui/customization/spacing/) помощника.

Следующий демонстрационный пример иллюстрирует использование свойства `spacing`:

{{"demo": "SpacingGrid.js", "bg": true, "hideToolbar": true}}

### Расстояние между строками и столбцами <meta data-oversett="" data-original-text="Row and column spacing">

Реквизиты `rowSpacing` и `columnSpacing` позволяют задать расстояние между строками и столбцами независимо друг от друга. Они ведут себя аналогично свойствам `row-gap` и `column-gap` [CSS Grid](/system/grid/#row-gap-amp-column-gap).

{{"demo": "RowAndColumnSpacing.js", "bg": true}}

## Отзывчивые значения <meta data-oversett="" data-original-text="Responsive values">

Вы можете задать значения реквизитов, которые будут меняться при активной точке останова. Например, мы можем реализовать [рекомендуемую](https://m2.material.io/design/layout/responsive-layout-grid.html) Material Design отзывчивую сетку макетов, как показано в следующем примере:

{{"demo": "ResponsiveGrid.js", "bg": true}}

Отзывчивые значения поддерживаются:

-   `columns`
-   `columnSpacing`
-   `direction`
-   `rowSpacing`
-   `spacing`
-   все остальные [реквизиты MUI System](#system-props)

## Авторазметка <meta data-oversett="" data-original-text="Auto-layout">

Функция авторазметки предоставляет равное пространство всем присутствующим элементам. Когда вы задаете ширину одного элемента, остальные автоматически изменяют размер в соответствии с ней.

{{"demo": "AutoGrid.js", "bg": true}}

### Содержимое переменной ширины <meta data-oversett="" data-original-text="Variable width content">

Если значение точки останова задано как `"auto"`, а не `true` или число, то размер колонки автоматически изменяется в соответствии с шириной ее содержимого. Демонстрация ниже показывает, как это работает:

{{"demo": "VariableWidthGrid.js", "bg": true}}

## Вложенная сетка <meta data-oversett="" data-original-text="Nested grid">

Контейнер сетки, который отображается внутри другого контейнера сетки, является вложенной сеткой, которая наследует его [`columns`](#columns) и [`spacing`](#spacing) Он также наследует реквизиты грида верхнего уровня, если получает их.

Посмотрите демонстрацию ниже, чтобы увидеть, как это выглядит:

{{"demo": "NestedGrid.js", "bg": true}}

## Колонки <meta data-oversett="" data-original-text="Columns">

Используйте параметр `columns`, чтобы изменить количество колонок по умолчанию (12) в сетке, как показано ниже:

{{"demo": "ColumnsGrid.js", "bg": true}}

## Смещение <meta data-oversett="" data-original-text="Offset">

Реквизиты смещения (такие как `smOffset`, `mdOffset`) сдвигают элемент в правую часть сетки. Эти реквизиты принимают:

-   числа - например, `mdOffset={2}` сдвигает элемент на два столбца вправо, если размер области просмотра равен или больше точки останова `md`.
-   `"auto"`\-это сдвигает элемент в крайний правый столбец контейнера сетки.

Демонстрация ниже показывает, как использовать реквизит смещения:

{{"demo": "OffsetGrid.js", "bg": true}}

## Пользовательские точки останова <meta data-oversett="" data-original-text="Custom breakpoints">

Если вы зададите в теме пользовательские точки останова, вы можете использовать эти имена в качестве реквизитов элементов сетки в отзывчивых значениях:

```js
import { ThemeProvider, createTheme } from '@mui/material/styles';

function Demo() {
  return (
    <ThemeProvider
      theme={createTheme({
        breakpoints: {
          values: {
            laptop: 1024,
            tablet: 640,
            mobile: 0,
            desktop: 1280,
          },
        },
      })}
    >
      <Grid container spacing={{ mobile: 1, tablet: 2, laptop: 3 }}>
        {Array.from(Array(4)).map((_, index) => (
          <Grid mobile={6} tablet={4} laptop={3} key={index}>
            <div>{index + 1}</div>
          </Grid>
        ))}
      </Grid>
    </ThemeProvider>
  );
}
```

:::info
Пользовательские точки останова влияют на реквизиты размера и смещения:

```diff
- <Grid xs={6} xsOffset={2}>
+ <Grid mobile={6} mobileOffset={2}>
```
:::

### TypeScript <meta data-oversett="" data-original-text="TypeScript">

Вы должны установить модуль augmentation в интерфейсе theme breakpoints. Свойства, установленные на `true`, будут отображаться как `{key}`(size prop) и `{key}Offset`(offset prop).

```ts
declare module '@mui/system' {
  interface BreakpointOverrides {
    // Your custom breakpoints
    laptop: true;
    tablet: true;
    mobile: true;
    desktop: true;
    // Remove default breakpoints
    xs: false;
    sm: false;
    md: false;
    lg: false;
    xl: false;
  }
}
```

## Отключите полосу прокрутки <meta data-oversett="" data-original-text="Disable the scrollbar">

Если вы используете сетку в качестве контейнера в маленьком окне просмотра, вы можете увидеть горизонтальную полосу прокрутки, поскольку отрицательное поле применяется со всех сторон контейнера сетки.

Чтобы отключить эту полосу прокрутки, установите параметр `disableEqualOverflow` в значение `true`. Это уберет отрицательные поля с нижней и правой сторон сетки, чтобы предотвратить переполнение.

Демонстрация ниже показывает, как это работает:

{{"demo": "OverflowGrid.js", "bg": true}}

:::warning
Вам следует избегать добавления границ и фонов в сетку, когда `disableEqualOverflow` имеет значение `true`, поскольку отрицательные поля (применяемые только к верхней и левой сторонам) вызывают визуальное смещение сетки.
:::

## Персонализация <meta data-oversett="" data-original-text="Customization">

### Центрирование элементов <meta data-oversett="" data-original-text="Centered elements">

Чтобы отцентрировать содержимое элемента сетки, укажите `display="flex"` непосредственно на элемент. Затем используйте `justifyContent` и/или `alignItems` для настройки положения содержимого, как показано ниже:

{{"demo": "CenteredElementGrid.js", "bg": true}}

:::warning
Использование реквизита `container` в данной ситуации не подходит, поскольку контейнер сетки предназначен исключительно для обертывания элементов сетки. Он не может обертывать другие элементы.
:::

### Полная граница <meta data-oversett="" data-original-text="Full border">

{{"demo": "FullBorderedGrid.js"}}

### Половина границы <meta data-oversett="" data-original-text="Half border">

{{"demo": "HalfBorderedGrid.js"}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### Направление колонок и реверсирование <meta data-oversett="" data-original-text="Column direction and reversing">

Реквизиты ширина колонки (`xs`, ..., `xl`) и смещение _не_ поддерживаются в контейнерах, использующих `direction="column"` или `direction="column-reverse"`.

Реквизиты size и offset определяют количество колонок, которые компонент будет использовать для данной точки разрыва. Они предназначены для управления шириной с помощью `flex-basis` в контейнерах `row`, но они будут влиять на высоту в контейнерах `column`. При использовании эти реквизиты могут оказать нежелательное влияние на высоту элементов `Grid`.
