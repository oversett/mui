---
product: material-ui
title: React Tooltip component
components: Tooltip
githubLabel: 'component: tooltip'
materialDesign: https://m2.material.io/components/tooltips
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/
---

# Всплывающие подсказки <meta data-oversett="" data-original-text="Tooltip">

<p class="description">Всплывающие подсказки отображают информативный текст, когда пользователи наводят курсор, фокусируются на элементе или касаются его.</p>

При активации всплывающие подсказки отображают текстовую метку, идентифицирующую элемент, например, описание его функции.

{{"component": "modules/components/ComponentLinkHeader.js"}}

## Базовая всплывающая подсказка <meta data-oversett="" data-original-text="Basic tooltip">

{{"demo": "BasicTooltip.js"}}

## Расположенные всплывающие подсказки <meta data-oversett="" data-original-text="Positioned tooltips">

На сайте `Tooltip` есть 12 вариантов **размещения**. Они не имеют стрелок направления; вместо этого они полагаются на движение, исходящее от источника, чтобы передать направление.

{{"demo": "PositionedTooltips.js"}}

## Персонализация <meta data-oversett="" data-original-text="Customization">

Ниже приведены примеры настройки компонента. Подробнее об этом вы можете узнать на [странице документации по переопределениям](/material-ui/customization/how-to-customize/).

{{"demo": "CustomizedTooltips.js"}}

## Всплывающие подсказки со стрелками <meta data-oversett="" data-original-text="Arrow tooltips">

Вы можете использовать свойство `arrow`, чтобы придать всплывающей подсказке стрелку, указывающую, к какому элементу она относится.

{{"demo": "ArrowTooltips.js"}}

## Пользовательский дочерний элемент <meta data-oversett="" data-original-text="Custom child element">

Подсказка должна применять слушателей событий DOM к своему дочернему элементу. Если дочерний элемент является пользовательским элементом React, вам нужно убедиться, что он распространяет свои реквизиты на базовый элемент DOM.

```jsx
const MyComponent = React.forwardRef(function MyComponent(props, ref) {
  //  Spread the props to the underlying DOM element.
  return (
    <div {...props} ref={ref}>
      Bin
    </div>
  );
});

// ...

<Tooltip title="Delete">
  <MyComponent />
</Tooltip>;
```

