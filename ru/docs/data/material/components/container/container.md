---
product: material-ui
title: React Container component
components: Container
githubLabel: 'component: Container'
---

# Контейнер <meta data-oversett="" data-original-text="Container">

<p class="description">Контейнер центрирует содержимое по горизонтали. Это самый простой элемент макета.</p>

Хотя контейнеры могут быть вложенными, большинство макетов не требуют вложенных контейнеров.

{{"component": "modules/components/ComponentLinkHeader.js", "design": false}}

## Жидкий <meta data-oversett="" data-original-text="Fluid">

Ширина плавного контейнера ограничена значением параметра `maxWidth`.

{{"demo": "SimpleContainer.js", "iframe": true, "defaultCodeOpen": false}}

```jsx
<Container maxWidth="sm">
```

## Фиксированный <meta data-oversett="" data-original-text="Fixed">

Если вы предпочитаете разрабатывать дизайн для фиксированного набора размеров вместо того, чтобы пытаться приспособить полностью текучий видовой экран, вы можете установить реквизит `fixed`. Максимальная ширина совпадает с минимальной шириной текущей точки останова.

{{"demo": "FixedContainer.js", "iframe": true, "defaultCodeOpen": false}}

```jsx
<Container fixed>
```
