---
product: material-ui
title: React Grid component
components: Grid
githubLabel: 'component: Grid'
materialDesign: https://m2.material.io/design/layout/understanding-layout.html
---

# Сетка <meta data-oversett="" data-original-text="Grid">

<p class="description">Сетка отзывчивого макета Material Design адаптируется к размеру и ориентации экрана, обеспечивая согласованность макетов.</p>

[Сетка](https://m2.material.io/design/layout/responsive-layout-grid.html) создает визуальную согласованность между макетами, обеспечивая при этом гибкость в самых разных дизайнах. Отзывчивый пользовательский интерфейс Material Design основан на 12-колоночной сетке.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

:::warning
Компонент `Grid` не следует путать с сеткой данных; он ближе к сетке макетов. Для работы с сеткой данных перейдите к [компоненту `DataGrid`](/x/react-data-grid/) .
:::

## Как это работает <meta data-oversett="" data-original-text="How it works">

Система сетки реализована с помощью компонента `Grid`:

-   Он использует [модуль CSS Flexible Box](https://www.w3.org/TR/css-flexbox-1/) для обеспечения высокой гибкости.
-   Существует два типа макетов: _контейнеры_ и _элементы_.
-   Ширина элементов задается в процентах, поэтому они всегда подвижны и имеют размер относительно родительского элемента.
-   Элементы имеют прокладки для создания расстояния между отдельными элементами.
-   Существует пять точек разрыва сетки: xs, sm, md, lg и xl.
-   Каждой точке разрыва можно присвоить целочисленные значения, указывающие, сколько из 12 доступных столбцов занимает компонент, когда ширина области просмотра удовлетворяет [ограничениям точки разрыва](/material-ui/customization/breakpoints/#default-breakpoints).

Если вы **новичок или не знакомы с flexbox**, рекомендуем вам прочитать это руководство по [flexbox на CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

## Жидкие сетки <meta data-oversett="" data-original-text="Fluid grids">

Жидкие сетки используют колонки, которые масштабируют и изменяют размер содержимого. В макете текучей сетки можно использовать точки останова, чтобы определить, нужно ли кардинально изменить макет.

### Базовая сетка <meta data-oversett="" data-original-text="Basic grid">

Ширина колонок - это целочисленные значения от 1 до 12; они применяются в любой точке останова и указывают, сколько колонок занимает компонент.

Значение, заданное для точки останова, применяется ко всем другим точкам останова, расположенным шире нее (если оно не переопределено, о чем вы можете прочитать далее на этой странице). Например, `xs={12}` позволяет компоненту занимать всю ширину области просмотра, независимо от его размера.

{{"demo": "BasicGrid.js", "bg": true}}

### Сетка с несколькими точками разрыва <meta data-oversett="" data-original-text="Grid with multiple breakpoints">

Компоненты могут иметь несколько значений ширины, что приводит к изменению макета в определенной точке останова. Значения ширины, заданные для больших точек останова, переопределяют значения, заданные для меньших точек останова.

Например, `xs={12} sm={6}` позволяет компоненту занимать половину ширины области просмотра (6 колонок), если ширина области просмотра составляет [600 или более пикселей](/material-ui/customization/breakpoints/#default-breakpoints). Для меньших видовых экранов компонент заполняет все 12 доступных колонок.

{{"demo": "FullWidthGrid.js", "bg": true}}

## Расстановка <meta data-oversett="" data-original-text="Spacing">

Для управления пространством между дочерними элементами используйте реквизит `spacing`. Значение интервала может быть любым положительным числом, включая десятичные дроби и любую строку. Реквизит преобразуется в свойство CSS с помощью реквизита [`theme.spacing()`](/material-ui/customization/spacing/) помощника.

{{"demo": "SpacingGrid.js", "bg": true}}

### Расстояние между строками и столбцами <meta data-oversett="" data-original-text="Row &amp; column spacing">

Реквизиты `rowSpacing` и `columnSpacing` позволяют независимо указывать расстояние между строками и столбцами. Это аналогично свойствам `row-gap` и `column-gap` в [CSS Grid](/system/grid/#row-gap-amp-column-gap).

{{"demo": "RowAndColumnSpacing.js", "bg": true}}

## Отзывчивые значения <meta data-oversett="" data-original-text="Responsive values">

Вы можете менять значение реквизита в зависимости от активной точки останова. Например, мы можем реализовать ["рекомендуемую"](https://m2.material.io/design/layout/responsive-layout-grid.html) отзывчивую сетку макета Material Design.

{{"demo": "ResponsiveGrid.js", "bg": true}}

Отзывчивые значения поддерживаются:

-   `columns`
-   `columnSpacing`
-   `direction`
-   `rowSpacing`
-   `spacing`
-   всеми [другими реквизитами](#system-props) системы.

:::warning
При использовании реквизита responsive `columns` каждый элемент сетки нуждается в соответствующей точке останова. Например, это не работает. Элемент сетки пропускает значение для `md`:

```jsx
<Grid container columns={{ xs: 4, md: 12 }}>
  <Grid item xs={2} />
</Grid>
```
:::

## Интерактивный <meta data-oversett="" data-original-text="Interactive">

Ниже представлен интерактивный демонстрационный пример, позволяющий изучить визуальные результаты различных настроек:

{{"demo": "InteractiveGrid.js", "hideToolbar": true, "bg": true}}

## Авторазметка <meta data-oversett="" data-original-text="Auto-layout">

Авторазметка позволяет _элементам_ равномерно распределить доступное пространство. Это также означает, что вы можете задать ширину одного _элемента_, а остальные автоматически изменят размер вокруг него.

{{"demo": "AutoGrid.js", "bg": true}}

### Содержимое переменной ширины <meta data-oversett="" data-original-text="Variable width content">

Установите один из реквизитов точки останова размера на `"auto"` вместо `true` / a `number`, чтобы изменить размер колонки в зависимости от естественной ширины ее содержимого.

{{"demo": "VariableWidthGrid.js", "bg": true}}

## Сложная сетка <meta data-oversett="" data-original-text="Complex Grid">

Следующая демонстрация не соответствует рекомендациям Material Design, но показывает, как сетка может быть использована для создания сложных макетов.

{{"demo": "ComplexGrid.js", "bg": true}}

## Вложенная сетка <meta data-oversett="" data-original-text="Nested Grid">

Реквизиты `container` и `item` - это два независимых булевых значения; их можно объединить, чтобы позволить компоненту Grid быть одновременно гибким контейнером и дочерним компонентом.

:::info
Гибкий **контейнер** - это поле, создаваемое элементом с вычисленным отображением `flex` или `inline-flex`. Потоковые дочерние элементы гибкого контейнера называются гибкими **элементами** и размещаются с использованием гибкой модели компоновки.
:::

[https://www.w3.org/TR/css-flexbox-1/#box-model](https://www.w3.org/TR/css-flexbox-1/#box-model)

{{"demo": "NestedGrid.js", "bg": true}}

⚠️ Определение явной ширины для элемента Grid, который одновременно является flex-контейнером, flex-элементом и имеет интервал, приводит к неожиданному поведению, избегайте этого:

```jsx
<Grid spacing={1} container item xs={12}>
```

Если вам необходимо сделать это, удалите один из реквизитов.

## Колонки <meta data-oversett="" data-original-text="Columns">

Вы можете изменить количество колонок по умолчанию (12) с помощью реквизита `columns`.

{{"demo": "ColumnsGrid.js", "bg": true}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### Отрицательное поле <meta data-oversett="" data-original-text="Negative margin">

Расстояние между элементами реализовано с отрицательным отступом. Это может привести к неожиданному поведению. Например, чтобы применить цвет фона, необходимо применить `display: flex;` к родителю.

### white-space: nowrap <meta data-oversett="" data-original-text="white-space: nowrap">

Начальным значением для гибких элементов является `min-width: auto`. Это вызывает конфликт позиционирования, когда дочерние элементы используют `white-space: nowrap;`. Вы можете воспроизвести эту проблему с помощью:

```jsx
<Grid item xs>
  <Typography noWrap>
```

Чтобы элемент оставался внутри контейнера, необходимо установить `min-width: 0`. На практике можно установить `zeroMinWidth`:

```jsx
<Grid item xs zeroMinWidth>
  <Typography noWrap>
```

{{"demo": "AutoGridNoWrap.js", "bg": true}}

### direction: column | column-reverse <meta data-oversett="" data-original-text="direction: column | column-reverse">

Реквизиты `xs`, `sm`, `md`, `lg` и `xl` **не поддержи** ваются в контейнерах `direction="column"` и `direction="column-reverse"`.

Они определяют количество сеток, которые компонент будет использовать для данной точки останова. Они предназначены для управления **шириной** при использовании `flex-basis` в контейнерах `row`, но будут влиять на высоту в контейнерах `column`. При использовании эти реквизиты могут оказать нежелательное влияние на высоту элементов `Grid`.

## CSS Grid Layout <meta data-oversett="" data-original-text="CSS Grid Layout">

Компонент `Grid` внутри использует CSS flexbox. Но, как показано ниже, вы можете легко использовать [систему](/system/grid/) и CSS Grid для компоновки ваших страниц.

{{"demo": "CSSGrid.js", "bg": true}}

## Системные реквизиты <meta data-oversett="" data-original-text="System props">

Как компонент CSS, `Grid` поддерживает все свойства. [`system`](/system/properties/) свойства. Вы можете использовать их в качестве реквизитов непосредственно в компоненте. Например, padding:

```jsx
<Grid item p={2}>
```