Аналогичную концепцию можно найти в руководстве по [обертыванию компонентов](/material-ui/guides/composition/#wrapping-components).

Если в качестве дочернего элемента используется компонент класса, вам также нужно убедиться, что ссылка на него передается на базовый элемент DOM. (Ссылка на сам компонент класса работать не будет).

```jsx
class MyComponent extends React.Component {
  render() {
    const { innerRef, ...props } = this.props;
    //  Spread the props to the underlying DOM element.
    return (
      <div {...props} ref={innerRef}>
        Bin
      </div>
    );
  }
}

// Wrap MyComponent to forward the ref as expected by Tooltip
const WrappedMyComponent = React.forwardRef(function WrappedMyComponent(props, ref) {
  return <MyComponent {...props} innerRef={ref} />;
});

// ...

<Tooltip title="Delete">
  <WrappedMyComponent />
</Tooltip>;
```

## Триггеры <meta data-oversett="" data-original-text="Triggers">

Вы можете определить типы событий, которые вызывают отображение всплывающей подсказки.

Действие прикосновения требует длительного нажатия, поскольку по умолчанию для параметра `enterTouchDelay` установлено значение `700`мс.

{{"demo": "TriggersTooltips.js"}}

## Управляемые всплывающие подсказки <meta data-oversett="" data-original-text="Controlled tooltips">

Вы можете использовать реквизиты `open`, `onOpen` и `onClose` для управления поведением всплывающей подсказки.

{{"demo": "ControlledTooltips.js"}}

## Переменная ширина <meta data-oversett="" data-original-text="Variable width">

По умолчанию `Tooltip` обертывает длинный текст, чтобы сделать его читабельным.

{{"demo": "VariableWidth.js"}}

## Интерактивные <meta data-oversett="" data-original-text="Interactive">

Всплывающие подсказки по умолчанию интерактивны (чтобы пройти [критерий успеха WCAG 2.1 1.4.13](https://www.w3.org/TR/WCAG21/#content-on-hover-or-focus)). Они не закроются, если пользователь наведет курсор на подсказку до истечения срока действия `leaveDelay`. Вы можете отключить это поведение (тем самым не пройдя критерий успеха, который требуется для достижения уровня AA), передав `disableInteractive`.

{{"demo": "NonInteractiveTooltips.js"}}

## Отключенные элементы <meta data-oversett="" data-original-text="Disabled elements">

По умолчанию отключенные элементы, такие как `<button>`, не вызывают взаимодействия с пользователем, поэтому `Tooltip` не активируется при обычных событиях, таких как наведение курсора. Чтобы разместить элементы с ограниченными возможностями, добавьте простой элемент-обертку, например, `span`.

:::warning
Для работы с Safari вам необходимо, чтобы под оберткой всплывающей подсказки находился хотя бы один блок отображения или гибкий элемент.
:::

{{"demo": "DisabledTooltips.js"}}

:::warning
Если вы не оборачиваете MUI-компонент, который наследуется от `ButtonBase`, например, родной элемент `<button>`, вам также следует добавить CSS-свойство _pointer-events: none;_ к вашему элементу, когда он отключен:
:::

```jsx
<Tooltip title="You don't have permission to do this">
  <span>
    <button disabled={disabled} style={disabled ? { pointerEvents: 'none' } : {}}>
      A disabled button
    </button>
  </span>
</Tooltip>
```

## Переходы <meta data-oversett="" data-original-text="Transitions">

Используйте другой переход.

{{"demo": "TransitionsTooltips.js"}}

## Следовать за курсором <meta data-oversett="" data-original-text="Follow cursor">

Вы можете разрешить всплывающей подсказке следовать за курсором, установив `followCursor={true}`.

{{"demo": "FollowCursorTooltips.js"}}

## Виртуальный элемент <meta data-oversett="" data-original-text="Virtual element">

Если вам необходимо реализовать пользовательское размещение, вы можете использовать `anchorEl` prop: Значение `anchorEl` prop может быть ссылкой на поддельный элемент DOM. Вам необходимо создать объект в форме [`VirtualElement`](https://popper.js.org/docs/v2/virtual-elements/).

{{"demo": "AnchorElTooltips.js"}}

## Показ и скрытие <meta data-oversett="" data-original-text="Showing and hiding">

Обычно всплывающая подсказка отображается сразу же, когда пользователь наводит курсор мыши на элемент, и скрывается, когда пользователь отводит мышь. Задержка показа или скрытия всплывающей подсказки может быть добавлена с помощью реквизитов `enterDelay` и `leaveDelay`, как показано в демонстрации управляемых всплывающих подсказок выше.

На мобильных устройствах всплывающая подсказка отображается, когда пользователь долго нажимает на элемент, и скрывается после задержки в 1500 мс. Вы можете отключить эту функцию с помощью реквизита `disableTouchListener`.

{{"demo": "DelayTooltips.js"}}

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/)](https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/)

По умолчанию всплывающая подсказка только маркирует свой дочерний элемент. Это заметно отличается от `title`, который может либо маркировать **, либо** описывать свой дочерний элемент в зависимости от того, есть ли у него уже метка. Например, в:

```html
<button title="some more information">A button</button>
```

`title` действует как доступное описание. Если вы хотите, чтобы всплывающая подсказка действовала как доступное описание, вы можете передать `describeChild`. Обратите внимание, что вы не должны использовать `describeChild`, если всплывающая подсказка является единственной визуальной меткой. В противном случае у ребенка не будет доступного имени, а всплывающая подсказка нарушит [критерий успеха 2.5.3 в WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html).

{{"demo": "AccessibilityTooltips.js"}}
