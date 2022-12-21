---
product: material-ui
title: React Table component
components: Table, TableBody, TableCell, TableContainer, TableFooter, TableHead, TablePagination, TableRow, TableSortLabel
githubLabel: 'component: table'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/table/
materialDesign: https://m2.material.io/components/data-tables
---

# Таблица <meta data-oversett="" data-original-text="Table">

<p class="description">В таблицах отображаются наборы данных. Они могут быть полностью настроены.</p>

Таблицы отображают информацию в виде, удобном для сканирования, чтобы пользователи могли искать закономерности и выводы. Они могут быть встроены в основной контент, например, в карточки. Они могут включать в себя:

-   соответствующую визуализацию
-   Навигация
-   Инструменты для запросов и манипулирования данными

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовая таблица <meta data-oversett="" data-original-text="Basic table">

Простой пример без излишеств.

{{"demo": "BasicTable.js", "bg": true}}

## Таблица данных <meta data-oversett="" data-original-text="Data table">

Компонент `Table` имеет тесное сопоставление с родными элементами `<table>`. Это ограничение делает создание богатых таблиц данных сложной задачей.

[Компонент`DataGrid`](/x/react-data-grid/) предназначен для использования в случаях, ориентированных на работу с большими объемами табличных данных. Хотя он имеет более жесткую структуру, взамен вы получаете более мощные возможности.

{{"demo": "DataTable.js", "bg": "inline"}}

## Плотная таблица <meta data-oversett="" data-original-text="Dense table">

Простой пример плотной таблицы без излишеств.

{{"demo": "DenseTable.js", "bg": true}}

## Сортировка и выбор <meta data-oversett="" data-original-text="Sorting &amp; selecting">

Этот пример демонстрирует использование `Checkbox` и кликабельных строк для выбора с помощью пользовательского `Toolbar`. В нем используется компонент `TableSortLabel` для стилизации заголовков столбцов.

Таблица имеет фиксированную ширину, чтобы продемонстрировать горизонтальную прокрутку. Чтобы предотвратить прокрутку элементов управления пагинацией, компонент TablePagination используется вне таблицы. (В [примере 'Custom Table Pagination Action'](#custom-pagination-actions) ниже показана пагинация в нижнем колонтитуле таблицы).

{{"demo": "EnhancedTable.js", "bg": true}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTables.js", "bg": true}}

### Пользовательские параметры пагинации <meta data-oversett="" data-original-text="Custom pagination options">

Можно настроить параметры, отображаемые в селекте "Rows per page", используя реквизит `rowsPerPageOptions`. Вы должны предоставить либо массив из:

-   **чисел**, каждое число будет использоваться для метки и значения опции.
    
    ```jsx
    <TablePagination rowsPerPageOptions={[10, 50]} />
    ```
    
-   **объектов**, ключи `value` и `label` будут использоваться соответственно для значения и метки опции (полезно для языковых строк, таких как 'All').
    
    ```jsx
    <TablePagination rowsPerPageOptions={[10, 50, { value: -1, label: 'All' }]} />
    ```
    

### Пользовательские действия пагинации <meta data-oversett="" data-original-text="Custom pagination actions">

Реквизит `ActionsComponent` компонента `TablePagination` позволяет реализовать пользовательские действия.

{{"demo": "CustomPaginationActionsTable.js", "bg": true}}

## Липкий заголовок <meta data-oversett="" data-original-text="Sticky header">

Вот пример таблицы с прокручиваемыми строками и фиксированными заголовками столбцов. В нем используется свойство `stickyHeader`. (⚠️ нет поддержки IE 11)

{{"demo": "StickyHeadTable.js", "bg": true}}

## Группировка столбцов <meta data-oversett="" data-original-text="Column grouping">

Вы можете группировать заголовки столбцов, отображая несколько строк таблицы внутри заголовка таблицы:

```jsx
<TableHead>
  <TableRow />
  <TableRow />
</TableHead>
```

{{"demo": "ColumnGroupingTable.js", "bg": true}}

## Складная таблица <meta data-oversett="" data-original-text="Collapsible table">

Пример таблицы с расширяемыми строками, раскрывающими дополнительную информацию. В ней используется компонент [`Collapse`](/material-ui/api/collapse/) компонент.

{{"demo": "CollapsibleTable.js", "bg": true}}

## Растягивающаяся таблица <meta data-oversett="" data-original-text="Spanning table">

Простой пример с разделяющимися строками и столбцами.

{{"demo": "SpanningTable.js", "bg": true}}

## Виртуализированная таблица <meta data-oversett="" data-original-text="Virtualized table">

В следующем примере мы демонстрируем, как использовать [react-virtualized](https://github.com/bvaughn/react-virtualized) с компонентом `Table`. Он отображает 200 строк и может легко обрабатывать больше. Виртуализация помогает решить проблемы производительности.

{{"demo": "ReactVirtualizedTable.js", "bg": true}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(Учебник WAI: [https://www.w3.org/WAI/tutorials/tables/)](https://www.w3.org/WAI/tutorials/tables/)

### Надпись <meta data-oversett="" data-original-text="Caption">

Надпись функционирует как заголовок для таблицы. Большинство программ чтения с экрана объявляют содержание подписей. Подписи помогают пользователям найти таблицу, понять, о чем она, и решить, хотят ли они ее читать.

{{"demo": "AcccessibleTable.js", "bg": true}}

## Нестилизованный <meta data-oversett="" data-original-text="Unstyled">

Если вы хотите использовать нестилизованную таблицу, вы можете использовать примитивные элементы HTML и расширить таблицу с помощью компонента TablePaginationUnstyled. Смотрите демонстрационные примеры в [документации по нестилизованной пагинации таблиц](/base/react-table-pagination/)
