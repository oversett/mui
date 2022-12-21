---
product: material-ui
title: React Tabs component
components: Tabs, Tab, TabScrollButton, TabContext, TabList, TabPanel, TabsUnstyled, TabUnstyled, TabPanelUnstyled, TabsListUnstyled
githubLabel: 'component: tabs'
materialDesign: https://m2.material.io/components/tabs
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/tabpanel/
unstyled: /base/react-tabs/
---

# Вкладки <meta data-oversett="" data-original-text="Tabs">

<p class="description">Вкладки облегчают изучение и переключение между различными видами.</p>

Вкладки организуют и позволяют перемещаться между группами контента, которые связаны между собой и находятся на одном уровне иерархии.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Основные вкладки <meta data-oversett="" data-original-text="Basic tabs">

Базовый пример с панелями вкладок.

{{"demo": "BasicTabs.js"}}

## Экспериментальный API <meta data-oversett="" data-original-text="Experimental API">

`@mui/lab` предлагает вспомогательные компоненты, которые вводят реквизиты для реализации доступных вкладок в соответствии с [авторской практикой WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/tabpanel/).

{{"demo": "LabTabs.js"}}

## Обернутые метки <meta data-oversett="" data-original-text="Wrapped labels">

Длинные ярлыки автоматически заворачиваются на вкладках. Если ярлык слишком длинный для вкладки, он будет переполнен, и текст не будет виден.

{{"demo": "TabsWrappedLabel.js"}}

## Цветная вкладка <meta data-oversett="" data-original-text="Colored tab">

{{"demo": "ColorTabs.js"}}

## Отключенная вкладка <meta data-oversett="" data-original-text="Disabled tab">

Вкладку можно отключить, установив параметр `disabled`.

{{"demo": "DisabledTabs.js"}}

## Фиксированные вкладки <meta data-oversett="" data-original-text="Fixed tabs">

Фиксированные вкладки следует использовать при ограниченном количестве вкладок, а также в тех случаях, когда их последовательное размещение способствует развитию мышечной памяти.

### Полная ширина <meta data-oversett="" data-original-text="Full width">

