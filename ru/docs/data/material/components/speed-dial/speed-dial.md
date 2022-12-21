---
product: material-ui
title: React Speed Dial component
components: SpeedDial, SpeedDialAction, SpeedDialIcon
githubLabel: 'component: speed dial'
materialDesign: https://m2.material.io/components/buttons-floating-action-button#types-of-transitions
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/menubutton/
---

# Быстрый набор <meta data-oversett="" data-original-text="Speed Dial">

<p class="description">При нажатии плавающая кнопка действия может отображать от трех до шести связанных действий в виде быстрого набора.</p>

Если требуется более шести действий, для их отображения следует использовать что-то другое, а не FAB.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основной быстрый набор <meta data-oversett="" data-original-text="Basic speed dial">

Плавающая кнопка действия может отображать связанные действия.

{{"demo": "BasicSpeedDial.js"}}

## Игровая площадка <meta data-oversett="" data-original-text="Playground">

{{"demo": "PlaygroundSpeedDial.js"}}

## Управляемый быстрый набор <meta data-oversett="" data-original-text="Controlled speed dial">

Открытым состоянием компонента можно управлять с помощью реквизитов `open`/`onOpen`/`onClose`.

{{"demo": "ControlledOpenSpeedDial.js"}}

## Пользовательский значок закрытия <meta data-oversett="" data-original-text="Custom close icon">

Вы можете предоставить альтернативную иконку для закрытого и открытого состояния, используя реквизиты `icon` и `openIcon` компонента `SpeedDialIcon`.

{{"demo": "OpenIconSpeedDial.js"}}

## Постоянные всплывающие подсказки действий <meta data-oversett="" data-original-text="Persistent action tooltips">

Подсказки SpeedDialActions могут отображаться постоянно, чтобы пользователям не приходилось долго нажимать, чтобы увидеть подсказку на сенсорных устройствах.

Здесь эта функция включена для всех устройств в демонстрационных целях, но в производстве можно использовать логику `isTouch` для условной установки этого параметра.

{{"demo": "SpeedDialTooltipOpen.js"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

### ARIA <meta data-oversett="" data-original-text="ARIA">

#### Требуемый <meta data-oversett="" data-original-text="Required">

-   Вы должны предоставить `ariaLabel` для компонента быстрого набора.
-   Вы должны предоставить `tooltipTitle` для каждого действия быстрого набора.

#### Предоставляется <meta data-oversett="" data-original-text="Provided">

-   Fab имеет атрибуты `aria-haspopup`, `aria-expanded` и `aria-controls`.
-   Контейнер действий быстрого набора имеет `role="menu"` и `aria-orientation`, установленные в соответствии с направлением.
-   Действия быстрого набора имеют `role="menuitem"`, и атрибут `aria-describedby`, который ссылается на связанную подсказку.

### Клавиатура <meta data-oversett="" data-original-text="Keyboard">

-   Клавиатура быстрого набора открывается при фокусе.
-   Клавиши пробел и Enter вызывают выбранное действие быстрого набора и переключают состояние открытия быстрого набора.
-   Клавиши управления курсором перемещают фокус к следующему или предыдущему действию быстрого набора. (Обратите внимание, что изначально для открытия быстрого набора можно использовать любое направление курсора. Это обеспечивает ожидаемое поведение в зависимости от фактической или воспринимаемой ориентации быстрого набора, например, для пользователя программы чтения с экрана, который воспринимает быстрый набор как выпадающее меню).
-   Клавиша Escape закрывает быстрый набор и, если действие быстрого набора было сфокусировано, возвращает фокус на Fab.
