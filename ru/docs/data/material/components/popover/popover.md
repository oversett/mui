---
product: material-ui
title: React Popover component
components: Grow, Popover
githubLabel: 'component: Popover'
---

# Popover <meta data-oversett="" data-original-text="Popover">

<p class="description">Popover можно использовать для отображения некоторого содержимого поверх другого.</p>

Что нужно знать при использовании компонента `Popover`:

-   Компонент построен поверх [`Modal`](/material-ui/react-modal/) компонента.
-   Прокрутка и отклонение клика блокируются в отличие от [`Popper`](/material-ui/react-popper/) компонента.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Базовый Popover <meta data-oversett="" data-original-text="Basic Popover">

{{"demo": "BasicPopover.js" }}

## Якорная площадка <meta data-oversett="" data-original-text="Anchor playground">

Используйте радиокнопки для настройки позиций `anchorOrigin` и `transformOrigin`. Вы также можете установить `anchorReference` на `anchorPosition` или `anchorEl`. Когда это будет `anchorPosition`, компонент вместо `anchorEl` будет ссылаться на реквизит `anchorPosition`, который вы можете настроить для установки позиции попповера.

{{"demo": "AnchorPlayground.js", "hideToolbar": true}}

## Взаимодействие при наведении курсора мыши <meta data-oversett="" data-original-text="Mouse over interaction">

Эта демонстрация показывает, как использовать компонент `Popover` и событие mouseover для достижения поведения всплывающего окна.

{{"demo": "MouseOverPopover.js"}}

## Дополнительные проекты <meta data-oversett="" data-original-text="Complementary projects">

Для более сложных случаев использования вы можете воспользоваться:

### Помощник PopupState <meta data-oversett="" data-original-text="PopupState helper">

Существует пакет стороннего разработчика [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) который в большинстве случаев заботится о состоянии всплывающего окна.

{{"demo": "PopoverPopupState.js"}}
