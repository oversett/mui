---
product: material-ui
title: Tree view React component
components: TreeView, TreeItem
githubLabel: 'component: tree view'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/treeview/
packageName: '@mui/lab'
---

# Древовидный вид <meta data-oversett="" data-original-text="Tree view">

<p class="description">Виджет древовидного представления представляет иерархический список.</p>

Древовидные представления могут быть использованы для представления навигатора файловой системы, отображающего папки и файлы. Элемент, представляющий папку, может быть развернут, чтобы показать содержимое папки, которое может быть файлами, папками или тем и другим.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовое древовидное представление <meta data-oversett="" data-original-text="Basic tree view">

{{"demo": "FileSystemNavigator.js"}}

## Мультивыбор <meta data-oversett="" data-original-text="Multi-selection">

Древовидные представления также поддерживают мультивыбор.

{{"demo": "MultiSelectTreeView.js"}}

## Управляемое представление дерева <meta data-oversett="" data-original-text="Controlled tree view">

Древовидное представление также предлагает управляемый API.

{{"demo": "ControlledTreeView.js"}}

## Богатый объект <meta data-oversett="" data-original-text="Rich object">

Хотя API компонентов `TreeView`/`TreeItem` обеспечивает максимальную гибкость, для работы с богатыми объектами требуется дополнительный шаг.

Рассмотрим переменную данных со следующей формой, для ее обработки можно использовать рекурсию.

```js
const data = {
  id: 'root',
  name: 'Parent',
  children: [
    {
      id: '1',
      name: 'Child - 1',
    },
    // …
  ],
};
```

{{"demo": "RichObjectTreeView.js", "defaultCodeOpen": false}}

## ContentComponent prop <meta data-oversett="" data-original-text="ContentComponent prop">

Вы можете использовать `ContentComponent` prop и хук `useTreeItem` для дальнейшей настройки поведения TreeItem.

Например, ограничить расширение щелчком по иконке:

{{"demo": "IconExpansionTreeView.js", "defaultCodeOpen": false}}

Или увеличить ширину индикатора состояния:

{{"demo": "BarTreeView.js", "defaultCodeOpen": false}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

### Пользовательские иконки, границы и анимация <meta data-oversett="" data-original-text="Custom icons, border and animation">

{{"demo": "CustomizedTreeView.js"}}

### Клон Gmail <meta data-oversett="" data-original-text="Gmail clone">

{{"demo": "GmailTreeView.js"}}

## Отключенные элементы дерева <meta data-oversett="" data-original-text="Disabled tree items">

{{"demo": "DisabledTreeItems.js"}}

Поведение отключенных элементов дерева зависит от параметра `disabledItemsFocusable`.

Если он равен false:

-   Клавиши со стрелками не будут фокусировать отключенные элементы, а фокусироваться будет следующий элемент без отключения.
-   При вводе первого символа метки отключенного элемента этот элемент не будет фокусироваться.
-   При использовании мыши или клавиатуры отключенные элементы не будут разворачиваться/сворачиваться.
-   При взаимодействии с мышью или клавиатурой отключенные элементы не выбираются.
-   Клавиши Shift + стрелки пропустят отключенные элементы и будет выбран следующий элемент без отключения.
-   Программный фокус не будет фокусировать отключенные элементы.

Если это так:

-   Клавиши со стрелками будут фокусировать отключенные элементы.
-   Ввод первого символа метки отключенного элемента приведет к фокусировке элемента.
-   При взаимодействии с мышью или клавиатурой отключенные элементы не будут разворачиваться/сворачиваться.
-   При взаимодействии с мышью или клавиатурой отключенные элементы не выбираются.
-   Клавиши Shift + стрелки не пропускают отключенные элементы, но отключенный элемент не будет выбран.
-   Программная фокусировка фокусирует отключенные элементы.

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/treeview/)](https://www.w3.org/WAI/ARIA/apg/patterns/treeview/)

Компонент следует авторской практике WAI-ARIA.

Чтобы иметь доступное представление дерева, вы должны использовать `aria-labelledby` или `aria-label` для ссылки или предоставления метки на TreeView, иначе программы чтения с экрана будут объявлять его как "дерево", что затруднит понимание контекста конкретного элемента дерева.
