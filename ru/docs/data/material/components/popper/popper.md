---
product: material-ui
title: React Popper component
components: Popper
githubLabel: 'component: Popper'
unstyled: /base/react-popper/
---

# Поппер <meta data-oversett="" data-original-text="Popper">

<p class="description">Поппер можно использовать для отображения некоторого содержимого поверх другого. Это альтернатива react-popper.</p>

Некоторые важные особенности компонента `Popper`:

-   🕷 Popper полагается на стороннюю библиотеку[(Popper.js](https://popper.js.org/)) для идеального позиционирования.
-   💄 Это альтернативный API к react-popper. Он нацелен на простоту.
-   📦 [24.9 kB gzipped](/size-snapshot/).
-   дочерние элементы [`Portal`](/material-ui/react-portal/) в тело документа, чтобы избежать проблем с рендерингом. Вы можете отключить это поведение с помощью `disablePortal`.
-   Прокрутка не блокируется, как в случае с [`Popover`](/material-ui/react-popover/) Размещение всплывающего окна обновляется в соответствии с доступной областью в области просмотра.
-   Щелчок не скрывает компонент `Popper`. Если вам нужно такое поведение, вы можете использовать [`ClickAwayListener`](/material-ui/react-click-away-listener/) - см. пример в [разделе документации по меню](/material-ui/react-menu/#menulist-composition).
-   Объект `anchorEl` передается как объект ссылки для создания нового экземпляра `Popper.js`.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Базовый поппер <meta data-oversett="" data-original-text="Basic popper">

{{"demo": "SimplePopper.js"}}

## Переходы <meta data-oversett="" data-original-text="Transitions">

Состояние открытия/закрытия поппера можно анимировать с помощью дочернего компонента render prop и компонента transition. Этот компонент должен соблюдать следующие условия:

-   Быть прямым дочерним потомком popper.
-   Вызывать `onEnter` callback prop, когда начинается переход enter.
-   `onExited` Эти два обратных вызова позволяют попперу размонтировать дочерний контент, когда он закрыт и полностью перешел.

Popper имеет встроенную поддержку [react-transition-group](https://github.com/reactjs/react-transition-group).

{{"demo": "TransitionsPopper.js"}}

В качестве альтернативы вы можете использовать [react-spring](https://github.com/pmndrs/react-spring).

{{"demo": "SpringPopper.js"}}

## Позиционированный поппер <meta data-oversett="" data-original-text="Positioned popper">

{{"demo": "PositionedPopper.js"}}

## Игровая площадка прокрутки <meta data-oversett="" data-original-text="Scroll playground">

{{"demo": "ScrollPlayground.js", "hideToolbar": true, "bg": true}}

## Виртуальный элемент <meta data-oversett="" data-original-text="Virtual element">

Значением реквизита `anchorEl` может быть ссылка на поддельный элемент DOM. Вам необходимо создать объект, имеющий форму [`VirtualElement`](https://popper.js.org/docs/v2/virtual-elements/).

Выделите часть текста, чтобы увидеть поппер:

{{"demo": "VirtualElementPopper.js"}}

## Взаимодополняющие проекты <meta data-oversett="" data-original-text="Complementary projects">

Для более сложных случаев использования вы можете воспользоваться:

### Помощник PopupState <meta data-oversett="" data-original-text="PopupState helper">

Существует сторонний пакет [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) который в большинстве случаев заботится о состоянии поппера за вас.

{{"demo": "PopperPopupState.js"}}
