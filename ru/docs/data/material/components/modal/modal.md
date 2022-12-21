---
product: material-ui
title: React Modal component
components: Modal
githubLabel: 'component: modal'
waiAria: https://www.w3.org/WAI/ARIA/apg/patterns/dialogmodal/
unstyled: /base/react-modal/
---

# Модальный компонент <meta data-oversett="" data-original-text="Modal">

<p class="description">Компонент modal обеспечивает прочную основу для создания диалоговых окон, всплывающих окон, лайтбоксов или чего-либо еще.</p>

Компонент отображает свой узел `children` перед фоновым компонентом. `Modal` предлагает важные возможности:

-   💄 Управляет модальным стекингом, когда одного за раз просто недостаточно.
-   🔐 Создает фон для отключения взаимодействия под модалом.
-   🔐 Отключает прокрутку содержимого страницы при открытии.
-   ♿️ Правильно управляет фокусом; перемещает его на содержимое модала и удерживает его там до закрытия модала.
-   ♿️ Автоматически добавляет соответствующие роли ARIA.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

:::info
Термин "модальный" иногда используется для обозначения "диалога", но это неверное название. Модальное окно описывает части пользовательского интерфейса. Элемент считается модальным, если [он блокирует взаимодействие с остальной частью приложения](https://en.wikipedia.org/wiki/Modal_window).
:::

Если вы создаете модальный диалог, вам, скорее всего, лучше использовать компонент [Dialog](/material-ui/react-dialog/), а не напрямую Modal. Modal - это конструкция более низкого уровня, которая используется следующими компонентами:

-   [Dialog](/material-ui/react-dialog/)
-   [Ящик](/material-ui/react-drawer/)
-   [Меню](/material-ui/react-menu/)
-   [Всплывающее окно](/material-ui/react-popover/)

## Базовый модальный <meta data-oversett="" data-original-text="Basic modal">

{{"demo": "BasicModal.js"}}

Обратите внимание, что вы можете отключить контур (часто синий или золотой) с помощью свойства `outline: 0` CSS.

## Вложенный модал <meta data-oversett="" data-original-text="Nested modal">

Модалы могут быть вложенными, например, селект внутри диалога, но не рекомендуется вложение более двух модалов или любых двух модалов с фоном.

{{"demo": "NestedModal.js"}}

## Переходы <meta data-oversett="" data-original-text="Transitions">

Состояние открытия/закрытия модала может быть анимировано с помощью компонента перехода. Этот компонент должен соблюдать следующие условия:

-   Быть прямым дочерним потомком модала.
-   Иметь реквизит `in`. Он соответствует состоянию открытия/закрытия.
-   Вызывать `onEnter` callback prop, когда начинается переход enter.
-   Вызовите реквизит обратного вызова `onExited`, когда завершится переход exit. Эти два обратных вызова позволяют модалу размонтировать дочернее содержимое после закрытия и полного перехода.

Modal имеет встроенную поддержку [react-transition-group](https://github.com/reactjs/react-transition-group).

{{"demo": "TransitionsModal.js"}}

В качестве альтернативы вы можете использовать [react-spring](https://github.com/pmndrs/react-spring).

{{"demo": "SpringModal.js"}}

## Производительность <meta data-oversett="" data-original-text="Performance">

Содержимое модала размонтируется при закрытии. Если вам нужно сделать содержимое доступным для поисковых систем или отобразить дорогие деревья компонентов внутри модала, оптимизируя при этом отзывчивость взаимодействия, возможно, будет хорошей идеей изменить это поведение по умолчанию, включив параметр `keepMounted`:

```jsx
<Modal keepMounted />
```

{{"demo": "KeepMountedModal.js", "defaultCodeOpen": false}}

Как и любая оптимизация производительности, это не серебряная пуля. Убедитесь, что вы сначала определили узкие места, а затем попробуйте эти стратегии оптимизации.

## Модал на стороне сервера <meta data-oversett="" data-original-text="Server-side modal">

React [не поддерживает](https://github.com/facebook/react/issues/13097) [`createPortal()`](https://reactjs.org/docs/portals.html) API на сервере. Чтобы отобразить модальное окно, необходимо отключить функцию портала с помощью параметра `disablePortal`:

{{"demo": "ServerModal.js"}}

## Ограничения <meta data-oversett="" data-original-text="Limitations">

### Ловушка фокуса <meta data-oversett="" data-original-text="Focus trap">

Модал перемещает фокус обратно в тело компонента, если фокус пытается его покинуть.

Это делается в целях доступности. Однако это может создать проблемы. В случае если пользователям необходимо взаимодействовать с другой частью страницы, например, с окном чатбота, вы можете отключить это поведение:

```jsx
<Modal disableEnforceFocus />
```

## Доступность <meta data-oversett="" data-original-text="Accessibility">

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/dialogmodal/)](https://www.w3.org/WAI/ARIA/apg/patterns/dialogmodal/).

-   Обязательно добавьте `aria-labelledby="id..."`, ссылающийся на заголовок модала, на страницу `Modal`. Кроме того, вы можете дать описание вашего модала с помощью реквизита `aria-describedby="id..."` на странице `Modal`.
    
    ```jsx
    <Modal aria-labelledby="modal-title" aria-describedby="modal-description">
      <h2 id="modal-title">My Title</h2>
      <p id="modal-description">My Description</p>
    </Modal>
    ```
    
-   [Авторские практики WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/example-index/dialog-modal/dialog.html) помогут вам установить начальный фокус на наиболее релевантный элемент, основанный на содержимом вашего модала.
    
-   Помните, что "модальное окно" накладывается либо на основное окно, либо на другое модальное окно. Окна под модальным окном являются **инертными**. То есть пользователи не могут взаимодействовать с содержимым вне активного модального окна. Это может привести к [противоречивому поведению](#focus-trap).
