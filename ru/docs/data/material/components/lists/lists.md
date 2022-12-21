---
product: material-ui
title: React List component
components: Collapse, Divider, List, ListItem, ListItemButton, ListItemAvatar, ListItemIcon, ListItemSecondaryAction, ListItemText, ListSubheader
githubLabel: 'component: list'
materialDesign: https://m2.material.io/components/lists
---

# Списки <meta data-oversett="" data-original-text="Lists">

<p class="description">Списки - это непрерывные вертикальные указатели текста или изображений.</p>

Списки - это непрерывная группа текста или изображений. Они состоят из элементов, содержащих основные и дополнительные действия, которые представлены значками и текстом.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основной список <meta data-oversett="" data-original-text="Basic List">

{{"demo": "BasicList.js", "bg": true}}

Последний элемент предыдущей демонстрации показывает, как можно отобразить ссылку:

```jsx
<ListItemButton component="a" href="#simple-list">
  <ListItemText primary="Spam" />
</ListItemButton>
```

Вы можете найти [демо с React Router в этом разделе](/material-ui/guides/routing/#list) документации.

## Вложенный список <meta data-oversett="" data-original-text="Nested List">

{{"demo": "NestedList.js", "bg": true}}

## Папка-список <meta data-oversett="" data-original-text="Folder List">

{{"demo": "FolderList.js", "bg": true}}

## Интерактивный <meta data-oversett="" data-original-text="Interactive">

Ниже приведена интерактивная демонстрация, позволяющая изучить визуальные результаты различных настроек:

{{"demo": "InteractiveList.js", "bg": true}}

## Selected ListItem <meta data-oversett="" data-original-text="Selected ListItem">

{{"demo": "SelectedListItem.js", "bg": true}}

## Выравнивание элементов списка <meta data-oversett="" data-original-text="Align list items">

При отображении трех и более строк аватар не выравнивается по верху. Вам следует установить параметр `alignItems="flex-start"` для выравнивания аватара по верху, следуя рекомендациям Material Design:

{{"demo": "AlignItemsList.js", "bg": true}}

## Элементы управления списком <meta data-oversett="" data-original-text="List Controls">

### Флажок <meta data-oversett="" data-original-text="Checkbox">

Флажок может быть как основным, так и дополнительным действием.

Флажок - это первичное действие и индикатор состояния элемента списка. Кнопка комментария - это вторичное действие и отдельная цель.

{{"demo": "CheckboxList.js", "bg": true}}

Флажок является вторичным действием для элемента списка и отдельной целью.

{{"demo": "CheckboxListSecondary.js", "bg": true}}

### Переключатель <meta data-oversett="" data-original-text="Switch">

Переключатель является вторичным действием и отдельной целью.

{{"demo": "SwitchListSecondary.js", "bg": true}}

## Липкий подзаголовок <meta data-oversett="" data-original-text="Sticky subheader">

При прокрутке подзаголовки остаются прикрепленными к верхней части экрана, пока их не вытеснит следующий подзаголовок. Эта функция основана на липком позиционировании CSS. (⚠️ нет поддержки IE 11)

{{"demo": "PinnedSubheaderList.js", "bg": true}}

## Вставка элемента списка <meta data-oversett="" data-original-text="Inset List Item">

Реквизит `inset` позволяет элементу списка, не имеющему ведущей иконки или аватара, правильно выравниваться по отношению к элементам, имеющим ведущую иконку или аватар.

{{"demo": "InsetList.js", "bg": true}}

## Список без желоба <meta data-oversett="" data-original-text="Gutterless list">

При отображении списка в компоненте, который определяет свои собственные желоба, `ListItem` желоба могут быть отключены с помощью `disableGutters`.

{{"demo": "GutterlessList.js", "bg": true}}

## Виртуализированный список <meta data-oversett="" data-original-text="Virtualized List">

В следующем примере мы демонстрируем, как использовать [react-window](https://github.com/bvaughn/react-window) с компонентом `List`. Он отображает 200 строк и может легко обрабатывать больше. Виртуализация помогает решить проблемы производительности.

{{"demo": "VirtualizedList.js", "bg": true}}

Использование [react-window](https://github.com/bvaughn/react-window), когда это возможно, приветствуется. Если эта библиотека не подходит для вашего случая использования, вам следует рассмотреть возможность использования [react-virtualized](https://github.com/bvaughn/react-virtualized), а затем альтернативы, например [react-virtuoso](https://github.com/petyosi/react-virtuoso).

## Кастомизация <meta data-oversett="" data-original-text="Customization">

Здесь приведены примеры настройки компонента. Вы можете узнать больше об этом на[странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedList.js"}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/list-item/).
