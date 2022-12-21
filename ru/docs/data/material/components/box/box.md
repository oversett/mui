---
product: material-ui
title: React Box
components: Box
githubLabel: 'component: Box'
---

# Box <meta data-oversett="" data-original-text="Box">

<p class="description">Компонент Box служит в качестве компонента-обертки для большинства потребностей в утилитах CSS.</p>

Компонент Box объединяет [все функции стилей](/system/properties/), которые открыты в `@mui/system`.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Пример <meta data-oversett="" data-original-text="Example">

Функция стиля[палитры](/system/palette/).

## Реквизит `sx` <meta data-oversett="" data-original-text="The sx prop">

Все системные свойства доступны через [реквизит`sx`](/system/getting-started/the-sx-prop/) . Кроме того, реквизит `sx` позволяет задать любые другие правила CSS, которые могут вам понадобиться. Вот пример того, как его можно использовать:

{{"demo": "BoxSx.js", "defaultCodeOpen": true }}

## Переопределение компонентов MUI <meta data-oversett="" data-original-text="Overriding MUI components">

Компонент Box оборачивает ваш компонент. Он создает новый элемент DOM, `<div>`, который по умолчанию можно изменить с помощью свойства `component`. Допустим, вы хотите использовать вместо него `<span>`:

{{"demo": "BoxComponent.js", "defaultCodeOpen": true }}

Это отлично работает, когда изменения могут быть изолированы в новом элементе DOM. Например, таким образом можно изменить margin.

Однако иногда вам необходимо указать на базовый элемент DOM. Например, вы можете захотеть изменить границы кнопки Button. Компонент Button определяет свои собственные стили. Наследование CSS не поможет. Чтобы обойти эту проблему, вы можете использовать реквизит [`sx`](/system/getting-started/the-sx-prop/) непосредственно на дочернем компоненте, если это MUI-компонент.

```diff
-<Box sx={{ border: '1px dashed grey' }}>
-  <Button>Save</Button>
-</Box>
+<Button sx={{ border: '1px dashed grey' }}>Save</Button>
```

Для не-MUI компонентов используйте реквизит `component`.

```diff
-<Box sx={{ border: '1px dashed grey' }}>
-  <button>Save</button>
-</Box>
+<Box component="button" sx={{ border: '1px dashed grey' }}>Save</Box>
```

## Системные реквизиты <meta data-oversett="" data-original-text="System props">

Как компонент CSS-утилиты, `Box` также поддерживает все [`system`](/system/properties/) свойства. Вы можете использовать их как prop непосредственно на компоненте. Например, margin-top:

```jsx
<Box mt={2}>
```
