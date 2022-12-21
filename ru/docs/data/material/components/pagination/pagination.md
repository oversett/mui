---
product: material-ui
title: React Pagination component
components: Pagination, PaginationItem
githubLabel: 'component: pagination'
---

# Pagination <meta data-oversett="" data-original-text="Pagination">

<p class="description">Компонент Pagination позволяет пользователю выбрать определенную страницу из ряда страниц.</p>

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовая пагинация <meta data-oversett="" data-original-text="Basic pagination">

{{"demo": "BasicPagination.js"}}

## Очерченная пагинация <meta data-oversett="" data-original-text="Outlined pagination">

{{"demo": "PaginationOutlined.js"}}

## Закругленная пагинация <meta data-oversett="" data-original-text="Rounded pagination">

{{"demo": "PaginationRounded.js"}}

## Размер пагинации <meta data-oversett="" data-original-text="Pagination size">

{{"demo": "PaginationSize.js"}}

## Кнопки <meta data-oversett="" data-original-text="Buttons">

Вы можете включить кнопки первой и последней страниц или отключить кнопки предыдущей и следующей страниц.

{{"demo": "PaginationButtons.js"}}

## Пользовательские значки <meta data-oversett="" data-original-text="Custom icons">

Можно настроить значки элементов управления.

{{"demo": "CustomIcons.js"}}

## Диапазоны пагинации <meta data-oversett="" data-original-text="Pagination ranges">

Вы можете указать, сколько цифр отображать по обе стороны от текущей страницы с помощью реквизита `siblingRange`, а также рядом с номером начальной и конечной страницы с помощью реквизита `boundaryRange`.

{{"demo": "PaginationRanges.js"}}

## Управляемая пагинация <meta data-oversett="" data-original-text="Controlled pagination">

{{"demo": "PaginationControlled.js"}}

## Интеграция маршрутизатора <meta data-oversett="" data-original-text="Router integration">

{{"demo": "PaginationLink.js"}}

## `usePagination` <meta data-oversett="" data-original-text="usePagination">

Для продвинутых случаев использования кастомизации существует безголовый хук `usePagination()`. Он принимает почти те же опции, что и компонент Pagination, за вычетом всех реквизитов, связанных с рендерингом JSX. Компонент Pagination построен на этом хуке.

```jsx
import usePagination from '@mui/material/usePagination';
```

{{"demo": "UsePagination.js"}}

## Пагинация таблиц <meta data-oversett="" data-original-text="Table pagination">

Компонент `Pagination` был разработан для постраничного отображения списка произвольных элементов, когда бесконечная загрузка не используется. Он предпочтителен в контекстах, где важно SEO, например, в блоге.

Для постраничного отображения большого набора табличных данных следует использовать компонент `TablePagination`.

{{"demo": "TablePagination.js"}}

:::warning
Обратите внимание, что реквизит страницы `Pagination` начинается с 1, чтобы соответствовать требованию включения значения в URL, в то время как реквизит страницы `TablePagination` начинается с 0, чтобы соответствовать требованию нулевых массивов JavaScript, которые возникают при рендеринге большого количества табличных данных.
:::

Вы можете узнать больше об этом примере использования в [разделе](/material-ui/react-table/#custom-pagination-options) документации, посвященном [таблицам](/material-ui/react-table/#custom-pagination-options).

## Доступность <meta data-oversett="" data-original-text="Accessibility">

### ARIA <meta data-oversett="" data-original-text="ARIA">

Корневой узел по умолчанию имеет роль "navigation" и aria-label "pagination navigation". Элементы страницы имеют метку aria, которая определяет назначение элемента ("перейти на первую страницу", "перейти на предыдущую страницу", "перейти на страницу 1" и т.д.). Вы можете переопределить их с помощью параметра `getItemAriaLabel`.

### Клавиатура <meta data-oversett="" data-original-text="Keyboard">

Элементы пагинации располагаются в порядке вкладок, с tabindex "0".