Реквизит `variant="fullWidth"` следует использовать для небольших представлений. В этом демонстрационном примере также используется [react-swipeable-views](https://github.com/oliviertassinari/react-swipeable-views) для анимации перехода вкладок, что позволяет пролистывать вкладки на сенсорных устройствах.

{{"demo": "FullWidthTabs.js", "bg": true}}

### По центру <meta data-oversett="" data-original-text="Centered">

Реквизит `centered` следует использовать для больших представлений.

{{"demo": "CenteredTabs.js", "bg": true}}

## Прокручиваемые вкладки <meta data-oversett="" data-original-text="Scrollable tabs">

### Автоматические кнопки прокрутки <meta data-oversett="" data-original-text="Automatic scroll buttons">

По умолчанию левая и правая кнопки прокрутки автоматически отображаются на настольных компьютерах и скрываются на мобильных. (в зависимости от ширины области просмотра)

{{"demo": "ScrollableTabsButtonAuto.js", "bg": true}}

### Принудительные кнопки прокрутки <meta data-oversett="" data-original-text="Forced scroll buttons">

Левая и правая кнопки прокрутки будут представлены (резервируют место) независимо от ширины области просмотра с помощью `scrollButtons={true}` `allowScrollButtonsMobile` :

{{"demo": "ScrollableTabsButtonForce.js", "bg": true}}

Если вы хотите, чтобы кнопки всегда были видны, настройте их непрозрачность.

```css
.MuiTabs-scrollButtons.Mui-disabled {
  opacity: 0.3;
}
```

{{"demo": "ScrollableTabsButtonVisible.js", "bg": true}}

### Запретить кнопки прокрутки <meta data-oversett="" data-original-text="Prevent scroll buttons">

Левая и правая кнопки прокрутки никогда не будут представлены с помощью `scrollButtons={false}`. Вся прокрутка должна инициироваться через механизмы прокрутки пользовательского агента (например, прокрутка влево/вправо, сдвиг колеса мыши и т.д.).

{{"demo": "ScrollableTabsButtonPrevent.js", "bg": true}}

## Настройка <meta data-oversett="" data-original-text="Customization">

Здесь приведен пример настройки компонента. Вы можете узнать больше об этом на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTabs.js"}}

🎨 Если вы ищете вдохновение, вы можете посмотреть [примеры кастомизации MUI Treasury](https://mui-treasury.com/styles/tabs/).

## Вертикальные вкладки <meta data-oversett="" data-original-text="Vertical tabs">

Чтобы сделать вертикальные вкладки вместо горизонтальных по умолчанию, существует `orientation="vertical"`:

{{"demo": "VerticalTabs.js", "bg": true}}

Обратите внимание, что вы можете восстановить полосу прокрутки с помощью `visibleScrollbar`.

## Вкладки Nav <meta data-oversett="" data-original-text="Nav tabs">

По умолчанию вкладки используют элемент `button`, но вы можете предоставить свой собственный тег или компонент. Вот пример реализации навигации с вкладками:

{{"demo": "NavTabs.js"}}

## Вкладки с иконками <meta data-oversett="" data-original-text="Icon tabs">

Ярлыки вкладок могут быть либо полностью иконками, либо полностью текстом.

{{"demo": "IconTabs.js"}}

{{"demo": "IconLabelTabs.js"}}

## Положение значка <meta data-oversett="" data-original-text="Icon position">

По умолчанию значок располагается на `top` вкладки. Другие поддерживаемые позиции: `start`, `end`, `bottom`.

{{"demo": "IconPositionTabs.js"}}

## Сторонняя библиотека маршрутизации <meta data-oversett="" data-original-text="Third-party routing library">

Одним из частых случаев использования является выполнение навигации только на клиенте, без HTTP-перехода на сервер. Компонент `Tab` предоставляет реквизит `component` для обработки этого случая использования. Здесь представлено [более подробное руководство](/material-ui/guides/routing/#tabs).

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/tabpanel/)](https://www.w3.org/WAI/ARIA/apg/patterns/tabpanel/)

Чтобы предоставить необходимую информацию для вспомогательных технологий, необходимо выполнить следующие действия:

1.  Разметить `Tabs` через `aria-label` или `aria-labelledby`.
2.  `Tab`s должны быть связаны с соответствующим `[role="tabpanel"]` путем установки правильных `id`, `aria-controls` и `aria-labelledby`.

Пример текущей реализации можно найти в демонстрациях на этой странице. Мы также опубликовали [экспериментальный API](#experimental-api) в `@mui/lab`, который не требует дополнительной работы.

### Клавиатурная навигация <meta data-oversett="" data-original-text="Keyboard navigation">

Компоненты реализуют навигацию по клавиатуре, используя поведение "ручной активации". Если вы хотите переключиться на поведение "выбор автоматически следует за фокусом", вы должны передать `selectionFollowsFocus` компоненту `Tabs`. Практика разработки WAI-ARIA содержит подробное руководство о [том, как решить, когда выбор должен автоматически следовать за фокусом](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/#x6-4-deciding-when-to-make-selection-automatically-follow-focus).

#### Демонстрация <meta data-oversett="" data-original-text="Demo">

Следующие две демонстрации отличаются только поведением клавиатурной навигации. Сфокусируйтесь на вкладке и перемещайтесь с помощью клавиш со стрелками, чтобы заметить разницу, например, <kbd class="key">Arrow Left</kbd>.

```jsx
/* Tabs where selection follows focus */
<Tabs selectionFollowsFocus />
```

{{"demo": "AccessibleTabs1.js", "defaultCodeOpen": false}}

```jsx
/* Tabs where each tab needs to be selected manually */
<Tabs />
```

{{"demo": "AccessibleTabs2.js", "defaultCodeOpen": false}}
