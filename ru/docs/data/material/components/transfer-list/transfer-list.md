---
product: material-ui
title: Transfer list React component
components: List, ListItem, Checkbox, Switch
githubLabel: 'component: transfer list'
---

# Список переноса <meta data-oversett="" data-original-text="Transfer List">

<p class="description">Список переноса (или "челнок") позволяет пользователю перемещать один или несколько элементов списка между списками.</p>

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Основной список переноса <meta data-oversett="" data-original-text="Basic transfer list">

Для полноты картины в этом примере есть кнопки "переместить все", но они нужны не для каждого списка переноса.

{{"demo": "TransferList.js", "bg": true}}

## Расширенный список переноса <meta data-oversett="" data-original-text="Enhanced transfer list">

В этом примере кнопки "переместить все" заменены на флажок "выбрать все / не выбрать ни одного", а также добавлен счетчик.

{{"demo": "SelectAllTransferList.js", "bg": true}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

Компонент поставляется с парой ограничений:

-   Он работает только на настольном компьютере. Если у вас ограниченное количество вариантов для выбора, предпочтите компонент [Autocomplete](/material-ui/react-autocomplete/#multiple-values). Если для вас важна поддержка мобильных устройств, обратите внимание на [#27579](https://github.com/mui/material-ui/issues/27579).
-   Не существует высокоуровневых компонентов, экспортируемых из npm. Демонстрации основаны на композиции. Если для вас это важно, обратите внимание на [#27579](https://github.com/mui/material-ui/issues/27579).
