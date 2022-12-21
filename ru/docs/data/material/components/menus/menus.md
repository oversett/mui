---
product: material-ui
title: React Menu component
components: Menu, MenuItem, MenuList, ClickAwayListener, Popover, Popper
githubLabel: 'component: menu'
materialDesign: https://m2.material.io/components/menus
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/menubutton/
unstyled: /base/react-menu/
---

# Меню <meta data-oversett="" data-original-text="Menu">

<p class="description">Меню отображает список вариантов выбора на временных поверхностях.</p>

Меню отображает список вариантов выбора на временной поверхности. Оно появляется, когда пользователь взаимодействует с кнопкой или другим элементом управления.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовое меню <meta data-oversett="" data-original-text="Basic menu">

По умолчанию базовое меню открывается над якорным элементом (этот параметр можно [изменить](#menu-positioning) с помощью реквизитов). При приближении к краю экрана основное меню выравнивается по вертикали, чтобы все пункты меню были полностью видны.

Выбор опции должен немедленно зафиксировать опцию и закрыть меню.

**Дискриминация**: В отличие от простых меню, простые диалоги могут представлять дополнительные детали, связанные с опциями, доступными для элемента списка, или предоставлять навигационные или ортогональные действия, связанные с основной задачей. Хотя они могут отображать одно и то же содержимое, простые меню предпочтительнее простых диалогов, поскольку простые меню меньше нарушают текущий контекст пользователя.

{{"demo": "BasicMenu.js"}}

## Меню иконок <meta data-oversett="" data-original-text="Icon menu">

В области просмотра рабочего стола отступы увеличиваются, чтобы дать меню больше места.

{{"demo": "IconMenu.js", "bg": true}}

## Плотное меню <meta data-oversett="" data-original-text="Dense menu">

Для меню с длинным списком и длинным текстом можно использовать реквизит `dense`, чтобы уменьшить размер подкладок и текста.

{{"demo": "DenseMenu.js", "bg": true}}

## Выбранное меню <meta data-oversett="" data-original-text="Selected menu">

Если меню используется для выбора элементов, при открытии простое меню помещает начальный фокус на выбранный элемент меню. Текущий выбранный элемент меню устанавливается с помощью свойства `selected` (из [ListItem](/material-ui/api/list-item/)). Чтобы использовать выбранный элемент меню без изменения начального фокуса, установите для свойства `variant` значение "menu".

{{"demo": "SimpleListMenu.js"}}

## Позиционированное меню <meta data-oversett="" data-original-text="Positioned menu">

Поскольку компонент `Menu` использует компонент `Popover` для своего позиционирования, вы можете использовать те же [реквизиты позиционирования](/material-ui/react-popover/#anchor-playground) для его позиционирования. Например, вы можете отобразить меню поверх якоря:

{{"demo": "PositionedMenu.js"}}

## Композиция MenuList <meta data-oversett="" data-original-text="MenuList composition">

Компонент `Menu` внутренне использует компонент `Popover`. Однако вы можете захотеть использовать другую стратегию позиционирования или не блокировать прокрутку. Для удовлетворения этих потребностей мы предоставляем компонент `MenuList`, который вы можете компоновать, в данном примере с `Popper`.

Основная обязанность компонента `MenuList` - обрабатывать фокус.

{{"demo": "MenuListComposition.js", "bg": true}}

## Меню аккаунта <meta data-oversett="" data-original-text="Account menu">

`Menu` можно смешивать с другими компонентами, такими как `Avatar`.

{{"demo": "AccountMenu.js"}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedMenus.js"}}

Компонент `MenuItem` представляет собой обертку вокруг `ListItem` с некоторыми дополнительными стилями. Вы можете использовать те же возможности композиции списка с компонентом `MenuItem`:

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры настройки MUI Treasury](https://mui-treasury.com/styles/menu/).

## Меню максимальной высоты <meta data-oversett="" data-original-text="Max height menu">

Если высота меню не позволяет отобразить все пункты меню, меню может прокручиваться внутри.

{{"demo": "LongMenu.js"}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

Существует [ошибка flexbox](https://bugs.chromium.org/p/chromium/issues/detail?id=327437), которая не позволяет компоненту `text-overflow: ellipsis` работать в макете flexbox. Вы можете использовать компонент `Typography` вместе с `noWrap`, чтобы обойти эту проблему:

{{"demo": "TypographyMenu.js", "bg": true}}

## Изменить переход <meta data-oversett="" data-original-text="Change transition">

Используйте другой переход.

{{"demo": "FadeMenu.js"}}

## Контекстное меню <meta data-oversett="" data-original-text="Context menu">

Вот пример контекстного меню. (Щелкните правой кнопкой мыши, чтобы открыть).

{{"demo": "ContextMenu.js"}}

## Дополнительные проекты <meta data-oversett="" data-original-text="Complementary projects">

Для более сложных случаев использования вы можете воспользоваться:

### Помощник PopupState <meta data-oversett="" data-original-text="PopupState helper">

Существует пакет стороннего разработчика [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) который в большинстве случаев заботится о состоянии меню за вас.

{{"demo": "MenuPopupState.js"}}
