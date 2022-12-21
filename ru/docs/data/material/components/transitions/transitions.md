---
product: material-ui
title: React Transition component
components: Collapse, Fade, Grow, Slide, Zoom
githubLabel: 'component: transitions'
---

# Переходы <meta data-oversett="" data-original-text="Transitions">

<p class="description">Переходы помогают сделать пользовательский интерфейс выразительным и простым в использовании.</p>

MUI предоставляет переходы, которые можно использовать для придания базовой [динамики](https://m2.material.io/design/motion/) вашим приложениям.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Свернуть <meta data-oversett="" data-original-text="Collapse">

Разворачивается от начального края дочернего элемента. Используйте реквизит `orientation`, если вам нужно горизонтальное сворачивание. Реквизит `collapsedSize` можно использовать для установки минимальной ширины/высоты, когда он не развернут.

{{"demo": "SimpleCollapse.js", "bg": true}}

## Затухание <meta data-oversett="" data-original-text="Fade">

Переход от прозрачного к непрозрачному.

{{"demo": "SimpleFade.js", "bg": true}}

## Grow <meta data-oversett="" data-original-text="Grow">

Расширяется наружу от центра дочернего элемента, одновременно переходя от прозрачного к непрозрачному.

Второй пример демонстрирует, как изменить `transform-origin`, и условно применяет реквизит `timeout` для изменения скорости входа.

{{"demo": "SimpleGrow.js", "bg": true}}

## Слайд <meta data-oversett="" data-original-text="Slide">

Сдвиг от края экрана. Реквизит `direction` управляет тем, от какого края экрана начинается переход.

Реквизит `mountOnEnter` компонента Transition предотвращает установку дочернего компонента, пока `in` не станет `true`. Это предотвращает прокрутку относительно расположенного компонента из его внеэкранной позиции. Аналогично, реквизит `unmountOnExit` удаляет компонент из DOM после перехода за пределы экрана.

{{"demo": "SimpleSlide.js", "bg": true}}

### Сдвиг относительно контейнера <meta data-oversett="" data-original-text="Slide relative to a container">

Компонент Slide также принимает `container` prop, который является ссылкой на узел DOM. Если этот prop установлен, компонент Slide будет скользить от края этого узла DOM.

{{"demo": "SlideFromContainer.js"}}

## Zoom <meta data-oversett="" data-original-text="Zoom">

Развернуть наружу от центра дочернего элемента.

Этот пример также демонстрирует, как отсрочить переход enter.

{{"demo": "SimpleZoom.js", "bg": true}}

## Требование к дочернему элементу <meta data-oversett="" data-original-text="Child requirement">

-   **Переслать стиль**: Для лучшей поддержки серверного рендеринга MUI предоставляет дочерним элементам некоторых компонентов перехода (Fade, Grow, Zoom, Slide) реквизит `style`. Чтобы анимация работала, как ожидается, реквизит `style` должен быть применен к DOM.
-   **Переслать ссылку**: компоненты перехода требуют, чтобы первый дочерний элемент пересылал свою ссылку на узел DOM. Для получения более подробной информации о реферере ознакомьтесь с разделом [Осторожно с реферерами](/material-ui/guides/composition/#caveat-with-refs).
-   **Один элемент**: Компоненты перехода требуют только один дочерний элемент (`React.Fragment` не допускается).

```jsx
// The `props` object contains a `style` prop.
// You need to provide it to the `div` element as shown here.
const MyComponent = React.forwardRef((props, ref) {
  return (
    <div ref={ref} {...props}>
      Fade
    </div>
  );
})

export default Main() {
  return (
    <Fade>
      {/* MyComponent must be the only child */}
      <MyComponent />
    </Fade>
  );
}
```

## TransitionGroup <meta data-oversett="" data-original-text="TransitionGroup">

Чтобы анимировать компонент, когда он монтируется или размонтируется, вы можете использовать функцию [`TransitionGroup`](http://reactcommunity.org/react-transition-group/transition-group/) компонент из _react-transition-group_. Когда компоненты добавляются или удаляются, `in` prop переключается автоматически `TransitionGroup`.

{{"demo": "TransitionGroupExample.js"}}

## Свойство TransitionComponent <meta data-oversett="" data-original-text="TransitionComponent prop">

Некоторые компоненты MUI используют эти переходы внутри. Они принимают реквизит `TransitionComponent` для настройки перехода по умолчанию. Вы можете использовать любой из вышеперечисленных компонентов или свой собственный. Он должен удовлетворять следующим условиям:

-   Принимает реквизит `in`. Это соответствует состоянию открытия/закрытия.
-   Вызывать реквизит обратного вызова `onEnter`, когда начинается переход enter.
-   Вызов реквизита обратного вызова `onExited` при завершении перехода exit. Эти два обратных вызова позволяют размонтировать дочерние элементы, когда они находятся в закрытом состоянии и полностью перешли.

Для получения дополнительной информации о создании пользовательского перехода посетите [документацию](http://reactcommunity.org/react-transition-group/transition/) _react-transition-group_ [`Transition`](http://reactcommunity.org/react-transition-group/transition/) . Вы также можете посетить специальные разделы некоторых компонентов:

-   [Модальный](/material-ui/react-modal/#transitions)
-   [Диалог](/material-ui/react-dialog/#transitions)
-   [Popper](/material-ui/react-popper/#transitions)
-   [Snackbar](/material-ui/react-snackbar/#transitions)
-   [Всплывающая подсказка](/material-ui/react-tooltip/#transitions)

## Производительность и SEO <meta data-oversett="" data-original-text="Performance &amp; SEO">

Содержимое компонента перехода монтируется по умолчанию, даже если `in={false}`. Это поведение по умолчанию имеет в виду рендеринг на стороне сервера и SEO. Если вы рендерите дорогие деревья компонентов внутри вашего перехода, может быть хорошей идеей изменить это поведение по умолчанию, включив параметр`unmountOnExit`:

```jsx
<Fade in={false} unmountOnExit />
```

Как и любая оптимизация производительности, это не серебряная пуля. Убедитесь, что вы сначала определили узкие места, а затем попробуйте эти стратегии оптимизации.
